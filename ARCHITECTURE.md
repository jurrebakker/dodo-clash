# Dodo Clash: Architecture

Decided 2026-11-01 in a design grilling session. The game itself is described in
[DESIGN.md](DESIGN.md). This file covers how it is built. Background research is in
[TECH_RESEARCH.md](TECH_RESEARCH.md).

---

## 1. Overview

- **The server is the game.** A .NET server holds every match, runs the rules and owns the clock.
- **The browser is a shell.** It draws the state the server sends and calls endpoints to try to
  change it. It contains **no game rules**: no movement, no combat, no pathfinding.
- Practice mode, route previews and headless balancing all run on the server side too.

```
server/
  DodoClash.Core/          class library, zero dependencies: state, Advance(), commands,
                           map + waypoint graph, A*, combat, invader AI
  DodoClash.Core.Tests/    xUnit: unit tests, golden replays, determinism tests
  DodoClash.Server/        ASP.NET Core minimal APIs, SSE, background clock, persistence, admin
  DodoClash.Sim/           console app: headless week-in-seconds sims with bot players
client/                    Vite + TypeScript + React 19 + PixiJS v8; no game rules
data/                      JSON rules (clans, allies, invaders, heroes) and maps
assets/                    art, see assets/README.md
```

| Part | Choice |
|---|---|
| Server | **.NET 10 LTS**, ASP.NET Core minimal APIs |
| Push channel | **Server-sent events** (`TypedResults.ServerSentEvents`). Commands are plain HTTP POSTs |
| Database | **Postgres** via **EF Core** + Npgsql; game state and commands stored as `jsonb` |
| Client | **Vite + TypeScript + React 19** for HTML panels, **PixiJS v8** for the map |
| Contract | ASP.NET OpenAPI document → `openapi-typescript` → `client/src/api/types.ts` (committed) |
| Tests | xUnit (+ Testcontainers from M5), one Playwright smoke test from M5 |
| Deployment | One Docker image (server + client), docker compose with Postgres on a server at work |
| Repo / CI | GitHub (`jurrebakker/dodo-clash`), GitHub Actions |

---

## 2. Time model: continuous, no ticks

- Game time is an **integer number of island minutes** since the match started.
  **1 island minute = 10 real seconds** while the clock runs (1 island hour ≈ 10 real minutes).
- Everything happens at an exact minute: edge traversals, contacts, battle resolutions,
  hour/day boundaries (eggs, Fruit, den breeding) and ship arrivals.
- `Core` exposes two entry points:
  - `Advance(state, rules, toMinute)`: processes all events up to `toMinute` in time order.
  - `ApplyCommand(state, rules, command)`: applies a command **at the current minute**.
- **Orders take effect immediately.** When a command arrives, the server advances the match to
  "now" and applies it. A flock leaves straight away and the client sees it within a second.
  While the clock is paused the order is applied too; the flock starts moving when the clock resumes.
- **Edge durations are whole minutes** (base stride × terrain factor, e.g. 90 or 45 minutes), so
  every event time is an integer.
- Invader AI re-decides only on events (arriving at a waypoint, a battle ending, a den spawn)
  and on every island-hour boundary.

### 2.1 Positions, contact and battles

- A position is either **a waypoint** or **a point on an edge** (`edge`, `offsetMinutes`).
- **Contact** (Blight-style) happens when enemies:
  1. cross each other on an edge (moving in opposite directions),
  2. overtake each other on the same edge,
  3. meet at a waypoint or location where one of them stands,
  4. enter an edge on which the other stands still.
- A crossing minute is **rounded down** to a whole minute.
- At contact a **battle** is created at that point, possibly mid-edge. Both groups are **pinned**
  there and the battle resolves **60 island minutes later**. Units of either side that reach that
  point during the hour join it. A pinned flock may receive a new order; it takes effect after the battle.
- Survivors may stand mid-edge. Any order from there starts by walking to one end of the edge.
  Players cannot choose to stop mid-edge themselves. The route planner can target a battle point.

### 2.2 Clock and active hours

- A match stores `GameMinute` and `LastAdvancedAt` (real time). Active time only accumulates
  **while the server is running**, so downtime behaves like a pause: a deploy never causes a burst
  of catch-up battles. On startup `LastAdvancedAt` is reset to "now".
- The active-hours calendar is a pure, heavily tested function:
  `ActiveMinutesBetween(from, to, schedule)`, using `TimeZoneInfo` with IANA IDs
  (`Europe/Amsterdam`), including DST changes.
- The server reads time only through **`TimeProvider`**, so tests can fake "Friday 17:29".
- The end-of-week deadline counts in **island minutes**, not calendar dates.

---

## 3. Core: game state and rules

- **Plain data.** The state is mutable POCO classes with public properties, entities in
  `Dictionary<string, T>` keyed by ID (`Flocks`, `InvaderGroups`, `Colonies`, `Battles`, …).
  Logic lives in static functions (`Movement.Advance`, `Combat.Resolve`, …). No behaviour on the data classes.
- Serialised with **System.Text.Json source generation**. A snapshot is the JSON of the state.
- **Mutated in place, no clone.** If `Advance` or a command throws, the server discards the
  in-memory match and rebuilds it from the last snapshot plus the command log.
- **Core has zero I/O and zero dependencies.** The server loads `data/*.json` into a typed `Rules`
  record (validated at startup, errors name the bad field) and **copies it, including the map,
  into the match when it is created**. Core functions receive `rules` as a parameter; there are no
  static balance constants.
- The **waypoint grid** is generated deterministically from the map (ASCII hex grid + locations
  JSON) every time a match loads; it is never stored. Hex math and A* are our own small module,
  following Red Blob Games.
- **Invader AI:** one behaviour class per species implementing
  `ChooseTarget(state, rules, group)`. Behaviour parameters (search radius, flee ratio) live in `data/`.
- Core returns **events** (contact, battle resolved, AI retarget, colony under attack). The server
  logs them and turns them into SSE messages and inbox items. Core itself doesn't log.

### 3.1 Determinism

Exact replay is a **server-side** guarantee (the client runs no rules).

- Banned in `Core`, enforced with `Microsoft.CodeAnalysis.BannedApiAnalyzers`: `DateTime.Now`/`UtcNow`,
  `System.Random`, `Guid.NewGuid`, `Math.Pow`/`Exp`/`Log`/`Sin`/`Cos` and friends, and `float`.
- Randomness comes from our own **PCG32** generator whose state is stored in the game state.
- IDs come from a counter in the state.
- **Never let `Dictionary`/`HashSet` iteration order affect outcomes**: iterate sorted by ID
  wherever order matters.
- The square law `(loser / winner)²` is a plain multiplication.

---

## 4. Server

### 4.1 Runtime model

- **One server instance.** This is a hard assumption; there is no scaling out.
- Every running match lives in memory as a `MatchHost` with its own `SemaphoreSlim`.
- One `BackgroundService` advances all running matches every **10 real seconds** (1 island minute).
- A command takes the match lock, advances to now, validates and applies, appends to the command
  log, and pushes the new state over SSE.
- A **snapshot is written every island hour**, and the command log as commands arrive.
- On graceful shutdown every match is snapshotted at its current minute.

### 4.2 API

| Endpoint | Purpose |
|---|---|
| `GET /api/matches/{id}/map` | Static map data, fetched once: hexes, waypoints, edges, edge durations, locations |
| `GET /api/matches/{id}/state` | Full dynamic state (also sent over SSE) |
| `GET /api/matches/{id}/events` | SSE: full dynamic state on every change, plus events (contact, battle, inbox) |
| `POST /api/matches/{id}/commands` | One command; a `[JsonPolymorphic]` union with a `"type"` discriminator (`move`, `train`, `merge`, `split`, …). 200 = accepted, 422 = rejected with a reason |
| `POST /api/matches/{id}/route-preview` | `{unitId, via[]}` → `{path, minutes}`. Drives route lines and travel-time labels |
| `POST /api/matches/{id}/practice/{skip-day,reset,set-speed}` | Practice matches only; 403 on real matches |
| `/api/admin/...` | `pause`, `rollback?toMinute=`, `inspect`; protected by an admin key from configuration |
| `/join/{code}` | Invite link: pick a name, get a player cookie |

- **Identity:** joining sets an **HttpOnly cookie** scoped to the match (`EventSource` can't send
  headers, and tokens never go in URLs). Company SSO later.
- **Rollback / admin** goes through the admin endpoints of the running server, never directly
  to the database (the in-memory match would overwrite it). A tiny CLI may wrap them.

### 4.3 Persistence

- **EF Core** with the Npgsql provider and EF migrations. Tables: `matches`, `players`,
  `commands`, `snapshots`, `inbox`. Game state and command payloads are `jsonb`.
- The command log stores `(gameMinute, seq, command)`. Replay = snapshot + commands in order.
- Every snapshot records **`SchemaVersion`** and **`BuildVersion`**. On load, state migrations run on
  `JsonNode` (not typed classes), chained v1→v2→…. Logged commands are versioned and migrated the same way.
- **Exact replay is only guaranteed within one build.** A rollback to before a deploy loads the old
  snapshot and re-simulates with the new code, which may diverge. That's acceptable.
- **Practice matches** (`Practice = true`): one player, configurable clock speed, active hours
  ignored, extra practice endpoints, **in memory only** (never persisted).

### 4.4 Logging

Built-in `ILogger` with JSON console output (read with `docker compose logs`), with a per-match
scope (`matchId`, `gameMinute`). No Serilog or OpenTelemetry for now.

---

## 5. Client

- **React 19** renders the HTML: top bar, side panels (colony / flock / den), train/merge/split,
  inbox, toasts, lobby, battle report, end screen.
- **One tiny external store** holds the server state (from SSE) and local UI state (selection,
  route being planned, open panel). React reads it with `useSyncExternalStore`. No Redux.
- **PixiJS** is owned by an imperative **`MapRenderer`** class, mounted once in a `<MapCanvas>` div.
  It subscribes to the same store and sends back `selectUnit` / `planRoute` / `hover`. Map tokens are
  not React components.
- **Smooth movement:** each moving unit in the state carries its current segment
  `{fromPoint, toPoint, startMinute, endMinute}`. The renderer lerps the token along it every frame.
  That is drawing, not rules: if the next update disagrees, the token snaps.
- **Route previews** come from the `route-preview` endpoint, debounced ~100 ms on hover.
- **Pan and zoom** are our own (~150 lines): wheel zoom toward the cursor, drag to pan, WASD, clamped to 25–200%.
- **Terrain** is drawn once into chunks of 16×16 hexes with Pixi v8 `cacheAsTexture`. Hard edges
  between hex tiles stay until the final art solves them with transition overlays.
- **Layers**, bottom to top: terrain chunks → footpaths → waypoint lattice → locations → routes →
  tokens → markers/labels → hover/selection.
- **Assets:** individual PNGs loaded through a generated manifest. Pixi's AssetPack (atlases +
  mipmaps) comes when the final art arrives; file names stay the same.
- **Types** for state and commands are generated from the server's OpenAPI document
  (`npm run gen:api`) and committed. CI fails if they are stale.

---

## 6. Testing

- **Core:** xUnit unit tests (combat maths, movement, contact detection, A*, active-hours calendar).
- **Golden replays:** small scenario files (map + rules + timestamped commands) with a checked-in
  hash of the final state. A changed hash means a deliberate rule change or a bug.
- **Determinism test:** run the same scenario twice in one process, and once with shuffled
  dictionary insertion order; the hashes must match.
- **Server (from M5):** integration tests with `WebApplicationFactory` + Testcontainers Postgres.
- **Client:** almost no tests (it has no rules). One Playwright smoke test from M5:
  join, see the map, move a flock.
- **Balancing:** `DodoClash.Sim` runs whole weeks headless with bot players (from M4).

---

## 7. Development and operations

- **Local loop:** `dotnet watch` for the server, the Vite dev server proxying `/api` to it.
  From M5, Postgres via `docker compose up db`. No .NET Aspire.
- **Docker:** a multi-stage Dockerfile: Node builds `client/`, `dotnet publish` builds the server,
  and the client build goes into the server's `wwwroot`. ASP.NET serves both.
- **Production:** `docker compose` (app + Postgres with a volume) on a server at work, a nightly
  `pg_dump` into a mounted `backups/` folder, plain HTTP inside, TLS from the existing reverse proxy.
- **CI (GitHub Actions):** `dotnet test`, client typecheck/lint/build, generated-types check, Docker build.

---

## 8. Milestones (technical view)

The game milestones are in [DESIGN.md §12.2](DESIGN.md#122-milestones-each-one-playable).

1. **M1:** Core (map, waypoint graph, continuous movement, contact) + tests, a minimal ASP.NET app
   with one in-memory practice match, and a client that draws the map and moves one flock.
2. **M2–M3:** battles, invaders, economy, all in memory. M3 ends with deploying the Docker image
   so colleagues can try practice mode.
3. **M4:** the real map, balancing with `DodoClash.Sim`.
4. **M5:** Postgres, snapshots and command log, migrations, lobby, invite links, cookies, inbox,
   admin endpoints, integration and smoke tests.

---

## 9. Repository

- GitHub: <https://github.com/jurrebakker/dodo-clash> (public, no license yet: all rights reserved).
- Default branch `main`.
- `reference/` (screenshots and video frames of Blight of the Immortals) is **kept locally only**
  and is in `.gitignore`, so the public repo doesn't redistribute another game's art. Links to it in
  [GAMERULES.md](GAMERULES.md) and [WORLD.md](WORLD.md) only work in a local checkout.

# Technology Research: how games like this are built

Researched 2026-10-31. Purpose: choose a tech stack for Dodo Clash (see [DESIGN.md](DESIGN.md)).

---

## 1. How Blight of the Immortals is built

Nobody seems to have written about Blight's tech stack, so we checked it **directly**.
We opened <https://blight.ironhelmet.com/> in a browser and looked at what the page
loads (build 1052).

### Client (runs in the browser)
| Part | What Blight uses | What it does |
|---|---|---|
| Language | **Plain JavaScript**, one minified file (`blight.1052.min.js`, about 570 KB) | All game and UI code |
| UI framework | **"Crux"**, their own small framework: widgets (`Button`, `Tab`, `DropDown`, `Text`, `Image`…), an animation system with easing, a main loop and text formatting/localisation | Panels, buttons and menus are **HTML elements (DOM)**, not drawn on a canvas |
| Helper library | **jQuery** | DOM manipulation |
| Map | **HTML5 Canvas 2D** (`getContext("2d")`, `drawImage`, `requestAnimationFrame`). **No WebGL** | The map, hexes and tokens are drawn as images on a canvas |
| Audio | **Howler.js** | Sound effects |
| Touch | **Hammer.js** | Pinch and swipe gestures on phones and tablets |
| Keyboard | **Mousetrap** | Keyboard shortcuts (Space, Q, E, WASD…) |
| Code structure | Separate modules: `Universe` (game state), `UniversePathfinder` (route finding), `UniverseTargeter` (target selection), `Map` (drawing), `Interface*` (screens), `Inbox`, `Tutorial`, `Collection` | **Game logic is kept separate from drawing and UI** |

### Server
- The response header `server: Google Frontend` means it runs on **Google Cloud** (most
  likely App Engine, though that's an inference).
- The client sends requests to two endpoints: **`/grequest/`** (game actions) and
  **`/mrequest/`** (meta: menus, collection, scores).
  That's a classic **request/response API**, not live sockets. It suits a slow real-time game:
  the server keeps the clock, and the client only fetches the state and sends orders.
- The code mentions Steam 61 times, so there's also a Steam version of the same web code.

### What we can learn from this
1. **You don't need a heavy engine.** A 2D canvas for the map and HTML for the panels was
   enough for a complete, commercially released game.
2. **Map on a canvas, UI in HTML.** Panels, lists, buttons and text are much easier to build
   in HTML/CSS. Only the map needs a canvas.
3. **Game logic as its own layer** (Universe, Pathfinder) apart from drawing (Map) and screens
   (Interface). That makes multiplayer possible later, because the server can run the same logic.
4. **Touch and keyboard** were important from the start (Hammer.js, Mousetrap).

---

## 2. How similar modern browser games are built

| Project | Stack | Note |
|---|---|---|
| **Ancient Beast** (hex, turn-based) | TypeScript + **Phaser**, Webpack, Jest | Open source and featured by Phaser in 2025 |
| **Konkr.io** (hex strategy) | TypeScript + **Phaser 3**, ImmutableJS for game state | Immutable state makes undo and replay easy |
| Hex 4X study project (Novout/history) | **PixiJS** v6 + Vite + Vue 3 | Map in Pixi, UI in Vue. The same split as Blight |
| Operation Hex | Plain HTML5 Canvas + TypeScript + Vite + GSAP | No game framework at all |

Takeaway: for **turn-based** hex games, the choice of rendering library matters less than
**how you structure the game state**.

### Useful building blocks
- **Red Blob Games: Hexagonal Grids** (<https://www.redblobgames.com/grids/hexagons/>).
  The standard reference for hex coordinates, distance, neighbours, pathfinding and drawing.
  It includes TypeScript examples.
- **Honeycomb** (<https://github.com/flauwekeul/honeycomb>): a TypeScript hex grid library
  based on Red Blob Games.
- **PixiJS v8** (<https://pixijs.com/blog/pixi-v8-launches>): a fast 2D renderer using
  WebGL and WebGPU. The latest version is 8.20 (August 2026). WebGL is the default because WebGPU support
  still varies between browsers.
- **Phaser** (<https://phaser.io>): a complete game framework with scenes, input, tweens,
  audio and asset loading.
- **boardgame.io**: a framework for turn-based games (turns, phases, multiplayer). It doesn't
  look actively maintained right now, so it's not a good foundation.
- **Howler.js**: audio, the same library Blight uses.

---

## 3. Options for Dodo Clash

| | A. TypeScript + PixiJS + HTML UI | B. TypeScript + Phaser | C. TypeScript + plain Canvas 2D |
|---|---|---|---|
| Closest to Blight's proven setup | ✅ The same split (canvas map + HTML panels) | ➖ Everything inside the engine | ✅ Exactly like Blight |
| Hand-drawn sprites, zoom and pan, many tokens | ✅ Fast, made for this | ✅ Good | ➖ You build it all yourself |
| Panels and menus | ✅ HTML/CSS (easy) | ➖ Phaser UI is clunky, though HTML overlays are possible | ✅ HTML/CSS |
| How much you need to learn | Medium | Medium to high (framework concepts) | Low, but more work later |
| Animation and effects (cute style) | ✅ Good, plus GSAP for tweens if wanted | ✅ Built in | ➖ Build it yourself |
| Lock-in | Low (it's just a renderer) | High | None |

---

## 4. Recommendation

> Superseded by [§6](#6-update-2026-11-01-net-server-thin-client): the game logic moved to a .NET
> server, the client has no `core/`, there are no turns or ticks, and tests use xUnit. We also write
> our own hex module instead of using Honeycomb. The client side (Vite, PixiJS map, HTML panels) still holds.

**Option A: TypeScript + Vite + PixiJS (map) + HTML/CSS (UI)**, set up in three layers:

```
src/
  core/      pure game logic: map, units, combat, invader AI, turns
             (no drawing, fully testable, could later run on a server for co-op)
  render/    PixiJS: hex map, terrain, tokens, move lines, battle markers, animations
  ui/        HTML/CSS: top bar, colony/flock/den panels, battle report, menus
  data/      JSON: maps, clans, allies, invaders, heroes (numbers stay easy to tune)
```

Why:
- It's **the same architecture as Blight**, which has worked in browsers since 2013:
  a canvas map, HTML panels and separate game logic. Only the tools are more modern.
- **TypeScript** catches mistakes in game rules early, and **Vite** gives instant reloads while developing.
- **PixiJS** comfortably handles the cute hand-drawn style with zooming and many tokens,
  without being a full engine.
- **`core/` stays separate from everything else**, so the single-player version can grow into co-op later.
- **Testing** with Vitest on `core/` (combat formulas, movement, den spawning).
- **Hosting:** ~~single player needs no server; static hosting and `localStorage` saves.~~
  Superseded on 2026-11-01, see [§5](#5-update-2026-11-01-co-op-over-an-office-week).

Choose **B (Phaser)** instead if you'd rather have more built in (scenes, sound, tweens)
and don't mind tying the game to an engine.

Check the exact package versions when we set the project up.

---

## 5. Update 2026-11-01: co-op over an office week

> Superseded by [§6](#6-update-2026-11-01-net-server-thin-client): there is no shared `core/`,
> no ticks (snapshots are hourly), login uses a cookie instead of a browser token, and practice
> mode runs on the server instead of as a static site. Postgres, SSE and Docker still hold.

The game changed from single player with turns to **co-op for 2–6 colleagues over one office
week**, with a clock that only runs during active hours (see [DESIGN.md](DESIGN.md) §3 and §11).
Option A still holds for the client, but a server is now needed.

```
core/      pure game logic, shared by client and server; deterministic (seeded RNG in the state)
client/    Vite + PixiJS map + HTML/CSS UI; also runs core/ locally for the practice mode
server/    HTTP API + server-sent events ("a new tick happened"); runs ticks in the background
data/      JSON: maps, clans, allies, invaders, heroes; copied into a match when it starts
```

- **Communication:** HTTP for orders and state, **SSE** for tick updates. No WebSockets: ticks
  are ~10 real minutes apart.
- **Storage:** **Postgres**. Per match an **order log** and a **state snapshot per tick**, so any
  moment can be replayed and an admin can roll back. The state has a schema version and migrations.
- **Deployment:** one **Docker** image serving client and server. docker compose (with Postgres)
  for local testing, and a server at work for real matches.
- **Login:** invite link + browser token first, company SSO later.
- **Practice mode:** the client can also be built as a static site without a server (milestone 3).

---

## 6. Update 2026-11-01: .NET server, thin client

§5's shared TypeScript `core/` is **superseded**. The server is written in **.NET 10** and is
the only place the game rules live. The browser is a thin TypeScript shell (Vite + React 19 +
PixiJS) that draws the state and calls endpoints; practice mode and route previews run on the
server too. Ticks are replaced by a continuous clock counted in island minutes, so orders take
effect immediately and units can meet mid-edge, as in Blight. The full set of decisions is in
[ARCHITECTURE.md](ARCHITECTURE.md).

---

## Sources
- Blight of the Immortals client, inspected directly: <https://blight.ironhelmet.com/>
- Iron Helmet Games (studio info): <https://giantbomb.com/wiki/Companies/Iron_Helmet_Games>
- Ancient Beast (Phaser, hex, turn-based): <https://phaser.io/news/2025/09/ancient-beast>
- Konkr.io (Phaser 3, hex strategy): <https://phaser.discourse.group/t/phaser-3-konkr-io-a-pretty-polished-turn-based-strategy-game/12098>
- Hex 4X with PixiJS + Vue: <https://github.com/Novout/history>
- Operation Hex (Canvas + TS): <https://multiserver.itch.io/operation-hex>
- Red Blob Games, hex grids: <https://www.redblobgames.com/grids/hexagons-v1>
- Honeycomb hex library: <https://github.com/flauwekeul/honeycomb>
- PixiJS v8: <https://pixijs.com/blog/pixi-v8-launches>, <https://gamedev.net/news/5221-pixijs-v8200-released/>
- boardgame.io releases: <https://github.com/boardgameio/boardgame.io/releases>

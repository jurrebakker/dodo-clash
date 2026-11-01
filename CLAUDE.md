# Dodo Clash

A co-op browser strategy game for 2–6 colleagues over one office week: dodos and native allies
of Mauritius (1598) against introduced species. Hobby project, English only.

## Where things are

| File | Read it for |
|---|---|
| [DESIGN.md](DESIGN.md) | The game: rules, map, time, combat, interface, milestones (§12.2) and decisions (§12.3) |
| [ARCHITECTURE.md](ARCHITECTURE.md) | How it's built: .NET server, thin client, time model, API, persistence, testing, ops |
| [GAMERULES.md](GAMERULES.md), [WORLD.md](WORLD.md) | Notes on the reference game (Blight of the Immortals). Genre reference only, never copy it |
| [TECH_RESEARCH.md](TECH_RESEARCH.md) | Background research behind the stack. §4–§5 are partly superseded by §6 |
| [assets/README.md](assets/README.md) | Placeholder art: folders, sizes, how to re-export PNGs from `assets/source/` |
| `prompts/` | Local only, git-ignored: prompts used to generate assets with Claude Design |
| `reference/` | Local only, git-ignored: screenshots of the reference game. Not in the public repo |

If a decision isn't in DESIGN.md or ARCHITECTURE.md, it hasn't been made: ask before assuming.
When a decision changes, update those files in the same change.

## Current state

Design is settled; **no code yet**. The next step is milestone 1 (ARCHITECTURE.md §8).
Update this section and add build/test commands once the projects exist.

## Rules that are easy to break

- **The server is the game.** All rules live in `server/DodoClash.Core`. The client (`client/`)
  only draws state and calls endpoints. No movement, combat or pathfinding in TypeScript.
- **`DodoClash.Core` has no I/O and no dependencies**, and must stay deterministic. Follow the
  banned-API list and rules in ARCHITECTURE.md §3.1.
- Game time is integer island minutes, with no ticks (ARCHITECTURE.md §2). Balance numbers come
  from `data/` via the `Rules` parameter, never constants in code.
- Game state is plain mutable POCOs keyed by ID; logic lives in static functions.
- `client/src/api/types.ts` is generated from the server's OpenAPI document. Don't edit it by hand.
- Art follows the sizes and names in DESIGN.md §10.1 (`assets/<atlas>/<kind>-<name>.png`).
- Don't copy names, text, art or numbers from the reference game (DESIGN.md §13).

## Writing style for docs

Plain, short sentences; tables for comparisons; mark unbuilt features *Not in the MVP*.

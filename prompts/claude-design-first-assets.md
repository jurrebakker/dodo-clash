# Claude Design prompt: first asset set for Dodo Clash

Paste everything below the line into Claude Design. The sizes and names come from
[DESIGN.md §10.1](../DESIGN.md#101-art-specs); update both together.

---

I'm building **Dodo Clash**, a co-op browser strategy game. I need a **first asset set** so we
can start testing the map and the core rules, plus **one composite screen** that shows how the
game might look with those assets. These are early assets: clear and consistent matter more
than polish, but they should already point at the final style.

## The game in short

Mauritius, 1598. Ships bring sailors, pigs and rats to an island where the dodo never had an
enemy. 2–6 colleagues play together as dodo clans, over one office week, defending their
nesting colonies and destroying the dens where invaders breed. Tone: light and a bit funny on
the surface (clumsy, chunky birds fighting back), with a melancholy layer underneath.

The map is a **flat-top hex grid** of terrain. On top of it lies a **triangular grid of
waypoints** (thin dashed lines). Units are round tokens that move from waypoint to waypoint.
Panels and menus are HTML next to the map, not drawn on it.

## Style

- **Cute and hand-drawn**: chunky, round, charming animals with thick soft outlines and
  slightly wobbly lines, like an illustrated children's nature book. Warm and readable.
- Terrain is painterly but **calm**, so tokens and icons stand out on top of it.
- One consistent light direction (top left) and one outline weight across all assets.
- Everything must be **original**. Do not imitate Blight of the Immortals or any other game's
  art, icons or layout details.
- The animals are real species; keep them recognisable (the dodo's hooked beak and tuft of
  tail feathers, the giant tortoise's domed shell), but cartoon proportions are welcome.

## Technical specs (strict)

- All raster assets are drawn **at 2×**, as **PNG with transparent background**.
- Hex tiles are **flat-top, 256 × 222 px**, and must **tile seamlessly** with their neighbours,
  including where two different terrains meet (keep edges soft and the hex border itself
  invisible; the game draws a faint grid on top).
- Token portraits are **128 × 128 px**, the animal centred in a circle of ~112 px diameter,
  **without** a frame (the frame is a separate sprite so we can recolour it per player).
- Location icons are **128 × 128 px**, drawn as a small scene that sits on a waypoint.
- Map markers are **64 × 64 px**.
- UI icons are **SVG on a 24 px grid**, single colour (`currentColor`) so the HTML can tint them.
- Use exactly these file names.

## Asset list

### Terrain (`terrain/`)
| File | Content |
|---|---|
| `terrain-coast.png` | sandy beach with a bit of lagoon edge |
| `terrain-grassland.png` | open dry grass of the central plateau |
| `terrain-forest.png` | dense ebony rainforest, dark green |
| `terrain-marsh.png` | Mare aux Songes: reeds, pools, mud |
| `terrain-mountains.png` | volcanic basalt peaks (Le Pouce, Black River Gorges) |
| `terrain-water.png` | turquoise lagoon / sea, a hint of reef |
| `edge-footpath.png` | 256 × 32 px trampled trail, drawn along one edge between two waypoints, tileable lengthwise |

### Locations (`terrain/`)
| File | Content |
|---|---|
| `loc-colony.png` | dodo nesting ground: grass nests with a few eggs |
| `loc-colony-wild.png` | the same, but untamed and overgrown (not yet claimed by a player) |
| `loc-ruin.png` | a fallen colony: trampled, broken eggshells, melancholy |
| `loc-harbour.png` | a small wooden jetty with a rowing boat, a 1600s Dutch ship in the distance |
| `loc-settlement-tortoise.png` | giant tortoise resting ground |
| `loc-den-pig.png` | muddy pig wallow |
| `loc-den-rat.png` | rat nest in a hollow log |
| `loc-den-sailor.png` | sailors' camp: tent, campfire, barrel |

### Units (`units/`)
| File | Content |
|---|---|
| `unit-dodo-forest.png` | Forest Dodo (*Peck Flock*): balanced, brave, a leaf in its feathers |
| `unit-dodo-marsh.png` | Marsh Dodo (*Mud Guard*): stocky, mud-splashed, stubborn |
| `unit-dodo-highland.png` | Highland Dodo (*Rock Beaks*): big, grey-tinged, tough |
| `unit-dodo-shore.png` | Shore Dodo (*Tide Runners*): leaner, quick, sandy |
| `unit-tortoise.png` | Giant tortoise ally: huge, slow, kind |
| `unit-sailor.png` | Dutch sailor, around 1600: a threat, but cartoonish, not gory |
| `unit-pig.png` | feral pig: tough, snout down, after eggs |
| `unit-rat.png` | a small swarm of rats |
| `frame-dodo.png` | 128 × 128 round frame ring, green, with a neutral inner ring we tint per player |
| `frame-invader.png` | 128 × 128 round frame ring, red |
| `badge-strength.png` | 64 × 32 px rounded badge for the strength number (number drawn by the game) |
| `marker-battle.png` | 64 × 64 crossed beak-and-snout or similar clash symbol |
| `marker-flee.png` | 64 × 64 retreat symbol (dust cloud with an arrow) |

### UI icons (`ui/`, SVG)
`icon-fruit.svg`, `icon-courage.svg` (a feather), `icon-egg.svg`, `icon-dodo.svg` (population),
`icon-clock-running.svg`, `icon-clock-paused.svg`, `icon-inbox.svg`, `icon-train.svg`,
`icon-merge.svg`, `icon-split.svg`.

## Composite screen

Make one **1440 × 900** mock-up of the game in a desktop browser, built from the assets above
at **100% zoom** (hex 128 px wide, tokens 64 px). It should show:

- **Top bar:** "Day 3 · 14:00", clock state "running · pauses at 17:30", Fruit 42, Courage 7,
  inbox with a red badge "2".
- **Map** (most of the screen): the south-east coast of Mauritius around Mare aux Songes.
  Coast, marsh, forest and a mountain ridge, with the faint dashed triangular waypoint grid on top.
  - A harbour on the coast with a ship in the lagoon.
  - The player's **Marsh Dodo colony**, a **pig den** two waypoints away, a **ruin** further inland.
  - A **Marsh Dodo flock** token (strength 24) moving toward the pig den: a dashed move line
    along the waypoints with a small travel-time label "2h".
  - A teammate's **Forest Dodo flock** (strength 15, different player-colour ring) arriving
    from the forest.
  - A **battle marker** on the waypoint where 3 pig tokens (strength 30) meet a Highland flock.
  - A few rat tokens near the den.
- **Right panel** (HTML style, ~320 px wide): the selected colony: name "Mare aux Songes",
  adults 38, eggs 12, Fruit per day, a "Train flock" button with cost, and a short warning
  line about not training away the last adults.
- **Inbox toast** bottom left: "🐖 Pigs are heading for your colony."
- Panels use the same hand-drawn feel (paper texture, rounded corners), but text must be
  crisp and readable.

## What I want back

1. The asset sheet(s), with every asset labelled by file name and shown at its real size.
2. The composite screen.
3. A short note on the palette (hex values for terrain base colours, the dodo green, the
   invader red and 6 player colours that stay distinct from both, including for colour-blind
   players).

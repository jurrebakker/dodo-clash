# Assets

Placeholder art for the first playtests. Sizes and file names follow
[DESIGN.md §10.1](../DESIGN.md#101-art-specs), so the final art can replace these files one for one.

| Folder | Contents |
| --- | --- |
| `terrain/` | Hex tiles (256 × 222), `edge-footpath` (256 × 32), location icons (128 × 128) |
| `units/` | Token portraits and frames (128 × 128), `badge-strength` (64 × 32), markers (64 × 64) |
| `ui/` | Panel icons: SVG on a 24 px grid in `currentColor` |
| `source/` | The vector source of every PNG, same names and sizes |

All PNGs are drawn at 2× with a transparent background. `frame-dodo.png` has a neutral inner
ring that the game tints with the player colour, and the game draws the number on
`badge-strength.png`.

To re-export a PNG after editing its SVG, render the SVG at its own size with a transparent
background, for example with headless Chrome:

```bash
chrome --headless=new --default-background-color=00000000 --window-size=128,128 --screenshot=units/unit-pig.png source/units/unit-pig.svg
```

Known gaps: neighbouring hex tiles meet with a hard edge instead of blending.
The design canvas these came from: https://claude.ai/artifact/HfbihA7L4wijQJ1JCbqc86

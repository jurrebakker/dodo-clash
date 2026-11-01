# First assets (placeholder art)

Source files of the Claude Design canvas made from
[prompts/claude-design-first-assets.md](../../prompts/claude-design-first-assets.md).
Live canvas: https://claude.ai/artifact/HfbihA7L4wijQJ1JCbqc86 (private until shared).

These are vector stand-ins, not the final 2× PNGs. Every asset is drawn at its real size from
[DESIGN.md §10.1](../../DESIGN.md#101-art-specs) and labelled with its final file name, so the
sheets double as the spec for the real art pass.

| File | What it is |
| --- | --- |
| `Main.dc.html` | Composite screen, 1440 × 900 |
| `SheetTerrain.dc.html` | Hex tiles, tiling check, footpath, locations |
| `SheetUnits.dc.html` | Token portraits, frames, strength badge, markers |
| `SheetUI.dc.html` | UI icons and the palette |
| `Hex`, `Location`, `Token`, `Sprite`, `Icon` `.dc.html` | Reusable parts the sheets and screen are built from |
| `canvas.json` | Artboard layout of the canvas |

The `.dc.html` files load `./support.js` from the canvas runtime, so they only render inside
Claude Design, not when opened directly in a browser.

Still open for the real art: hex edges meet hard instead of blending, and the screen shows
`[N]` Fruit per day and `[cost]` for training because the rules don't fix those numbers yet.

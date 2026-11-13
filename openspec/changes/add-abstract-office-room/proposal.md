# Proposal: add-abstract-office-room

## Why
The photo scan of the office is accurate but visually noisy (smeared glass, clutter, holes), which distracts from the planting interventions. A clean, stylised model in the same style as the earlier atrium, with dimensions taken from the scan, is easier to read and to change with AI.

## What changes
- New base type `room` in `scene.json`: a rectangular room defined by floor bounds, ceiling height and a list of wall segments (solid or window), drawn in the same low-poly style as the atrium.
- Office dimensions from the scan: about 3.5 × 7.8 m, ceiling 2.7 m, window walls on the east side and the north end, solid west and south walls.
- Furniture as editable objects (so AI can also move or remove it): two desk rows of 4 desks each with olive divider screens, monitors and office chairs, plus a whiteboard. New object types: `desk`, `desk-divider`, `monitor`, `office-chair`, `whiteboard`.
- Existing plants and zones stay as they are.
- The scan version is kept as `scene-office-scan.json`; `scene.json` becomes the abstract office.
- `AI-EDITING.md` lists the new types and the `room` base block.

## Impact
- Modified capabilities: `scene-rendering` (room base), `scene-description` (room block, furniture types).
- Changed files: `index.html`, `scene.json`, `AI-EDITING.md`; new `scene-office-scan.json`.
- Risks: desk count and exact positions are read from a noisy scan (±20 cm); details such as doors, radiators and cabinets are left out unless you name them.

# Proposal: improve-office-realism

## Why
The clean office model is readable but looks bare and flat. More realistic materials, light and context make it a credible baseline for presenting greening interventions, while keeping it clean and AI-editable (user choice: "detailed clean model", not the scan).

## What changes
- Procedural surface textures: carpet, ceiling tiles (60 cm grid), plaster walls, fabric dividers, skirting boards.
- Light: low sun entering through the east windows with mullion shadows, soft shadows, recessed ceiling light panels with warm fill light.
- Context outside the windows: sky gradient, ground and low-poly trees, so the windows show a view.
- Desk items drawn with each desk (keyboard, mouse, mug, papers), switchable per desk with `items`.
- New base options: `ceilingLights`, `outside` (both default on).

## Impact
- Modified capability: `scene-rendering`. Changed files: `index.html`, `scene.json`, `AI-EDITING.md`.
- Risk: more lights and shadows may be slower on older laptops and phones.

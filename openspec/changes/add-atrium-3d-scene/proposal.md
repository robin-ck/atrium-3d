# Proposal: add-atrium-3d-scene

## Why
There is only a panorama photo of the atrium, which cannot be explored or modified. A stylised, navigable 3D model whose contents are described in a plain JSON file lets AI (Claude) change the space later, e.g. adding plants, without touching code.

## What changes
- New web page rendering the atrium in 3D with three.js: floor, two-storey shell, glass roof, mezzanine balcony, pillars, glazed meeting rooms, stair void with railing, elevator.
- Furniture and props from the photo: white work table with yellow chairs, wooden kitchen island with bar stools, lounge chairs, info poster frame, potted plants (existing ones as in photo).
- Scene content defined in `scene.json` (object type, position, rotation, scale, variant). A small library of object types, including several plant types (tree in pot, shrub, hanging plant, planter box, green wall panel).
- Navigation: orbit mode (default) and first-person walk mode (WASD + mouse) with a toggle button.
- A short `AI-EDITING.md` guide: how to ask Claude to change the scene and the JSON schema.
- Published as a private claude.ai artifact.

## Impact
- New capabilities: `scene-rendering`, `scene-description`.
- New files: `index.html`, `scene.json`, `AI-EDITING.md`.
- Risks: proportions are estimated from one photo (approx. ±1 m accuracy); walk mode is not usable on touch devices.

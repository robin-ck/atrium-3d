# Proposal: add-splat-view

## Why
The user wants a Gaussian-splat look. The uploads are textured meshes, not splat captures, so the chosen route (user choice) is a splat-style rendering of the existing partial atrium scan.

## What changes
- New base type `splats`: a point file of soft, coloured blobs (sampled from the scan surface, ~345k points, levelled and scaled to metres) drawn with a soft-edged shader.
- `scene.json` becomes the splat view; the stylised atrium moves to `scene-atrium.json`.
- Options: `splatSize`, `softness`, `clipHeight` (ceiling cut in orbit mode).

## Impact
- Modified capability: `scene-rendering`. New file `atrium-splats.b64.txt` (4.1 MB).
- Limits: covers only what the scan captured; it imitates a splat (no view-dependent shading); scale estimated from doorway and ceiling height (±10%).

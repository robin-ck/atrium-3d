# Proposal: refine-atrium-realism

## Why
The user uploaded a second KIRI scan, which turned out to be of the atrium (doorway, notice board, plant, pillar) rather than the office. It is too partial and lumpy to measure, so it is used as a visual reference to bring the atrium up to the realistic style of the office model.

## What changes
- The atrium becomes the default scene again (`scene.json`); the office moves to `scene-office.json` (scan: `scene-office-scan.json`).
- Atrium shell gets textures (carpet, plaster, board-marked concrete, oak), a sky seen through the glass roof, sun shadows from roof beams, downlights and warm fill light under the mezzanine.
- Details from the scan as editable objects: `doorway-corridor` (opening in the glass front into a warm, wood-lined corridor; hides the glass panes it overlaps), `notice-board` (pinned papers with a coloured header), and a large plant in a black planter.
- `AI-EDITING.md` puts the atrium first and documents the new types.

## Impact
- Modified capabilities: `scene-rendering`, `scene-description`. Changed files: `index.html`, `scene.json` (atrium), `scene-office.json` (was `scene.json`), `AI-EDITING.md`.
- Risk: positions of the new details are estimated (the scan cannot be aligned precisely with the panorama).

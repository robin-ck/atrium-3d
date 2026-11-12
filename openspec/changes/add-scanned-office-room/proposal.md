# Proposal: add-scanned-office-room

## Why
The stylised atrium is too inaccurate. A KIRI Engine scan of an office room (250k triangles, photo texture) gives a realistic, correctly proportioned base. Plants and furniture should stay editable objects on top, so AI editing keeps working.

## What changes
- Support a **scanned room** as the base of a scene: the page loads a GLB model instead of the hand-built shell.
- Convert the uploaded OBJ (30 MB) to a GLB under 15 MB, scaled to metres (scan ceiling 1.46 units → assumed 2.9 m, factor ≈ 2.0) with the floor at y = 0.
- New scene file `scene-office.json` with a `base` block (model file, scale, offset, rotation) and its own zones and objects (starts with a few plants).
- A room switch on the page: "Atrium (model)" and "Office (scan)". The atrium stays as it is.
- Walk mode in the scanned room is limited by the room's bounding box (no wall collision).
- `AI-EDITING.md` gets a section on the office room: coordinates, zones, how to place objects on desks.

## Impact
- Modified capabilities: `scene-rendering` (scan base, room switch), `scene-description` (`base` block, multiple scene files).
- New files: `office.glb`, `scene-office.json`; changes to `index.html`, `AI-EDITING.md`.
- Risks: scale is estimated (±10%); the scan has holes and smeared spots near glass and under desks; a 10 MB model loads slowly on phones.

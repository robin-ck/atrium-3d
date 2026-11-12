# Editing the room with AI

The 3D page (`index.html`) loads `scene.json`. That file now uses a **3D scan of the office room** (`office.glb`, published as base64 text in `office.glb.b64.txt` because artifacts cannot serve .glb files) as the base, and every plant or piece of furniture added on top comes from its `objects` list. To change the scene, ask Claude to edit **only the `objects` list in `scene.json`**, then republish the artifact.

The earlier stylised atrium is kept in `scene-atrium.json`. Copying it over `scene.json` brings the atrium back.

## Office room (scene.json)

- Units are metres, `y` is up, and the floor is at `y = 0`. The ceiling is at about `y = 2.7`, and desk tops are at `y = 0.74`.
- `x` runs from about -2.0 (west wall) to +1.5 (east window wall). `z` runs from about -3.9 (north end, also glazed) to +3.9 (south wall).
- Walk mode starts at the south end and looks north.
- In orbit mode the ceiling is cut off at `base.clipHeight` (2.3 m) so you can look in from above.
- The scale was estimated (scan units × 1.95, from desk height and ceiling). If things look too big or small, change `base.scale` (e.g. 1.05).

| zone id | x range | z range | notes |
|---|---|---|---|
| desks-north | -1.8 to 1.15 | -2.6 to -0.8 | desk row; desk plants go at y = 0.74 |
| desks-south | -2.0 to 1.15 | 0.3 to 2.1 | desk row; desk plants go at y = 0.74 |
| middle-aisle | -1.8 to 1.1 | -0.75 to 0.25 | keep clear |
| east-aisle | 1.15 to 1.45 | -3.4 to 3.4 | narrow, keep mostly clear |
| east-windows | 1.45 to 1.6 | -3.9 to 3.9 | glass wall; low planters can stand just in front |
| north-end | -1.9 to 1.45 | -3.9 to -2.7 | open floor, glazed end; good for large plants |
| south-end | -1.9 to 1.45 | 2.2 to 3.9 | open floor |
| west-wall | -2.0 to -1.85 | -3.9 to 3.9 | solid wall; green walls face east, so `rotation: 90` |

Office example prompts:
- "Put three large trees in the north end and a planter box along the south wall."
- "Add a small plant on every desk."
- "Cover the west wall with a green wall from z = -3 to z = 3, 2 m high."

# Atrium (scene-atrium.json)

## Coordinates

- Units are metres. `y` is up, and the floor is at `y = 0`.
- `x` runs from -14 (left wall, stair void) to +12 (concrete wall with the elevator).
- `z` runs from -12 (back wall behind the meeting rooms) to +8 (front edge, where the photo was taken).
- The photo was taken from about `(0, 1.6, 6.5)`, looking towards `-z`.
- `rotation` is in degrees around the vertical axis. At `0` an object faces `+z` (towards the viewer of the photo).

## Zones (also visible with the "Zones" button)

| id | x range | z range | notes |
|---|---|---|---|
| stair-void | -14 to -8.5 | -4 to 5 | no floor here; do not place floor objects |
| work-area | -8 to -1 | 0.5 to 7 | white work table, yellow chairs, info poster |
| lounge | -4 to 1.5 | -6 to -2 | two lounge chairs |
| kitchen | 1.5 to 9 | -4.5 to 3.5 | oak islands, bar stools, back counter |
| elevator-wall | 9.5 to 12 | -6 to 8 | black shelf with plants at x ≈ 10.6; elevator at z ≈ 4 (keep it clear) |
| meeting-rooms | -14 to 12 | -12 to -7 | behind the glass front at z = -7.3 |
| mezzanine-railing | -14 to 12 | -6.6 to -6.2 | parapet from y 3.0 to 4.6; hanging plants go here at y ≈ 2.2 to 2.8 |
| skylight | -12 to 8 | -6 to 8 | glass roof at y = 10 |
| open-floor | -1 to 9 | 3.5 to 8 | main walkway, keep at least 1.5 m clear |

Pillars stand at `x = -11.6, -7.2, 3.4` and `z = -6.5`. Mezzanine soffit (ceiling of the ground floor) is at `y = 3.0`.

## Object fields

```json
{ "id": "unique-name", "type": "plant-tree", "position": [x, y, z], "rotation": 0, "scale": 1, "variant": "medium", "size": [w, h, d], "color": "#hex" }
```

`id`, `type` and `position` are required. `scale` may be a number or `[x, y, z]`. Unknown types are shown as a pink box with a warning.

## Types

**Plants**

| type | variant | size | placement |
|---|---|---|---|
| `plant-tree` | small (~1.4 m), medium (~2.4 m), large (~3.4 m) | | position = base of the pot |
| `plant-shrub` | small, medium, large | | position = base of the pot; can stand on a shelf (y = shelf height) |
| `plant-hanging` | small, medium, large | | position = bottom of the pot; vines hang about 1 m below |
| `planter-box` | | `[width, height, depth]`, default `[1.6, 0.5, 0.5]` | position = bottom centre |
| `green-wall` | | `[width, height]`, default `[2, 2.4]` | position = bottom centre; leaves face local +z, so rotate it to face the room (e.g. `-90` on the right wall at x ≈ 11.9) |

`color` on a plant sets the pot colour.

**Furniture**: `table-work`, `chair-shell`, `chair-lounge`, `side-table`, `bar-stool`, `kitchen-island`, `counter`, `coffee-machine`, `poster-frame`, `shelf`, `booth`. Boxes take `size`; chairs take `color`.

## Example prompts

- "Add five large trees along the front edge of the stair void, 1 m apart."
- "Hang eight plants along the mezzanine parapet between x = -6 and x = 6."
- "Put a green wall 4 m wide and 3 m high on the concrete wall right of the elevator."
- "Replace the yellow chairs with green ones and add planter boxes between the work table and the kitchen."
- "Make a second version of the scene called scene-greened.json with as much greenery as possible while keeping the walkway clear."

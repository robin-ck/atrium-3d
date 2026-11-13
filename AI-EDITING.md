# Editing the room with AI

The 3D page (`index.html`) loads `scene.json`. That file describes the room (`base`) and every plant or piece of furniture in it (`objects`). To change the scene, ask Claude to edit **only `scene.json`** (usually its `objects` list), then republish the artifact.


# Atrium (scene.json, the default)

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

**Atrium details** (from the second, partial atrium scan; positions estimated): `doorway-corridor` (`size` [width, height, depth]; the opening faces +z and the wood-lined corridor runs to -z; placed on the glass front at z = -7.25 it removes the glass pane there; `surround` sets the white wall width each side), `notice-board` (`size` [w, h], bottom centre, faces +z, `header` colour and `title` text).

**Furniture**: `table-work`, `chair-shell`, `chair-lounge`, `side-table`, `bar-stool`, `kitchen-island`, `counter`, `coffee-machine`, `poster-frame`, `shelf`, `booth`. Boxes take `size`; chairs take `color`.

## Example prompts

- "Add five large trees along the front edge of the stair void, 1 m apart."
- "Hang eight plants along the mezzanine parapet between x = -6 and x = 6."
- "Put a green wall 4 m wide and 3 m high on the concrete wall right of the elevator."
- "Replace the yellow chairs with green ones and add planter boxes between the work table and the kitchen."
- "Make a second version of the scene called scene-greened.json with as much greenery as possible while keeping the walkway clear."

## Office room (scene-office.json)

`scene-office.json` is a stylised model of the office, with dimensions taken from the photo scan (the scan itself is `scene-office-scan.json`). Copy it over `scene.json` to show the office instead of the atrium.

- Units are metres, `y` is up, and the floor is at `y = 0`. The ceiling is at `y = 2.7`, and desk tops are at `y = 0.74`.
- `x` runs from -2.0 (west wall) to 1.5 (east window wall). `z` runs from -3.9 (north window wall) to 3.7 (south wall).
- Walk mode starts at the south-east corner and looks north.

### Room block

```json
"base": { "type": "room", "x": [-2.0, 1.5], "z": [-3.9, 3.7], "height": 2.7,
  "walls": [ { "side": "north", "kind": "window" }, { "side": "east", "kind": "window", "from": -3.9, "to": 0, "sill": 0.8 } ] }
```

Each wall side (`north`, `east`, `south`, `west`) is solid unless a `window` segment covers it. `from`/`to` are x values for north/south and z values for east/west. `sill` is the parapet height under the glass.

Other base options: `ceilingLights` (default on; `false` hides them, `{ "spacing": 1.8 }` sets the grid in metres), `outside` (sky, ground and trees seen through the windows; default on), `sunDirection` (vector pointing towards the sun, default `[1, 0.55, -0.45]`, i.e. low sun from the east-north-east).

### Zones

| zone id | x range | z range | notes |
|---|---|---|---|
| desks-north | -1.75 to 1.05 | -2.5 to -0.9 | 4 desks, divider at z = -1.7; desk plants at y = 0.74 |
| desks-south | -1.95 to 0.85 | 0.8 to 2.4 | 4 desks, divider at z = 1.6; desk plants at y = 0.74 |
| middle-aisle | -1.9 to 1.05 | -0.55 to 0.45 | keep clear |
| east-aisle | 1.05 to 1.45 | -3.4 to 3.4 | narrow, keep mostly clear |
| east-windows | 1.4 to 1.5 | -3.9 to 3.7 | glass wall, sill at 0.8 m |
| north-end | -1.95 to 1.45 | -3.85 to -3.0 | open floor at the windows; good for large plants |
| south-end | -1.95 to 1.45 | 2.95 to 3.65 | open floor; whiteboard on the south wall |
| west-wall | -2.0 to -1.9 | -3.9 to 3.7 | solid wall; green walls face east, so `rotation: 90` |

### Office furniture types

| type | notes |
|---|---|
| `desk` | position = floor centre, `size` [w, h, d] default [1.4, 0.74, 0.8]; the user side (keyboard, mouse, mug, papers) is local +z, so `rotation: 180` for a desk whose chair is on its north side; `"items": false` clears the desk, or list a subset such as `["keyboard", "mouse"]` |
| `desk-divider` | position = floor centre, `size` [length, top height, thickness] |
| `monitor` | position on the desk top (y = 0.74); screen faces +z, use `rotation: 180` to face -z |
| `office-chair` | faces +z; `rotation: 180` faces -z; `color` sets the upholstery |
| `whiteboard` | position = bottom centre of the board; faces +z; `size` [w, h] |

Office example prompts:
- "Put three large trees in the north end and a planter box along the south wall."
- "Add a small plant on every desk."
- "Cover the west wall with a green wall from z = -3 to z = 3, 2 m high."
- "Make the west wall a window wall too."


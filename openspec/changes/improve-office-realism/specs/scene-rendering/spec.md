# Delta: scene-rendering

## ADDED Requirements

### Requirement: Realistic office rendering
The system SHALL render the `room` base with textured floor, ceiling tiles and walls, recessed ceiling lights, directional sunlight through window walls with shadows, and an outdoor context (sky, ground, trees) visible through windows. `ceilingLights: false` or `outside: false` in `base` SHALL turn these off.

#### Scenario: Looking out
- **WHEN** the user walks to the east windows
- **THEN** trees and sky are visible outside and sunlight patches with mullion shadows lie on the floor

### Requirement: Desk items
A `desk` object SHALL draw a keyboard, mouse, mug and papers on the user side (local +z) unless `items` is `false` or a list naming a subset.

#### Scenario: Clear desk
- **WHEN** a desk has `"items": false`
- **THEN** only the desk itself is drawn

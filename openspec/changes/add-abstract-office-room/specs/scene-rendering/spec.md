# Delta: scene-rendering

## ADDED Requirements

### Requirement: Abstract room base
The system SHALL draw a stylised room from a `base` block of type `room`: floor, ceiling at the given height, and each wall segment as a solid wall or a glazed window wall with mullions. Walls facing the camera in orbit mode SHALL not block the view into the room.

#### Scenario: Office opens
- **WHEN** the user opens the page with the abstract office `scene.json`
- **THEN** a clean low-poly office with window walls on the east and north, two desk rows and the plants is shown

#### Scenario: Changing a wall
- **WHEN** Claude changes the west wall segment from `solid` to `window`
- **THEN** the west wall is drawn as glazing

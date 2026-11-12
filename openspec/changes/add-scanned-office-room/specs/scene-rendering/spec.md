# Delta: scene-rendering

## ADDED Requirements

### Requirement: Scanned room base
The system SHALL render a scene's base from a GLB model when the scene file has a `base` block of type `scan`, applying its scale, offset and rotation, instead of the hand-built atrium shell.

#### Scenario: Office scan loads
- **WHEN** the user opens the page and `scene.json` has a scan base
- **THEN** the textured scan appears at real-world scale with its floor at y = 0, and the scene's objects are placed on top

#### Scenario: Model fails to load
- **WHEN** the GLB cannot be loaded
- **THEN** a message names the missing file and the objects are still shown


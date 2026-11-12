# Delta: scene-rendering

## ADDED Requirements

### Requirement: Atrium reconstruction
The system SHALL render a stylised 3D atrium matching the photo's layout: open floor, glass roof, mezzanine, pillars, glazed rooms, stair void, elevator, and the furniture listed in `scene.json`.

#### Scenario: Page opens
- **WHEN** the user opens the page
- **THEN** the atrium is shown in orbit view within 3 seconds, lit as daylight through the glass roof

### Requirement: Orbit and walk navigation
The system SHALL offer orbit mode (rotate, pan, zoom) and first-person walk mode (WASD/arrow keys + mouse look at 1.6 m eye height), switchable via an on-screen button.

#### Scenario: Switch to walk mode
- **WHEN** the user clicks "Walk"
- **THEN** the camera moves to eye height and keyboard/mouse control walking; Esc returns to orbit mode

#### Scenario: Touch device
- **WHEN** the page is opened on a phone
- **THEN** orbit mode works with touch gestures

### Requirement: Render from scene description
The system SHALL build all movable objects (furniture, plants, props) exclusively from `scene.json`.

#### Scenario: Unknown object type
- **WHEN** `scene.json` contains an object with an unknown `type`
- **THEN** a visible placeholder box is rendered and a warning is shown, and the rest of the scene still renders

# Delta: scene-description

## ADDED Requirements

### Requirement: Room base block
A scene file MAY contain `base: { "type": "room", "x": [min,max], "z": [min,max], "height": h, "walls": [{ "side": "north|east|south|west", "kind": "solid|window", "from": a, "to": b }] }`.

#### Scenario: Room size edit
- **WHEN** Claude changes `base.height` from 2.7 to 3.0
- **THEN** the ceiling and walls are drawn 3.0 m high

### Requirement: Office furniture types
The system SHALL provide `desk`, `desk-divider`, `monitor`, `office-chair` and `whiteboard` object types.

#### Scenario: Remove a desk
- **WHEN** Claude deletes one `desk` entry
- **THEN** that desk disappears and the rest of the room is unchanged

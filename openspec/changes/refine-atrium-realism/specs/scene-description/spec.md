# Delta: scene-description

## ADDED Requirements

### Requirement: Atrium detail types
The system SHALL provide `doorway-corridor` (size [width, height, depth]; opening faces local +z, corridor runs to local -z; glass-front panes it overlaps are hidden) and `notice-board` (size [width, height]; faces +z; optional `header` colour).

#### Scenario: Moving the doorway
- **WHEN** Claude changes the doorway's x position
- **THEN** the opening and corridor appear at the new position and the glass pane there is hidden

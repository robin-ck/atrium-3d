# Delta: scene-description

## ADDED Requirements

### Requirement: Declarative scene file
The system SHALL describe scene contents in `scene.json` as a list of objects with `id`, `type`, `position` [x,y,z] in metres, optional `rotation` (degrees around Y), `scale`, and `variant`.

#### Scenario: AI adds plants
- **WHEN** Claude adds five `plant-tree` entries to `scene.json` and the artifact is republished
- **THEN** five potted trees appear at the given positions, nothing else changes

### Requirement: Plant library
The system SHALL provide at least five plant types (`plant-tree`, `plant-shrub`, `plant-hanging`, `planter-box`, `green-wall`) with size variants.

#### Scenario: Green wall on a pillar
- **WHEN** a `green-wall` object is placed against a pillar with a given width and height
- **THEN** a vegetated panel of that size is rendered on that surface

### Requirement: AI editing guide
The system SHALL include `AI-EDITING.md` documenting the schema, coordinate system, a floor-plan map of named zones (e.g. "kitchen island", "stair void", "skylight"), and example prompts.

#### Scenario: Named zone prompt
- **WHEN** the user asks "add hanging plants along the mezzanine railing"
- **THEN** Claude can derive coordinates from the zone map without guessing

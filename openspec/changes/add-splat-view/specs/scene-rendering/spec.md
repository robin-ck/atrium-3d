# Delta: scene-rendering

## ADDED Requirements

### Requirement: Splat-style base
The system SHALL render a `base` of type `splats` as soft, coloured, camera-facing blobs whose on-screen size shrinks with distance, cut off above `clipHeight` in orbit mode.

#### Scenario: Opening the splat view
- **WHEN** the user opens the page with the splat `scene.json`
- **THEN** the scanned part of the atrium appears as soft coloured blobs and added objects render on top

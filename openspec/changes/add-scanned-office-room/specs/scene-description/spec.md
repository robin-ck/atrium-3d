# Delta: scene-description

## ADDED Requirements

### Requirement: Base block
A scene file MAY contain `base: { "type": "scan", "model": "<file>.glb", "scale": <number>, "offset": [x,y,z], "rotation": <deg> }`. Without it, the hand-built atrium shell is used.

#### Scenario: Correcting the scale
- **WHEN** Claude changes `base.scale` from 2.0 to 2.2
- **THEN** the scan is drawn 10% larger and objects keep their metre positions

# Project: Atrium 3D (NbS planning sketch)

## Purpose
Interactive, stylised 3D reconstruction of a university atrium (source: one 360° panorama photo), used as a base scene that can be modified with AI (e.g. adding plants / nature-based interventions).

## Stack
- Single-page web app: HTML + JavaScript, three.js (pinned version, loaded from cdnjs/jsdelivr).
- Scene content defined in a declarative JSON file (`scene.json`); the page renders whatever the JSON describes.
- Published as a private claude.ai Artifact; source files kept in this folder.

## Conventions
- Units: metres; Y is up; origin at floor centre of the atrium.
- AI edits happen by editing `scene.json` only, never the renderer code.
- No build step, no backend, no API keys.

## Constraints
- Must run in a modern desktop browser; usable on phone (orbit only).
- Stylised/low-poly look; no photogrammetry.

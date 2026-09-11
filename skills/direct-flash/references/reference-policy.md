# Reference Policy

## One locked master

The project has exactly one `MASTER_REFERENCE`.

Read its path and lock state from `../assets/references/manifest.yaml`.

Rules:

1. The master remains unchanged across edits.
2. New user uploads default to **edit target**, not reference.
3. Only explicit instructions such as “更换参考图”, “把这张设为新的基准图”, or “replace the master reference” authorize a master change.
4. A scene reference cannot become the master implicitly.
5. Do not average multiple references into a new pseudo-master unless the user explicitly asks to redefine the style system.

## Optional scene references

Scene references are narrow helpers. Use at most one per edit unless the user explicitly requests a multi-reference analysis.

They may refine:
- daylight outdoor flash behavior;
- ordinary indoor flash behavior;
- night-street falloff;
- dining/food reflections and tabletop behavior;
- strong reflective material behavior;
- close-subject flash emphasis.

## Current fixed mapping in this package

- `master_reference.jpg`
- `scene_daylight_outdoor.jpg`
- `scene_indoor_daily.jpg`
- `scene_night_street.jpg`
- `scene_dining_food.jpg`
- `scene_strong_reflective_surfaces.jpg`
- `scene_close_subject.jpg`

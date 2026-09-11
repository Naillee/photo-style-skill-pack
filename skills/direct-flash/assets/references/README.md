# Reference Assets

This repository contains the currently selected Direct Flash reference set.

## Fixed reference mapping

1. `master_reference.jpg` → overall Direct Flash master
2. `scene_daylight_outdoor.jpg` → daylight outdoor
3. `scene_indoor_daily.jpg` → ordinary indoor
4. `scene_night_street.jpg` → night street
5. `scene_dining_food.jpg` → dining / food
6. `scene_strong_reflective_surfaces.jpg` → strong reflective surfaces
7. `scene_close_subject.jpg` → close subject

## Reference priority

- `master_reference.jpg` is the only locked full-style anchor.
- Scene references are auxiliary and should be used one at a time when the target scene matches.
- New user uploads are edit targets by default and never replace the master unless explicitly requested.

## Image status

The seven files currently stored in this directory are the original user-uploaded reference images moved from the repository root into their final fixed paths. Keep these filenames unchanged so `manifest.yaml` continues to resolve them correctly.

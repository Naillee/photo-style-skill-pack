---
name: direct-flash
description: >
  High-preservation Direct Flash photo editing. Reconstruct a controlled near-camera
  frontal flash look with strong subject emphasis, plausible depth falloff, crisp
  specular response, restrained cool-neutral color, and selective ambient-cast cleanup.
  Uses one locked MASTER_REFERENCE plus six optional scene references. New uploads are
  edit targets by default and never replace the master unless the user explicitly asks.
---

# Direct Flash

## Dependency

This Skill uses the shared execution contract in sibling Skill `photo-edit-base`.

For every edit:

1. Read `../photo-edit-base/references/input-contract.md`.
2. Read `references/reference-policy.md`.
3. Read `references/style-definition.md`.
4. Read `references/scene-policy.md`.
5. Read `../photo-edit-base/references/prompt-compiler.md` before compiling the edit prompt.
6. Read `../photo-edit-base/references/quality-gate.md` before returning the result.

## Reference set in this package

- `master_reference.jpg` → overall Direct Flash master
- `scene_daylight_outdoor.jpg` → daylight outdoor
- `scene_indoor_daily.jpg` → indoor daily
- `scene_night_street.jpg` → night street
- `scene_dining_food.jpg` → dining / food
- `scene_strong_reflective_surfaces.jpg` → strong reflective surfaces
- `scene_close_subject.jpg` → close subject

## Default Direct Flash intent

Unless the user overrides it, aim for:

- near-camera frontal flash that is clearly visible on the main subject;
- subject brighter and more immediate than farther surroundings;
- crisp but controlled highlights and reflections;
- firmer local shadows than soft ambient light;
- plausible flash spill on nearby walls, tables, and objects;
- restrained, neutral-cool color rather than a heavy blue grade;
- cleaner skin color when ambient lighting contaminates it;
- reduced color clutter outside the main subject when useful;
- candid, raw, real-life photographic energy rather than polished beauty or cinematic grading.

## Intensity vocabulary

Use `low / medium / high` only as internal preference labels.

### Flash reconstruction
- **low:** refine existing flash-like qualities.
- **medium:** establish a clear frontal flash impression.
- **high:** strongly reconstruct frontal flash and suppress ambient dominance while preserving scene detail.

### Ambient-cast cleanup
- **low:** remove only obvious contamination from skin/highlights.
- **medium:** reduce ambient cast on the subject and quieter areas.
- **high:** substantially neutralize overwhelming contamination on the subject while keeping scene-defining color.

### Non-subject saturation suppression
- **low:** minimal change.
- **medium:** reduce distracting background color density.
- **high:** strongly simplify non-subject color clutter without making the whole image gray.

## Edit workflow

1. **Resolve target and reference roles.** New upload defaults to edit target. Load the locked master if available. Add at most one matched scene reference when it materially helps.
2. **Inspect the original target.** Record available dimensions, subject identity/structure, nearby surfaces, ambient-light dominance, color contamination, reflective materials, and scene depth.
3. **Choose only the needed style deltas.** Decide flash reconstruction, ambient-cast cleanup, and non-subject saturation suppression as low/medium/high.
4. **Choose a scene class.** Route through one of the six scene directions from `references/scene-policy.md`.
5. **Compile concrete pixel instructions.** Follow the shared prompt compiler and `references/style-definition.md`.
6. **Attach actual images.** The tool must receive the original target and required reference asset(s), not just text descriptions.
7. **Generate/edit.** Do not redesign subject or scene.
8. **Inspect the actual result.** Apply the shared quality gate plus the Direct Flash checks below.
9. **Retry once if needed.** Correct the dominant failure only, from the original target.

## Direct Flash checks

A successful result should show:

- visible near-camera frontal illumination on the intended subject;
- stronger luminance/readability separation between near subject and farther environment;
- crisp, localized highlight/reflection response instead of a global exposure lift;
- spatially plausible falloff;
- no blanket background blackout;
- no global blue filter masquerading as “cool”; 
- believable skin;
- restrained color density;
- no unnecessary crop, pose change, object change, or scene reconstruction.

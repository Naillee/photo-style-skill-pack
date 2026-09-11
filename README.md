# Photo Style Skill Pack

This pack separates a reusable photo-editing base from style-specific photo editing layers.

Current included styles:

- `direct-flash` - high-preservation near-camera frontal flash editing.

## Structure

```text
skills/
├── photo-edit-base/
│   ├── SKILL.md
│   └── references/
│       ├── input-contract.md
│       ├── prompt-compiler.md
│       └── quality-gate.md
└── direct-flash/
    ├── SKILL.md
    ├── references/
    │   ├── style-definition.md
    │   ├── reference-policy.md
    │   └── scene-policy.md
    ├── assets/
    │   └── references/
    │       ├── README.md
    │       ├── manifest.yaml
    │       ├── master_reference.jpg
    │       ├── scene_daylight_outdoor.jpg
    │       ├── scene_indoor_daily.jpg
    │       ├── scene_night_street.jpg
    │       ├── scene_dining_food.jpg
    │       ├── scene_strong_reflective_surfaces.jpg
    │       └── scene_close_subject.jpg
    └── evals/
        └── evals.json
```

## Reference set in this package

The reference images included in this package are fixed as follows:

1. `master_reference.jpg` → overall Direct Flash master
2. `scene_daylight_outdoor.jpg` → daylight outdoor
3. `scene_indoor_daily.jpg` → ordinary indoor / daily interior
4. `scene_night_street.jpg` → night street
5. `scene_dining_food.jpg` → dining / food
6. `scene_strong_reflective_surfaces.jpg` → strong reflective surfaces
7. `scene_close_subject.jpg` → close subject

## Design decisions

- `photo-edit-base` owns image roles, preservation, prompt compilation, actual-image attachment, inspection, retry limits, and dimension reporting.
- Style-specific skills own only their visual logic. The current `direct-flash` layer owns frontal flash behavior, subject/background separation, restrained cool-neutral color, ambient-cast cleanup, scene adaptations, and reference routing.
- There is exactly one locked `MASTER_REFERENCE`. New uploads are edit targets by default and never replace the master unless the user explicitly asks to change the master/reference.
- Scene references are optional helpers. They can refine a matched scene but never override the master.
- Preference levels are `low / medium / high`, defined by visible image changes rather than pseudo-precise numeric scores.
- Follow-up edits are deltas. The original target remains the identity/structure anchor to reduce serial generative drift.
- A generated result is inspected once; one targeted retry is allowed for a central failure. After that, return the better result and state the remaining limitation.

# Photo Edit Prompt Compiler

Compile the final edit prompt from **visible changes**, not abstract aesthetic labels.

## Required order

Every prompt must resolve these items in order:

1. **Image-role contract** — identify the edit target and each reference role.
2. **Preservation invariants** — what must remain recognizable.
3. **Lighting transformation** — concrete changes to subject light, falloff, highlights, shadows, and nearby surfaces.
4. **Color transformation** — concrete cast cleanup, saturation distribution, skin handling, and palette constraints.
5. **Permitted local changes** — only the objects/regions the user allowed to change.
6. **Hard avoids** — short, relevant failure constraints.

## Compilation rule

Translate diagnosis into pixel-visible instructions.

Bad:
- “make the direct flash stronger”
- “increase subject readability”
- “more documentary”

Better:
- “increase near-camera frontal illumination on the main subject; make skin, clothing folds, and reflective details respond more clearly to the flash; keep the far environment relatively darker; do not lift the entire frame equally.”

Bad:
- “darken the background”

Better:
- “reduce luminance mainly in surfaces and objects farther from the subject; keep a wall immediately behind or beside the subject plausibly illuminated by flash spill instead of forcing it black.”

## Compact prompt shape

Use 3–4 compact paragraphs:

1. **Target + invariants.** State what image is being edited and list the small set of identity/structure details that must not drift.
2. **Lighting.** State the visible lighting change, its spatial behavior, highlight/reflection response, and subject/environment separation.
3. **Color.** State what cast/saturation should change and what should stay stable, especially skin and intentionally colored lights.
4. **Avoids.** State only the relevant failure modes.

## Preservation language

Do not use promises such as:

- “100% unchanged”
- “pixel-perfect identity”
- “lossless face preservation”

Use operational wording instead:

- “preserve recognizable identity and facial geometry”
- “keep expression, pose, clothing pattern, and object count consistent with the original target”
- “do not redesign or re-pose the subject”

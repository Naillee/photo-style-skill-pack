---
name: photo-edit-base
description: >
  Shared execution contract for high-preservation photo style editing. Use as an
  internal dependency for style-specific skills. It defines image roles, source
  inspection, preservation invariants, actual image attachment, prompt compilation,
  result inspection, limited retry, and output-dimension reporting. Do not use it to
  invent a visual style by itself.
---

# Photo Edit Base

## Purpose

This is the shared execution layer for photo-style Skills. It does **not** define the final aesthetic. A style Skill must provide the desired visible lighting/color/texture behavior.

## Load order

For every image-editing job that uses this base:

1. Read `references/input-contract.md` before assigning image roles.
2. Read `references/prompt-compiler.md` before writing the generation/edit prompt.
3. Read `references/quality-gate.md` before returning an edited image.
4. Read the active style Skill's own files for style-specific behavior.

## Required workflow

1. **Resolve image roles.** Every available image must be one of: edit target, style reference, scene/supporting reference, or previous generated result.
2. **Inspect actual inputs.** Record available pixel dimensions, aspect ratio, visible main subject, identity-sensitive details, clothing patterns, object count, and scene geometry when relevant.
3. **Declare preservation invariants.** Use only visible or user-specified facts. Do not promise pixel-identical preservation from a generative editor.
4. **Attach the actual images to the edit call.** Do not rely on textual descriptions when the real target/reference is available.
5. **Compile visible editing instructions.** Convert diagnosis and style intent into concrete changes that could appear as pixels.
6. **Generate/edit.** Apply only permitted changes.
7. **Inspect the actual result.** Compare it with the original target, not only with the prompt.
8. **Retry at most once for a central failure.** Retry from the **original target**, with tighter instructions. Do not use a failed generated image as the sole identity source.
9. **Return the better result.** If the second result still has a meaningful limitation, state it briefly instead of claiming full success.

## Follow-up edits

Treat follow-up instructions as deltas unless the user clearly asks for a full restart.

- Keep the original target as the identity and structure anchor on every iteration.
- A previous result may be used only to indicate the current style state or desired delta.
- If the tool cannot include both original target and previous result, prefer the original target and restate the desired delta in text.
- Never let repeated generations progressively redefine the person's face, pose, clothing pattern, object count, or scene layout.

## Tool attachment contract

Use the runtime's supported image-input mechanism so the edit tool receives the actual images.

When local-path attachment is supported:

- pass the edit target first;
- pass the locked master/style reference second when required;
- pass one matched scene/supporting reference after that when needed;
- include the previous result only when it is necessary to communicate a follow-up style delta.

If the runtime exposes a field such as `referenced_image_paths`, use it with the actual paths. If it exposes a different image-input channel, use the equivalent. Never claim that an image was supplied to the model if it was only described in text.

## Preservation levels

### High — default for identifiable people, pets, products, and recognizable scenes

Preserve, when visible and relevant:

- identity and facial structure;
- expression;
- hairstyle and defining markings;
- body proportions and pose;
- clothing shape, pattern, and major color relationships;
- accessories;
- object count and object geometry;
- camera angle, framing, and scene layout.

High preservation does **not** mean lossless pixels. It means the edit should avoid material visual drift in these features.

### Medium

Preserve the recognizable subject and major scene structure, while allowing broader crop, palette, local lighting, surface, or surrounding-context changes explicitly permitted by the user.

### Reference-only

Learn requested visual behavior from the image without preserving its subject identity, wording, or exact composition.

## Output metadata

Internally record when available:

```yaml
input_size: WIDTHxHEIGHT
output_size: WIDTHxHEIGHT
preservation: high|medium|reference-only
retry_count: 0|1
remaining_limitation: none|short description
```

If the output pixel dimensions differ from the input, do not describe the result as pixel-level lossless.

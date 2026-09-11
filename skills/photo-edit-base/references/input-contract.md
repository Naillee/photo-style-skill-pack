# Input Contract

## Role assignment

Assign a role to every image before editing.

### Edit target

The photograph whose content must remain recognizable in the final result.

Default rule: **a newly uploaded image is an edit target unless the user's wording explicitly makes it a reference or supporting source.**

### Style reference

An image used to learn lighting, color, texture, or mood. The user must explicitly identify it as a reference, baseline, master, style example, or equivalent.

### Scene/supporting reference

An optional image used for a narrow scene-specific behavior. It cannot silently replace a locked master reference.

### Previous generated result

May be used to communicate the current edit state during a follow-up. It is never the sole source of identity or scene structure when the original target remains available.

## Ambiguity rule

Prefer the interpretation that preserves user content and does not mutate reference state.

- New upload + no explicit “reference” language → edit target.
- New upload does **not** change a locked master.
- Only explicit language such as “更换参考图 / 把这张设为基准 / replace the master reference” authorizes a master change.

## Source inspection

Before editing, inspect each edit target and record only visible facts needed for preservation:

- pixel dimensions and aspect ratio when accessible;
- number of identifiable people/animals/products;
- face, expression, pose, body proportions;
- hairstyle, accessories, clothing pattern;
- object count and prominent geometry;
- nearby walls/surfaces and their distance relationship to the subject;
- reflective materials;
- strong ambient color casts;
- readable text or branding that should remain.

Do not infer hidden details.

## Original-target anchor

For every follow-up generation:

1. re-include the original target whenever the tool supports it;
2. preserve the original target's identity and structure;
3. apply the user's newest request as a delta;
4. do not recursively re-edit only the last generated image when that could compound drift.

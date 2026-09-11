# Photo Edit Quality Gate

Inspect the **actual generated image** before returning it.

## Gate 1 — Input contract

- The edit target was actually included in the edit call.
- Required style/master reference was actually included when the task depends on it.
- Optional scene reference was included only when it matched the scene and was available.
- No new upload silently replaced a locked master.

## Gate 2 — Preservation

Compare against the **original target**:

- recognizable identity and facial geometry remain stable;
- expression is not materially changed unless requested;
- pose and body proportions remain stable;
- hairstyle, clothing shape/pattern, accessories, and defining markings remain stable when relevant;
- object count, prominent geometry, framing, and scene layout have not drifted materially;
- readable text/branding that should remain has not been rewritten or hallucinated.

Do not claim exact or lossless preservation merely because the prompt requested it.

## Gate 3 — Requested edit is visible

The requested change must be visibly present. For lighting edits, inspect subject illumination, local highlights, reflections, shadow behavior, and subject/environment separation. For color edits, inspect the intended regions rather than relying only on global color impression.

## Gate 4 — Spatial plausibility

- Light falloff follows scene depth reasonably.
- A wall or surface close to the subject may also brighten from flash spill.
- Distant background can recede more than near background.
- Do not mechanically darken every non-subject pixel.
- Reflective materials may brighten more strongly than matte surfaces.

## Retry policy

A central failure is one of:

- identity/structure drift;
- requested edit is too weak or absent;
- major color failure;
- implausible light geometry;
- missing or hallucinated objects/text.

If a central failure occurs:

1. revise only the dominant failure variable;
2. regenerate **once** from the original target with tighter invariants;
3. do not stack the second attempt on top of the first failed output as the sole source.

After one retry, stop. Return the better result and state any remaining limitation briefly. Never describe a failed preservation check as successful.

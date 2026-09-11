# Scene Policy

Scene routing changes **how** Direct Flash is applied, not what the master style is.

Choose a scene class from the actual target image. Do not rely only on filenames or user labels.

## daylight_outdoor
- keep the scene recognizably daylight;
- add clear near-camera flash on the subject without turning sky/buildings unnaturally dark;
- use modest subject/environment separation;
- keep color restrained but not washed out.

## indoor_daily
- establish direct frontal flash on the near subject;
- allow walls/furniture close to the subject to brighten from spill;
- let deeper room areas recede more than near surfaces;
- avoid making the whole room black.

## night_street
- flash-lit subject may be much brighter than surroundings;
- preserve a small amount of real street lighting/signage when present;
- avoid cinematic night grading or artificial rim light;
- retain plausible dark detail instead of crushing all background to black.

## dining_food
- let plates, cutlery, glasses, sauces, oils, wet surfaces, and glossy food show controlled flash reflections;
- make the table/near food clearly readable;
- allow the farther dining environment to recede;
- avoid blowing white plates or metallic reflections into large detail-less patches.

## strong_reflective_surfaces
- make flash reflections and specular hotspots more obvious and intentional;
- preserve the difference between glass, metal, water, polished paint, and other materials;
- keep highlights concentrated rather than milky or smeared;
- avoid large clipped white patches that erase texture or form.

## close_subject
- preserve facial geometry or subject shape above stylistic strength;
- make the near subject feel distinctly flash-lit and immediate;
- increase local texture and highlight clarity without redesigning the subject;
- if the background is physically close, allow it to receive plausible spill.

# Materials, reference description, and code twin

Read this alongside the reconstruction contract before analyzing a reference. The material workflow applies to every reconstruction. Save the handoff by default in the current workspace; create the code twin when requested. Do not add documentation frames to Figma.

## Evidence before parameters

A screenshot determines appearance, not a unique source construction. Separate observed facts, inferred implementation, and unavailable information. Do not assign numerical confidence without a measurement model. Use high / medium / low confidence with a short evidence statement. Similar foreground and background hues alone establish neither transparency nor opacity.

Inspect the whole screen and matched crops at native size and enlarged scale. Calibrate screenshot pixels to source-frame pixels before estimating effect widths. Enlarging a crop does not recover missing detail. If editable original layers are available, inspect their actual paints/effects first and distinguish those values from estimates derived from pixels.

For each visually important surface, record an ordered material recipe:

- underlying background and relevant content behind the surface;
- base fills, gradient types, stops with alpha, centers, handles, axes and coordinate units;
- tint, fill alpha, blend mode, and separate node opacity;
- background blur versus layer blur, target layer and estimated radius;
- border alignment, width, color/alpha, edge highlights and inner shadows;
- outer shadows or glow with offset, radius, spread, color/alpha;
- mask, clipping bounds, corner geometry, and front-to-back relationships.

Include only supported contributions. A glass label is not a recipe. Test glass against an opaque gradient alternative: does recognizable content continue behind it, lose contrast or sharpness inside it, and change with the underlying background? Preserve sharp foreground labels. A bright rim can be a stroke, highlight, or inner effect; inspect its direction and falloff rather than adding all three.

For gradients, locate color maxima and transition geometry across the whole surface before tuning stops. Distinct blooms may require several radial layers. For shadows, compare the contour and falloff on multiple edges, separate contact shadow from broad ambient shadow only when both are visible. A screenshot cannot reliably prove refraction, noise, or hidden backgrounds; mark these unknown instead of inventing them.

## Candidate and render loop

For an ambiguous, prominent material, compare two plausible recipes on the same reconstructed background. Start with background and geometry, then fills, translucency and blur, then borders/highlights and shadows. Change one parameter family per comparison. Prefer the simplest recipe that explains the visible evidence; retain the rejected alternative and reason in the handoff when uncertainty matters.

Inspect equal-size source/output crops and the whole screen. Check color-field topology, edge sharpness, background visibility, shadow falloff, clipping and foreground contrast separately. Use overlays or difference images when available, but exclude intentional system-UI omissions and substituted media from fidelity claims. Never interpret a single whole-screen similarity score as proof of correct effects.

Treat a visually dominant material as an early acceptance criterion, alongside layout and typography. Do not defer it to final polish. After three correction passes without meaningful improvement, record the remaining mismatch and likely limitation rather than looping indefinitely or declaring a match.

## Shared reference package

Save each reference under `reference-packs/<stable-reference-id>/`, preserving previous versions and unrelated files. Use `reference.md` for a concise human-readable handoff and `reference.json` for the same model in structured form. Include an original image/export when accessible and authorized; otherwise keep the source link and mark the image unavailable. Never fabricate an export path.

Use these top-level JSON keys (schema version `1.0`):

| Key | Content |
| --- | --- |
| schemaVersion | `1.0` |
| original | Source URL/file/node IDs, accessible image path, viewport, image-to-frame transform and crop |
| structure | Stable element IDs, parent IDs, type, bounds in source-frame px, z-order, layout and clipping |
| designTokens | Colors, typography, spacing, radii, material recipes and their IDs; scope limited to this reference |
| components | Instances, element IDs, token/material references, visible variants |
| composition | Alignment, spacing relationships, hierarchy, overlap and anchoring rules |
| behavior | Observed states/interactions with evidence; unknown for motion or gestures unavailable in a static image |
| semanticTags | Interface type, style, mood and searchable material tags, labeled as interpretation |
| rebuild | Figma file/node IDs, optional code paths, asset substitutions with donor page/node ID, Fill index, image hash and output-node mapping (or bundled asset path and fallback reason), and renderer-specific approximations |
| quality | Verification status per target, compared crops, discrepancies, confidence/evidence and unresolved alternatives |

For inferred properties use `{ "value": ..., "status": "inferred", "confidence": "medium", "evidence": "..." }`; use `observed` for directly established facts and `unknown` with a null value for unavailable information. Store editable-source values as observed with their source node. An inferred estimate remains inferred even after its rendered appearance has been verified.

Record units, coordinate origins and paint-stack ordering explicitly. Preserve stable element/material IDs across Figma and code. The Markdown summary should explain distinctive composition and materials, reconstruction decisions, missing evidence and what the next agent should verify; it must link to the JSON and accessible original. Validate JSON syntax and that all parent/token/material references resolve before reporting the package complete.

## Optional code twin

When the user requests code as well as Figma, build both from the shared model. Use the existing project's stack; in an otherwise empty workspace use a self-contained HTML/CSS preview with local assets and SVG icons. Do not require an app framework for a static reference. Generate the code after the current reference's material model is established and reconcile corrections back into that model.

Use semantic DOM, editable text and CSS layout. Keep decorations in separate elements or pseudo-elements when they need independent opacity, blur or stacking. Map background blur to a backdrop effect, layer blur to a foreground filter, and shadow layers to independently tunable shadows. Translate coordinate systems and paint ordering explicitly; do not copy renderer-specific gradient transforms or blur values assuming visual equivalence. Preserve the intended background behind translucent surfaces.

Inspect currently available Figma capabilities and browser behavior when implementing; do not invent unsupported API properties or claim that CSS and Figma support identical materials. Record approximations for corner smoothing, gradient types, blending, clipping or effects that cannot be reproduced exactly. Never flatten the reference screenshot into the code twin.

Render the browser output at the original viewport and compare it independently against the original reference, not just the Figma reconstruction. Label it unverified if browser rendering is unavailable. Static references do not establish responsive layouts, animations or interactions: retain a fixed reference viewport unless the user requests those additions. Do not deploy or publish solely to provide a code twin.

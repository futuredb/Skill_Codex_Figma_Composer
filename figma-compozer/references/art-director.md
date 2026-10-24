# Art director quality review

Act as a Senior Digital Art Director and Visual Designer reviewing the actual reconstruction. Your responsibility is visual fidelity, coherent composition, precise materials and editable execution. This role is adapted from the user's Art Director brief for reconstruction, not for generating a new visual concept.

## Scope and independence

The original reference and explicit user constraints are the authority. Preserve its distinctive composition and visual language. Do not generate three creative directions, remix references, introduce decorative glass or normalize independent screens. Originality means preserving the reference's character, not making the reconstruction more original. Report UX weaknesses inherited from the reference separately; do not redesign them without a user request.

Use a separate reviewer subagent when available, with read-only review responsibility. The composer owns all mutations. If delegation is unavailable, run an explicit separate review pass and label it self-review; do not claim independent review. Do not create a new user-facing chat for this role.

Give the reviewer the original reference, current actual render, viewport/crop mapping, user constraints, relevant reconstruction rules, reference model and target node IDs or code paths. Include declared omissions and asset substitutions. Provide accessible image files or tool access so the reviewer can inspect pixels; descriptions of images are insufficient. Keep the first review independent of the composer's own quality verdict.

## Before construction

Record a compact ArtDirectionSpec in the reference package:

- reference ID and faithful reconstruction direction;
- three to five defining visual principles, with source regions as evidence;
- composition: focal point, hierarchy, major proportions, alignment, density and whitespace rhythm;
- typography: role contrast, typeface character, wrapping and baseline rhythm;
- color and materials: dominant fields, depth, gradients, glass, blur, borders and shadows;
- imagery and component roles, provenance IDs when known, substitutions and constraints;
- per-screen instructions and concrete acceptance criteria;
- risks, assumptions and unknowns, including motion/interaction unavailable in a static reference.

Keep this concise and reuse the existing reference model rather than duplicating all tokens. Do not invent a Product Brief or Design DNA Library when none is supplied. Check consistency only within the same reference or an explicitly established shared product system.

## Review checkpoints

1. After the major layout and dominant materials are visible, inspect composition, proportions and visual focus. Treat unfinished details as pending, not defects.
2. After the complete screen is rendered, review all dimensions below before moving to the next reference.
3. After each correction cycle, inspect a fresh render of the changed output and check for regressions. If a code twin exists, review its browser render independently against the original; a Figma pass does not approve the code twin.

Review the full screen at the reference viewport plus aligned crops for typography and important materials. Inspect:

- composition, hierarchy, scale relationships, density, whitespace and alignment;
- font character, optical weight, line breaks, text bounds and spacing;
- component geometry, corners, clipping, overlap and image-container treatment;
- gradient topology and layering, tint and alpha, background versus layer blur, crisp foreground content, highlight direction and shadow falloff;
- preservation of the reference's distinctive visual choices;
- introduced UX/readability defects and technical defects;
- editable structure through node/code inspection, separately from visual evidence.

Honor intentional status-bar omissions, keyboard replacement and permitted media substitutions from the supplied Figma file or fallback bundled assets. Record their impact on fidelity; do not demand reversal of those rules or claim that substituted imagery matches the source. Review the geometry and treatment of substituted media. Do not infer motion, responsive behavior or gestures from static screenshots.

## Actionable feedback and correction loop

Return the three highest-impact actionable findings per pass; retain other known issues in the backlog. Each finding includes:

- stable issue ID, target and region/node/element ID;
- severity: blocker, major or minor;
- observed source/output difference with screenshot/crop evidence;
- why it changes the composition, hierarchy, material or legibility;
- a specific correction and observable acceptance criterion;
- confidence and any uncertainty in the inferred parameters.

Example: “The glass card obscures the background transition visible in the source. Keep its text opaque; adjust surface tint/alpha and background blur separately until the transition remains visible while underlying detail is softened. Recheck the left-edge crop.” Give pixel values only when measurable in calibrated source-frame units. Avoid commands such as “make premium” or unjustified exact blur values.

Correct composition and hierarchy first, then typography and components. A dominant material that defines the reference is also a high-priority issue, not optional decoration. The composer applies supported corrections, records any rejected finding with its reason, renders again, and returns the new evidence to the reviewer. Do not close an issue based only on a claimed code/property change.

Allow at most three art-director correction cycles per reference by default. Existing material-tuning passes contribute to this shared budget when they address the same reviewed issue; do not nest unlimited three-pass loops. Stop earlier if the criteria pass or progress is blocked by missing evidence/capabilities. At the limit, preserve remaining issues and report the actual status. The next reference may proceed after this documented bounded review; do not present the unresolved screen as approved.

## Verdict and saved output

Use these verdicts per target:

- `pass`: current render inspected, acceptance criteria met, no known actionable visual defects remain;
- `pass_with_notes`: current render inspected, no blocker/major issues remain, minor issues or declared approximations are recorded;
- `needs_revision`: blocker or major issues remain, including when the correction budget is exhausted;
- `unverified`: original or actual output pixels cannot be inspected; structural inspection alone cannot establish a visual pass.

Save `art-direction.md` and `art-review.md` beside `reference.md`. Record reviewer mode, target, revision or capture identity, evidence paths/node references, criteria, findings, correction history, remaining issues and verdict. Add `quality.artDirector` to `reference.json` with report paths and per-target verdicts, iteration counts and open issue IDs. Keep the existing schema fields intact. Verify saved links and IDs. Do not create annotation/showcase frames in Figma.

The completion report includes the art-director verdict and material unresolved issues. Say when review was self-review or unverified. Never invent screenshots, visual inspection, numerical fidelity scores or reviewer approval.

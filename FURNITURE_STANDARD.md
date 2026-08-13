# Furniture 3D Presentation Standard

This is a reusable standard for interactive furniture presentations. It is not a cutting list, a manufacturing drawing, or a parameter source for the illustrative cabinet in this repository.

## 1. Source of truth and measurements

- Use millimetres for every dimension, label, calculation, and review note.
- Start every new model with a compact project data block: external envelope, board/facade/rear-panel thicknesses, plinth or support height, openings, doors, and approved marker offsets.
- Derive all boards, openings, facades, labels, and dimensions from that data. Do not use unrelated hand-tuned geometry.
- Verify each axis end-to-end: all clear openings, boards, gaps, plinth/support, and outer panels must equal the declared external width, height, and depth.
- Record actual materials, edge-banding allowance, maximum sheet sizes, hardware clearances, and load requirements for the project. Never silently reuse them from another cabinet.

## 2. Structural representation

- A free-standing cabinet requires planar stability. Show a rear panel and required wall anchors unless a qualified craftsperson specifies another structural solution.
- Divide rear panels on structural partitions, never through the centre of a clear opening. Rear panels should visibly overlap supporting outer boards instead of appearing to float.
- When hardboard is used as the rear panel, choose the panel division from the structural section boundaries and the available sheet size. A seam belongs between sections, not behind a shelf or in the middle of a usable compartment.
- In the rear view, show each hardboard sheet as one restrained rectangular outline with a subtle diagonal cross inside. The outline identifies one sheet; the cross identifies its plane. Use a clear grey tone that is distinct from cabinet geometry.
- Show internal boards behind a rear sheet as broad dashed guides with the board's nominal thickness, placed in a separate non-overlapping plane. The guides must be visually subordinate to the hardboard sheet outline and must not protrude as if they were rear-mounted boards.
- A standing cabinet needs a plinth or an explicitly designed support system. Structural inter-section partitions continue to the floor; only the front plinth face may be split into separate pieces.
- Model every load path. A support above a niche must continue to a structural board, floor support, wall fixing, or specified metal reinforcement.
- Show wall-fixing points where required. They are safety information, not decoration.

## 3. Doors, mirrors, and hinges

- Every door covers the boards it is intended to cover and leaves only agreed facade gaps.
- Confirm all perimeter and meeting gaps with the selected hardware. Mirrored doors need safe clearance so they cannot touch neighbouring leaves after adjustment.
- A hinge consists of a cup on the inside of the facade and a mounting plate on the inside of the cabinet wall. No hinge hardware is visible from outside.
- Place hinge centres in clear opening space, never on a shelf, a partition edge, or another collision surface. Keep top and bottom hinge placement symmetric when practical.
- Labels and dimensions remain attached to a moving door. A mirror effect belongs only on the exterior face; the interior and edges remain normal board material.

## 4. Openings and annotations

- Give every internal rectangular opening one unique letter and use it consistently.
- A dimension annotation belongs to one owner opening. Vertical annotations are constrained to that opening's left/right edges; horizontal annotations are constrained to its bottom/top edges. They never enter a neighbouring opening.
- Every opening uses the same local snap fractions on its relevant axis: **0%, 25%, 33 1/3%, 50%, 66 2/3%, 75%, and 100%**. Calculate them from that opening's real bounds, never from the full cabinet or a screen offset.
- A marker may snap to a neighbouring marker only if the target coordinate already lies inside the owner opening. It never expands the owner's bounds.
- During review, marker controls may be visible. On approval, save the complete current marker map exactly as placed, hide the editing UI, and publish the saved map unchanged. Different openings may intentionally use different final fractions.
- Exterior dimensions use compact cards anchored to the actual outer surface. Internal lines and labels must depth-test and be occluded by solid boards and closed doors.

## 5. Visual and interaction rules

- Boards meet edge-to-edge without intersecting. Avoid coplanar or overlapping geometry: it causes visual flicker.
- Rear panel divisions are explanatory only. Use subdued bounded rectangles and dashed guides; they must not look like protruding boards or required cuts through openings. Each dashed segment pattern starts and ends with a visible dash, for both horizontal and vertical guides.
- Keep the scene lightweight: simple procedural geometry, compact canvas labels, static mirror highlights, and no continuous costly reflection pass.
- Support touch and mouse orbit controls, useful front/isometric views, and PNG export. Validate the result on desktop and a modest phone.
- If Russian and Azerbaijani are supplied, make language state shareable in the URL and translate every visible label consistently.

## 6. Review and publication checklist

1. Recalculate widths, heights, depths, material thicknesses, facade gaps, rear panels, and plinth/support elements.
2. Inspect open and closed doors for collisions, visible hinges, unintended overlap, and exposed board strips.
3. Inspect the rear view for load paths, rear-panel seams, and geometry flicker.
4. Save the full approved annotation layout and remove or hide the editing controls.
5. Export screenshots in their agreed order. Set the requested image in both `og:image` and `twitter:image`.
6. Verify the published page, desktop/mobile behaviour, language links, screenshots, and social preview before handoff.

## Scope boundary

The model communicates an agreed concept. Cutting lists, load calculations, joinery, edge-banding deductions, hardware selection, wall anchors, and installation must be verified by the responsible designer and craftsperson.

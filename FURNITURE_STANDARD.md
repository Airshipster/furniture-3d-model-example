# FURNITURE_3D_STANDARD v1

## 0. Agent contract

```text
ROLE: Codex builds an interactive furniture presentation model.
UNIT: mm.
SCOPE: visual communication and review only; never treat the model as a manufacturing drawing.
INPUT: project-specific data supplied by the user.
OUTPUT: a lightweight interactive model, approved screenshots, and share metadata.
RULE PRECEDENCE: user project brief > this standard > existing illustrative scene.
FORBIDDEN: infer dimensions, material properties, load capacity, sheet size, hardware clearances, or wall-fixing requirements when they are not supplied.
```

## 1. Required project input

Before changing geometry, obtain or explicitly mark as pending:

```yaml
envelope_mm: { width, height, carcass_depth, overall_depth }
materials: { carcass_thickness, facade_thickness, rear_panel_thickness, edge_banding_allowance }
support: { mode: freestanding|built_in, plinth_or_support_height, wall_anchor_requirement }
sections: [{ id, bounds_mm, openings: [{ id, bounds_mm, intended_use, load_if_known }] }]
doors: [{ id, owner_openings, bounds_mm, hinge_side, hinge_count, gaps_mm, mirror_exterior }]
rear_panels: { material, available_sheet_bounds_mm, panel_boundaries }
presentation: { languages, screenshot_order, social_preview_image, published_url }
```

Do not copy these values from a previous furniture model. Store each new model's input in a project-specific data block in the implementation, not in this standard.

## 2. Coordinate and accounting invariants

```text
ALL_DIMENSIONS_USE_MM = true
ALL_GEOMETRY_IS_DERIVED_FROM_PROJECT_DATA = true
NO_UNEXPLAINED_MAGIC_COORDINATES = true

sum(clear_openings + board_thicknesses + declared_gaps + plinth/support + outer_panels)
  == declared_outer_axis_length
for axis in {width, height, depth}
```

- Recalculate all three axes after every structural change.
- Material thickness, edge-banding deduction, maximum sheet size, hardware clearance, and facade gap are project inputs, not global constants.
- Flag any missing value that changes a fabrication, safety, collision, or sheet-layout decision.

## 3. Structure and safety

```text
IF support.mode == freestanding:
  REQUIRE rear_panel_for_planar_stability
  REQUIRE explicit_wall_anchor_status

IF a vertical support receives load from above:
  REQUIRE continuous_load_path_to(structural_board OR floor_support OR wall_anchor OR specified_metal_reinforcement)

IF a structural inter-section partition is a floor support:
  REQUIRE partition.extends_to_floor == true
```

- Do not leave an unsupported vertical load on the middle of a shelf or niche top.
- Keep a usable niche clear unless the brief explicitly accepts a support/reinforcement inside it.
- A standing cabinet requires a plinth or an explicitly designed support system.
- Divide only the **front plinth face** when required by material length or access; do not split structural inter-section partitions because of that division.
- Render required wall-fixing points as safety information.

## 4. Rear hardboard / rear-panel contract

```text
rear_panel_seam.position MUST coincide_with structural_section_boundary
rear_panel_seam.position MUST NOT pass_through clear_opening
rear_panel.geometry MUST overlap supporting_outer_boards
rear_guides.z MUST NOT intersect rear_panel.z
rear_guides.style = broad_dash(nominal_board_thickness)
```

- Choose rear-panel sheet boundaries from structural section boundaries and available sheet dimensions.
- In rear view, render each sheet as one subtle rectangular outline with a diagonal cross inside it.
- The rectangle identifies one sheet. The cross identifies the sheet plane. Neither is a physical board.
- Render internal boards behind a rear sheet as visually subordinate broad dashed guides in a separate, non-overlapping plane.
- Dashed guides must start **and** end with a visible dash on both horizontal and vertical lines.
- Rear sheet outlines, crosses, and guides must not resemble protruding boards or mandatory cuts through clear openings.

## 5. Geometry anti-flicker invariant

```text
FOR EVERY pair of visible surfaces:
  INTERSECTION_VOLUME == 0
  COPLANAR_OVERLAP == 0

edge_to_edge_contact IS ALLOWED
surface_penetration IS FORBIDDEN
```

- Boards meet edge-to-edge; they do not penetrate each other.
- Rear panels, rear guides, labels, facade overlays, mirrors, and dimensions must use separated planes when overlap would otherwise be coplanar.
- Treat flicker as a geometry error. Find and remove the intersection; do not conceal it with rendering options.

## 6. Door and hinge contract

```text
door.coverage == agreed_board_coverage
door.perimeter_gap == project.door.gaps_mm
door.meeting_gap >= agreed_safe_clearance

hinge.cup.location == door.interior
hinge.mounting_plate.location == cabinet_wall.interior
hinge.visible_from_exterior == false
hinge.center MUST be inside clear_opening_space
hinge.center MUST NOT be on shelf OR partition_edge OR collision_surface
```

- Model closed and open door states; inspect both before publication.
- Keep top and bottom hinge distances symmetric where practical.
- Door dimensions and labels move with the facade.
- Mirroring exists only on a mirror door's exterior face. Its interior and edges use ordinary board material.
- Do not leave a board strip exposed where the agreed facade must cover it.

## 7. Opening IDs and annotations

```text
opening.id: unique_letter
annotation.owner_opening: required

vertical_annotation.range = [owner.left, owner.right]
horizontal_annotation.range = [owner.bottom, owner.top]
allowed_snap_fractions = [0, 0.25, 1/3, 0.5, 2/3, 0.75, 1]
```

```text
ANNOTATION MUST NOT leave owner_opening.bounds
ANNOTATION MUST NOT use cabinet-global bounds for local snapping
NEIGHBOUR_MARKER may_be_snap_target ONLY IF neighbour.coordinate IN owner_opening.bounds
NEIGHBOUR_MARKER MUST NOT expand owner_opening.bounds
```

- Create local snap coordinates from real owner-opening bounds on every relevant axis.
- Do not implement section-specific snap exceptions. Fix any snapping problem in the generic owner-bound calculation.
- Keep annotation placement editable only during review.
- When approved, save the entire marker map in one operation. Preserve exact per-marker values; do not round, normalise, reconstruct from generic fractions, or copy a stale partial map.
- Hide or remove annotation editing controls in the published model.
- Exterior dimensions use compact cards anchored to their actual exterior plane. Internal annotations and cards must depth-test and be occluded by closed doors and boards.

## 8. Presentation runtime requirements

```text
renderer: lightweight
labels: compact_canvas_textures
mirrors: static_exterior_highlight
continuous_expensive_reflection: forbidden
controls: mouse_orbit + touch_orbit
views: front + isometric + PNG_export
```

- Validate desktop and modest-phone performance.
- Do not use a floor/grid that obstructs underside inspection unless the project brief requires it.
- If Russian and Azerbaijani are supplied, translate all visible labels. Persist language in a shareable URL state.

## 9. Publication acceptance checks

```text
CHECK axis_accounting == PASS
CHECK free_standing_stability_and_anchor_status == PASS_or_explicitly_pending
CHECK load_paths == PASS
CHECK rear_panel_seams_and_visual_guides == PASS
CHECK no_visible_geometry_flicker == PASS
CHECK closed_and_open_doors == PASS
CHECK no_exterior_hinges == PASS
CHECK annotation_bounds_and_saved_marker_map == PASS
CHECK desktop_and_mobile == PASS
CHECK screenshots_in_agreed_order == PASS
CHECK og:image == requested_social_preview_image
CHECK twitter:image == requested_social_preview_image
CHECK published_page == PASS
```

## 10. Scope boundary

The model communicates an agreed concept. Cutting lists, load calculations, joinery, edge-banding deductions, hardware selection, wall anchors, and installation remain subject to verification by the responsible designer and craftsperson.

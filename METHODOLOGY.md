# Methodology for interactive furniture models

This repository is a reusable example of a **presentation model**, not a furniture planner or a manufacturing drawing package. Its job is to let a customer or craftsman inspect one agreed configuration clearly on desktop and mobile.

## Core principles

1. **One visible model, one source of truth.** Dimensions, sections, doors, labels, materials, and interactions must describe the same physical cabinet.
2. **Measurements use centimetres.** The cabinet depth is communicated as a construction formula: carcass depth + facade thickness = overall depth.
3. **Every internal rectangular opening has one letter.** Letters are unique, contain no numbers, and remain readable from the intended viewing side. They make conversation about an opening unambiguous.
4. **Annotations behave like physical objects.** Internal dimension lines sit inside their own opening; surface cards sit directly on the corresponding exterior plane; door cards are attached to the exterior face of the door. Labels must be occluded by solid boards and doors rather than drawn through them.
5. **Doors explain construction.** A door opens around its actual hinge side by 90 degrees. Hinges are shown only on the interior side. Door labels stay attached when a leaf opens. Mirrored leaves are mirrored only on the external face; their interior and edges remain ordinary panel material.
6. **The model must stay lightweight.** Use simple procedural geometry, compact canvas labels, one static environment reflection for mirrored faces, and no continuous expensive reflection pass. It must remain usable on a modest phone.
7. **Mobile is a first-class view.** Start in isometric view, keep controls visible, keep the information panel compact, and explain two-finger navigation when it is needed.
8. **Language is shareable through the URL.** Russian is the default. `?az` opens Azerbaijani. Switching language updates the URL without rebuilding the model state.

## Implementation pattern

- Keep the scene in a single static `index.html` unless the model grows enough to justify modules.
- Define overall dimensions and panel thickness first, then derive every section, shelf, door, and label position from those values.
- Build carcass panels and internal boards with solid geometry before adding labels. Keep label materials depth-tested so hidden labels do not leak through furniture.
- Use a compact canvas texture for each label. Draw the card in its own local plane rather than making it a camera-facing overlay.
- Keep interactive dimensions in a dedicated group. Permit movement only perpendicular to the line: vertical dimensions move left/right; horizontal dimensions move up/down. Freeze final offsets in `fixedDimensionOffsets` once the layout is approved.
- Use an explicit state model for language, door visibility, and door-open state. Hiding doors disables the open/close action.

## Reusing this method with Codex

Give Codex this repository and describe the new cabinet in terms of:

- outer width, height, carcass depth, facade thickness;
- section widths and shelf heights;
- each opening's desired letter and measured width/height;
- doors, hinge sides, hinge count, handles, and mirrored exterior faces;
- which exterior sides need dimension cards;
- Russian and Azerbaijani labels, if both are required.

Ask it to preserve the principles above, update `MODEL_SPEC.md`, and verify the model on desktop and mobile before publishing.

## Scope boundary

This model is for visual communication and review. It does not calculate cutting lists, hardware tolerances, load capacity, joinery, or manufacturing approvals. Those remain the responsibility of the designer and craftsman.

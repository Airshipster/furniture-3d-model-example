# Current model specification

## Overall construction

| Property | Value |
| --- | --- |
| Overall width | 297 cm |
| Overall height | 265 cm |
| Carcass depth | 53.2 cm |
| Facade / panel thickness | 1.8 cm |
| Overall depth | 55 cm |

All dimensions are in centimetres. The carcass, internal partitions, shelves, and facades use the same nominal 1.8 cm panel thickness.

## Sections and opening notation

The screen-left module is an 82 cm shelving section. Its openings are lettered **A–H** from top to bottom. The middle module contains the hanging section with **I**, **J**, and **K** from bottom to top. The screen-right module contains **L** below and the upper openings **M–O** on the left, **P–R** on the right.

The model creates rear cards for each opening: letter first, then the clear opening size. They are attached to the rear wall and are physically hidden when a solid panel blocks the view.

## Doors and fittings

- Two leaves in the screen-left module: 2 hinges per leaf, hinges on the screen-left side.
- Two central full-height leaves: 3 hinges per leaf, mirrored external face only, with ordinary panel material on their interior and edges.
- One upper and one lower leaf in the screen-right module: 3 hinges for the upper leaf and 2 hinges for the lower leaf.
- Doors are open by default at 90 degrees. The controls can close/open them or hide them completely.
- Every leaf has a two-line exterior label with its type and dimensions. Central leaves are labelled as mirrored doors.

## Dimensions and labels

- Orange lines and arrows are working dimensions. Internal lines are positioned 15 cm inside the cabinet.
- Exterior dimensions use compact two-line cards attached to the top, left, and right surfaces. They replace exterior orange dimension lines.
- All label text is rendered in Russian by default; `?az` switches the interface and labels to Azerbaijani.
- The language query is intentionally shareable: `/?az` is the Azerbaijani link and the URL without the query is Russian.

## Visual and performance rules

- Light neutral-grey carcass and doors; central exterior faces have a lightweight static mirror highlight.
- Rear seams use dark solid strips so every partition reads from the back consistently.
- There is no floor or grid, allowing inspection from below.
- The renderer is kept intentionally light for phones: simple geometries, canvas-based label cards, and static rather than continuous reflection.

## Interaction

- Orbit controls support mouse and touch navigation.
- The front and isometric buttons set repeatable review views.
- `Save PNG` captures the current view.
- The information panel starts open and can be closed; the GitHub button links back to this repository.

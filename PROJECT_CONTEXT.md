# PROJECT_CONTEXT: furniture-3d-model-example

## Status

```yaml
status: completed_reference_project
branch: main
repository: https://github.com/Airshipster/furniture-3d-model-example
published_model: https://airshipster.github.io/furniture-3d-model-example/
purpose: reusable interactive furniture-presentation reference
```

## Canonical reuse rule

For any future furniture model, read `FURNITURE_STANDARD.md` before changing geometry, labels, doors, rear panels, or interaction. Treat the scene in this repository as a visual example only. Do not copy its dimensions, section layout, marker positions, material assumptions, or hardware decisions into a new commission.

## Current repository conventions

```yaml
documentation:
  entrypoint: README.md
  agent_standard: FURNITURE_STANDARD.md
screenshots:
  ordered_files:
    - screenshots/model-view-1.png
    - screenshots/model-view-2.png
    - screenshots/model-view-3.png
  social_preview: screenshots/model-view-2.png
social_metadata:
  og_image: model-view-2.png
  twitter_image: model-view-2.png
runtime:
  hosting: GitHub Pages
  dependencies: Three.js CDN
  local_server_required_for_published_model: false
```

## Handoff

- Keep this project self-contained; do not duplicate its project-specific history into global Codex context.
- When publishing new screenshots with unchanged filenames, update README image URL query versions if GitHub's rendered README image cache remains stale.
- Before a future reuse, collect a new project brief and apply the `FURNITURE_STANDARD.md` contract end-to-end.

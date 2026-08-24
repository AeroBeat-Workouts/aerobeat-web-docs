# Web Repo Map

Use this map before opening a PR or assigning work. If a change crosses several domains, put shared shapes in `aerobeat-web-contracts` and keep implementation details in each owning repo.

## Current First-Wave Repos

| Repo | Purpose |
| --- | --- |
| `aerobeat-web-contracts` | Shared service IDs, event names, element names, and public data shapes. |
| `aerobeat-web-vendor-movenet` | TensorFlow.js/MoveNet isolation behind an AeroBeat adapter boundary. |
| `aerobeat-web-cv` | Camera lifecycle, frame sources, pose-frame production, and vendor CV orchestration. |
| `aerobeat-web-input` | Device-independent routing from pose/body data into gameplay-facing input events. |
| `aerobeat-web-style` | Design tokens, CSS variables, base styles, and theme primitives. |
| `aerobeat-web-ui` | Native `aero-*` Web Components, calibration screens, HUD, menus, and testbed UI. |

## Future Or Adjacent Repos

| Repo | Purpose |
| --- | --- |
| `aerobeat-web-assembly` | Deployable app shell, service wiring, integration flows, and release artifacts. |
| `aerobeat-web-audio` | Web Audio clock, song playback, timeline sync, and beat/time conversion. |
| `aerobeat-web-renderer` | WebGL2 gameplay renderer, target visuals, effects, and debug overlays. |
| `aerobeat-web-gameplay` | Mode rules, hit windows, scoring, and Boxing/Flow gameplay logic. |
| `aerobeat-web-content` | Canonical map/event fixtures, converted content, and content loading boundaries. |
| `aerobeat-web-performance` | Frame budgets, diagnostics, quality levels, and adaptive performance policy. |
| `aerobeat-web-assets` | Product-owned static assets and asset manifests. |
| `aerobeat-web-config` | Environment profiles, feature flags, and runtime/build configuration. |
| `aerobeat-web-tools` | Generators, validators, conversion helpers, and repo tooling. |
| `aerobeat-web-docs` | Public-facing web architecture and contributor docs. |

## Contributor Checklist

Before editing a web repo:

1. Read the AeroBeat root `README.md`.
2. Read the target repo `README.md`.
3. Confirm the work belongs in that repo, not an adjacent repo.
4. Import sibling repos only through declared public `@aerobeat/web-*` exports.
5. Run the target repo's validation commands before handoff.
6. Mirror accepted cross-repo decisions into `aerobeat-web-docs` when they become contributor-facing.


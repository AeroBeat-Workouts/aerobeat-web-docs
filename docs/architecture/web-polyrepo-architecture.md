# Web Polyrepo Architecture

AeroBeat Web is a polyrepo browser-native port. The existing Godot repos remain source references and fallback paths, but the web repos are not required to copy Godot contracts when browser-native seams need a better shape.

## Repo And Package Naming

Web repo folders use:

```text
aerobeat-web-<domain>
```

Published package names use the `@aerobeat` scope:

```text
@aerobeat/web-<domain>
```

New packages start private at version `0.0.0` until an accepted release plan changes that posture.

## Routing Rules

Use the owning repo for the domain being changed:

| Work | Owning repo |
| --- | --- |
| Product shell, service wiring, integration flows, release artifacts | `aerobeat-web-assembly` |
| Service IDs, event names, element names, shared data shapes | `aerobeat-web-contracts` |
| Design tokens, CSS variables, reset/base styles, theme primitives | `aerobeat-web-style` |
| Web Components, HUD, menus, calibration UI, settings UI | `aerobeat-web-ui` |
| Replay/fake pose input, device-independent input routing, gameplay-facing input events | `aerobeat-web-input` |
| Camera lifecycle, pose-frame production, vendor CV orchestration | `aerobeat-web-cv` |
| Web Audio clock, song playback, timeline sync | `aerobeat-web-audio` |
| WebGL2 gameplay renderer, visuals, debug overlays | `aerobeat-web-renderer` |
| Mode rules, hit windows, scoring, Flow and Boxing logic | `aerobeat-web-gameplay` |
| Canonical map/event fixtures, converted content, content loading boundaries | `aerobeat-web-content` |
| Frame budgets, quality levels, diagnostics, adaptive performance policy | `aerobeat-web-performance` |
| Product-owned static assets and asset manifests | `aerobeat-web-assets` |
| Environment profiles, feature flags, runtime/build config | `aerobeat-web-config` |
| Generators, validators, conversion helpers, repo tooling | `aerobeat-web-tools` |
| Public-facing docs and contributor docs intended for publication | `aerobeat-web-docs` |
| Third-party runtime dependency isolation | `aerobeat-web-vendor-*` |

Do not put UI components in assembly, performance policy in CV, content conversion in vendor repos, or vendor-native object graphs in gameplay, UI, renderer, input, or assembly code.

## Code Posture

Web implementation repos use JavaScript with `// @ts-check` and strict JSDoc. Public shapes, service contracts, event payloads, classes, functions, methods, exported values, and test data must be documented.

Do not use `any`, star-shaped JSDoc escapes, or undocumented public structures. Unknown external values must be narrowed into documented AeroBeat shapes before they cross repo boundaries.

Repos import other AeroBeat packages only through declared public `@aerobeat/web-*` exports. Shared IDs and data shapes live in `aerobeat-web-contracts`; implementation code lives in the owning domain repo.

## Standard Repo Shape

Standard AeroBeat-authored package repos keep package code at the repo root with source under `src/`. Tests, demos, scenes, Playwright config, debug data, and local dependency wiring live under `.testbed/`.

Generated `.testbed/node_modules` symlinks are local state and must not be committed. Testbed code should import the repo under test through the same public package path a consumer would use.

Exceptions:

- `aerobeat-web-assembly` keeps root-level app dependencies, demos, tests, Vite config, and release scripts because it is the deployable product shell.
- `aerobeat-web-docs` uses a docs-native authoring, preview, and hosting shape.
- Forked vendor repos preserve upstream layout. AeroBeat wrapper repos above them own normalized AeroBeat APIs.

## Web Component Rules

Every visible UI primitive, control, widget, panel, HUD element, modal, overlay, and screen must be a named `aero-*` Web Component.

Screens and testbed scenes may own layout and composition, but visible controls, panels, status displays, and repeated visual elements must be imported components. Each Web Component must have a standalone scene under `.testbed/scenes/` and representative debug data under `.testbed/debug-data/`.

Tests or static validators must enforce the component-only screen/scene rule. Review preference alone is not enough.

## First Wave

The first web repo wave after templates and contracts is focused on mobile/desktop input proof, not full product assembly:

- `aerobeat-web-vendor-movenet`
- `aerobeat-web-cv`
- `aerobeat-web-input`
- `aerobeat-web-style`
- `aerobeat-web-ui`

This wave should preserve the legacy proving posture: live camera, video/replay/fixture sources, visible debug state, Boxing and Flow proving scenes, camera selection persistence, and regression tests. Web scenes replace Godot scenes with `.testbed/scenes/*.scene.html` built from `aero-*` components.

## Release Posture

Repo-local testbeds are for rapid iteration. `aerobeat-web-assembly` owns product release artifacts and should prove raw `0.0.1` artifact creation and GitHub release submission wiring before minified builds or future machine-dependent bytecode outputs.

Do not host or redistribute unlicensed music content.


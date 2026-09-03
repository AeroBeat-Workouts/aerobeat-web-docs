# Web Repo Map

Use this map before opening a PR or assigning work. If a change crosses several domains, put shared shapes in `aerobeat-web-contracts` and keep implementation details in each owning repo.

## Current Repos

These repositories exist with accepted, actively validated implementations:

| Repo | Purpose |
| --- | --- |
| `aerobeat-web-contracts` | Shared service IDs, event names, element names, and public data shapes. |
| `aerobeat-web-video` | Browser camera/video/replay media lifecycle, stream ownership, and media surface descriptors (`aero.video.media`). |
| `aerobeat-web-cv` | Pose-frame production above the video facade, vendor-neutral CV orchestration, and phone-testable performance presets. |
| `aerobeat-web-input` | Device-independent routing from calibrated pose/body-grid data into gameplay-facing input evidence. |
| `aerobeat-web-style` | Design tokens, CSS variables, base styles, and theme primitives. |
| `aerobeat-web-ui` | Native `aero-*` Web Components: calibration screens, content-discovery presenters, gameplay HUDs, Visual Test transport, and testbed UI. |
| `aerobeat-web-audio` | Per-game Web Audio playback, authoritative clock snapshots, timeline sync, and beat/time conversion. |
| `aerobeat-web-renderer` | PlayCanvas gameplay renderer (`aero.renderer.playcanvas`) with pinned canonical GLB assets, bounded feedback, landmark overlays, and debug camera controls. |
| `aerobeat-web-gameplay` | Deterministic session coordinator: mode rules, hit windows, scoring, and Boxing/Flow judgement. |
| `aerobeat-web-content` | Validated song-package loading, hash verification, runtime variant resolution, and content loading boundaries. |
| `aerobeat-web-content-authoring` | Provider-neutral browser conversion, IndexedDB authoring persistence, and deterministic `AEROPKG1` package export. |
| `aerobeat-web-assembly` | Deployable `<aero-game>` app shell, service wiring, media-lease arbitration, Test/Visual Test presentation modes, and release artifacts. |

## Vendor Repos

Third-party runtime dependencies stay isolated behind AeroBeat-owned adapter boundaries. Production CV composes only the MediaPipe adapter; MoveNet and ONNX Runtime remain research/reference adapters that release proof rejects, and BeatSaver acquisition is provider-side only:

| Repo | Purpose |
| --- | --- |
| `aerobeat-web-vendor-movenet` | TensorFlow.js/MoveNet adapter boundary (research/reference path). |
| `aerobeat-web-vendor-mediapipe` | MediaPipe Tasks Vision Pose Landmarker adapter boundary; the only vendor composed into production CV. |
| `aerobeat-web-vendor-onnxruntime` | ONNX Runtime Web + RTMPose-t evaluation adapter boundary (research/reference path). |
| `aerobeat-web-vendor-beatsaver` | BeatSaver acquisition, provider-hash verification, and untrusted ZIP inspection behind neutral source-manifest contracts. |

## Planned Repos

These domains are routed in the root README matrix but have no repository yet; confirm with the orchestrator before assuming one exists:

| Repo | Purpose |
| --- | --- |
| `aerobeat-web-performance` | Frame budgets, diagnostics, quality levels, and adaptive performance policy. |
| `aerobeat-web-assets` | Product-owned static assets and asset manifests. |
| `aerobeat-web-config` | Environment profiles, feature flags, and runtime/build configuration. |
| `aerobeat-web-tools` | Generators, validators, conversion helpers, and repo tooling. |

## This Docs Repo

| Repo | Purpose |
| --- | --- |
| `aerobeat-web-docs` | Public-facing web architecture and contributor docs for the web family. |

## Contributor Checklist

Before editing a web repo:

1. Read the AeroBeat root `README.md`.
2. Read the target repo `README.md`.
3. Confirm the work belongs in that repo, not an adjacent repo.
4. Import sibling repos only through declared public `@aerobeat/web-*` exports.
5. Run the target repo's validation commands before handoff.
6. Mirror accepted cross-repo decisions into `aerobeat-web-docs` when they become contributor-facing.

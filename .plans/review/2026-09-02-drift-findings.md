# Docs Drift Findings — AeroBeat Web Docs Direction Refresh

**Date:** 2026-09-02 (audit performed 2026-09-03)
**Bead:** `aerobeat-web-docs-yb5`
**Role:** research
**Plan:** `.plans/2026-09-02-web-docs-direction-refresh.md`

Method: every substantive claim in the five docs pages plus `mkdocs.yml` was compared against
the `Responsibility` / `Public API` sections of each sibling web repo README under
`/home/derrick/.dsh/projects/aerobeat/`, with recent git logs as supporting context.
No content page, `mkdocs.yml`, or README was edited. Nothing committed.

Legend per finding: **stale claim (quote)** → current truth → source evidence.

---

## Page 1: `docs/index.md`

### I-1 — Renderer stack listed as "WebGL2"

> "It uses JavaScript, JSDoc, HTML, CSS, native Web Components, Web Audio, WebGL2, and browser camera/CV APIs." (`docs/index.md:3`)

**Current truth:** the gameplay renderer is PlayCanvas-based (`aero.renderer.playcanvas`);
the legacy WebGL2 facade was removed, not aliased. The root README still says "WebGL2"
(stale wording propagated from there), so this is shared-upstream staleness — but the docs
site should state PlayCanvas explicitly for the renderer layer.

**Evidence:** `aerobeat-web-renderer/README.md:3,13,28` (PlayCanvas ownership, service ID,
"removed rather than aliased"). Note `aerobeat-web-video/README.md:9,35` still says "WebGL2
drawing"/"owns WebGL2 gameplay drawing" — upstream stale wording worth relaying.

### I-2 — "first web repo family" framing on the repo-map pointer

> "[Web Repo Map](contributors/web-repo-map.md) tells contributors where work belongs across the first web repo family." (`docs/index.md:10`)

**Current truth:** the family is no longer "first wave" only; 14 implementation repos plus docs
exist with closed audited work (see Missing Coverage). The pointer should describe the current family.

**Evidence:** directory listing shows 16 `aerobeat-web-*` non-template repos; git logs show audit
closures through 2026-09-02 in every implementation repo.

---

## Page 2: `docs/architecture/web-polyrepo-architecture.md`

### A-1 — Routing table folds camera lifecycle into CV (hypothesis 2 confirmed)

> "| Camera lifecycle, pose-frame production, vendor CV orchestration | `aerobeat-web-cv` |" (`web-polyrepo-architecture.md:32`)

**Current truth:** browser camera/video/replay **media lifecycle** split out into its own repo
`aerobeat-web-video` with service ID `aero.video.media`. CV consumes media surfaces; it no longer
owns them at the browser facade level. Root README already reflects the split (`README.md:35`).

**Evidence:** `aerobeat-web-video/README.md:1-17` (Responsibility + `createBrowserVideoMediaFacade()`
/ `aero.video.media`); root `README.md:35`; `aerobeat-web-video/README.md:32` ("`aerobeat-web-cv`
consumes media surfaces later to produce normalized pose frames").

### A-2 — Routing table renderer row says "WebGL2 gameplay renderer" (hypothesis 1 confirmed)

> "| WebGL2 gameplay renderer, visuals, debug overlays | `aerobeat-web-renderer` |" (`web-polyrepo-architecture.md:34`)

**Current truth:** PlayCanvas renderer (`createAeroPlayCanvasRenderer()` /
`AeroPlayCanvasRenderer`, service ID `aero.renderer.playcanvas`). Legacy `AeroWebGl2Renderer`,
`createAeroWebGl2Renderer`, `aero.renderer.webgl2`, and gameplay-plan exports removed, not aliased.
Debug overlays are now the debug-camera + landmark-overlay surfaces in the renderer README.

**Evidence:** `aerobeat-web-renderer/README.md:13` (service ID), `:28` (removal-not-alias).

### A-3 — Routing table has no content-authoring row; vendors only implicit

The routing table (`web-polyrepo-architecture.md:25-42`) is copied from the archived 2026-08-23
plan and lacks the domain that now exists between content and vendor:

- `aerobeat-web-content-authoring` (conversion, IndexedDB persistence, `AEROPKG1` export) — exists and is heavily built out.
- `aerobeat-web-vendor-beatsaver` (provider acquisition/source inspection) — exists; the generic "Third-party runtime dependency isolation | `aerobeat-web-vendor-*`" row covers it only implicitly.

**Evidence:** `aerobeat-web-content-authoring/README.md:1-24`; `aerobeat-web-vendor-beatsaver/README.md:1-31`.
Upstream note: root `README.md:26-46` routing matrix is *also* missing a content-authoring row — relay to
orchestrator; docs should mirror root truth once corrected rather than invent it unilaterally.

### A-4 — "First Wave" section is stale framing (hypothesis 4 confirmed)

> "## First Wave — The first web repo wave after templates and contracts is focused on mobile/desktop input proof, not full product assembly: `aerobeat-web-vendor-movenet`, `aerobeat-web-cv`, `aerobeat-web-input`, `aerobeat-web-style`, `aerobeat-web-ui`" (`web-polyrepo-architecture.md:74-84`)

**Current truth:** that wave shipped; the project moved well past input proof into audio, content
pipeline, gameplay judgement, PlayCanvas renderer, and assembly release proofs. Audio/renderer/gameplay/
content/assembly all have closed audited work (`aerobeat-web-audio` "Close audited audio mixer work",
`aerobeat-web-gameplay` "close audited visual test gameplay", renderer "Render canonical gameplay assets",
assembly environment/release commits). The section should become a current-family description (or merge into
routing rules), keeping the historical proving posture only where still relevant.

**Evidence:** git logs `-5` per repo; READMEs of audio/content/gameplay/assembly describe full product runtime behavior, not scaffolding.

### A-5 — Release posture says assembly "should prove raw `0.0.1` artifact creation" (hypothesis 6 confirmed)

> "`aerobeat-web-assembly` owns product release artifacts and should prove raw `0.0.1` artifact creation and GitHub release submission wiring before minified builds or future machine-dependent bytecode outputs." (`web-polyrepo-architecture.md:88`)

**Current truth:** assembly is at package version `0.0.34`; the deterministic raw release proof is
`0.0.33`, with every `0.0.32` and older release byte declared immutable. Release work grew a reproducible
npm-pack policy (`release-pack-policy.js` normalize/verify flow) plus pinned-asset posture: renderer owns
pinned canonical gameplay assets `0.0.2`; assembly owns the alien-moon environment payload with hashes.
Docs should describe the current raw-release-proof posture, not the pre-`0.0.1` intent.

**Evidence:** `aerobeat-web-assembly/package.json:3` (`"version": "0.0.34"`); assembly README `:115`
("The current deterministic raw release proof is `0.0.33`; every `0.0.32` and older release byte remains
immutable"); assembly README `:100-113` pack policy; `aerobeat-web-renderer/src/gameplay-assets.js:3`
(`gameplayAssetReleaseVersion="0.0.2"`).

### A-6 — Vendor topology beyond MoveNet (hypothesis 3 confirmed)

The page never names vendors beyond the generic `aerobeat-web-vendor-*` row, and the sibling "first wave"
list names only movenet. Current vendor family:

| Repo | Truth |
| --- | --- |
| `aerobeat-web-vendor-movenet` | TensorFlow.js/MoveNet adapter; research/reference path — **not** a CV production dependency |
| `aerobeat-web-vendor-mediapipe` | MediaPipe Tasks Vision Pose Landmarker adapter; **the only production-composed vendor** (`@mediapipe/tasks-vision@1.0.1`, Lite float16 `/1/`, GPU-WebGL) |
| `aerobeat-web-vendor-onnxruntime` | ONNX Runtime Web + RTMPose-t evaluation backend (research/reference, not a CV dependency) |
| `aerobeat-web-vendor-beatsaver` | BeatSaver/SongCore acquisition, provider-hash and untrusted ZIP inspection |

**Evidence:** `aerobeat-web-cv/README.md:44` ("Production assembly currently composes only
`aerobeat-web-vendor-mediapipe`; MoveNet and ONNX Runtime remain separate research/reference repos and are
not CV dependencies"); assembly README "Locked production CV" (`:52-65`, "Release proof rejects MoveNet,
TensorFlow pose, ONNX Runtime, and ONNX model assets"); vendor READMEs as listed.

### A-7 — Testbed-shape exceptions verified (no drift)

Exceptions list (`web-polyrepo-architecture.md:60-64`): assembly, docs, forked vendors. Matches current
reality (assembly app exception confirmed by root-level package.json/scripts; docs-native shape confirmed).
The "forked vendor repos preserve upstream layout" sentence has no current web-repo example — all four web
vendor repos are AeroBeat-authored shapes; keep as forward-looking policy or note it applies to Godot-era vendors.

### A-8 — Code posture / component rules verified (no drift)

`@ts-check` + strict JSDoc, no `any`, public-import-only boundaries, `aero-*` component-only scenes:
every repo README repeats these exactly (`aerobeat-web-contracts/README.md:39-41`, cv `:50-52`, etc.).

---

## Page 3: `docs/architecture/secure-testbed-serving.md`

**0 drift findings.** The secure-context, Tailscale `tailscale cert`/`mkcert`, and `testbed:serve`
expectations match the root README testbed posture (`aerobeat/README.md:60-65`) and repo behavior;
`testbed:serve` verified present in cv/video/ui/renderer package.json scripts.

Optional enrichment (S-1): phone secure-context validation is now a routine QA gate, not a future
expectation — mobile-CV-responsiveness plan `.plans/2026-08-25-mobile-cv-responsiveness.md` exists at the
root, and assembly README `:132` names "A final physical Chromium/Android secure-context camera/calibration/playability
handoff ... part of the cross-repo QA task". Low priority.

---

## Page 4: `docs/contributors/web-repo-map.md`

### R-1 — "Current First-Wave Repos" mislabels status (hypothesis 4 confirmed)

> "## Current First-Wave Repos" (`web-repo-map.md:5`)

All six are active with post-first-wave functionality. Specifically:
- CV row still claims "Camera lifecycle, frame sources…" — media lifecycle moved to `aerobeat-web-video` (see A-1). **Careful:** the CV README itself retains "owns camera permissions, camera lifecycle, live/video/replay frame sources" wording (`aerobeat-web-cv/README.md:6-7`) at the permissions/frame-source-consumption level while video owns the browser media facade; describe the boundary as "pose-frame production + vendor orchestration above the video facade" and flag the residual cv README wording to the orchestrator rather than silently contradicting it.
- UI row understates growth: content-discovery presenters (`aero-beatsaver-browser`, `aero-content-library`), calibration, HUDs, Visual Test transport per `aerobeat-web-ui/README.md:13-31`.

### R-2 — CV row missing performance-preset posture (hypothesis 5 confirmed)

**Current truth:** `aeroCvPerformancePresets` / `getAeroCvPerformancePreset()` expose phone-testable CV
workload presets: Direct full (default, Derrick-selected baseline), direct downscale 256/192/160 isolating
main-thread inference resize, plus explicitly experimental worker variants. Contributor docs should carry a
one-line summary, not the full matrix.

**Evidence:** `aerobeat-web-cv/README.md:17` and Performance Presets section `:20-33`.

### R-3 — "Future Or Adjacent Repos" table is stale (hypothesis 4 confirmed)

> "## Future Or Adjacent Repos" (`web-repo-map.md:16`) listing assembly, audio, renderer, gameplay, content, performance, assets, config, tools, docs.

**Current truth:**
- **Active now** (exist with audited implementation): `aerobeat-web-assembly`, `aerobeat-web-audio`, `aerobeat-web-renderer`, `aerobeat-web-gameplay`, `aerobeat-web-content`, plus docs itself → move to a Current table.
- **Not yet created** (planned only): `aerobeat-web-performance`, `aerobeat-web-assets`, `aerobeat-web-config`, `aerobeat-web-tools` — verified absent via `ls` → label as planned.
- **Missing from every table:** `aerobeat-web-video`, `aerobeat-web-content-authoring`, and vendors mediapipe/onnxruntime/beatsaver (map lists only movenet).

### R-4 — Renderer row "WebGL2 gameplay renderer" (hypothesis 1 confirmed)

> "| `aerobeat-web-renderer` | WebGL2 gameplay renderer, target visuals, effects, and debug overlays. |" (`web-repo-map.md:22`)

Current truth: PlayCanvas renderer with pinned canonical GLB gameplay assets (`0.0.2`). Evidence: A-2 sources plus `aerobeat-web-renderer/README.md:24`.

### R-5 — MoveNet row overstates its role

> "| `aerobeat-web-vendor-movenet` | TensorFlow.js/MoveNet isolation behind an AeroBeat adapter boundary. |" (`web-repo-map.md:10`)

The purpose sentence is still true, but the map should note production CV composes **mediapipe**, with
movenet/onnxruntime as research/reference adapters — otherwise contributors wire MoveNet into production paths
assembly explicitly rejects. Evidence: cv README `:44`; assembly README `:65`.

---

## Page 5: `docs/contributors/documentation-handoff.md`

**0 drift findings.** Every rule (put-here / keep-local / avoid-duplication / contracts boundary) matches this
repo's own README boundaries (`aerobeat-web-docs/README.md:36-41`) and the identical handoff sections in every
implementation README. Optional enrichment (H-1): the "Put It Here" list could name the now-active domains
(video, content-authoring, vendor adapters) as examples of multi-repo surfaces. Nothing here is wrong.

---

## Page 6: `mkdocs.yml`

**0 drift findings.** Nav covers exactly the five pages; all paths exist; site_url/repo_url match the git remote
(`git@github.com:AeroBeat-Workouts/aerobeat-web-docs.git`). No nav changes needed unless new pages are added (plan forbids new top-level pages without orchestrator sign-off).

---

## Missing Coverage

Existing repos/domains absent from docs entirely:

| Missing | Evidence |
| --- | --- |
| `aerobeat-web-video` — media lifecycle repo, `aero.video.media` | exists; zero mentions in any docs page (grep) |
| `aerobeat-web-content-authoring` — conversion/persistence/export | exists; zero mentions in any docs page (grep) |
| `aerobeat-web-vendor-mediapipe` (production vendor), `-onnxruntime`, `-beatsaver` | exist; only movenet appears in docs |
| Visual Test / Test presentation modes (assembly-owned, gameplay purpose-split `play` vs `visual_test`) | assembly README Test/Visual Test sections; gameplay README `:57`; no contributor-facing mention anywhere |
| Pinned canonical gameplay assets posture (`0.0.2`) and owned environment payload | renderer README `:24-26`, assembly README `:44-46`; no docs mention |
| CV performance presets (phone-testable) | cv README `:17,20-33`; no docs mention |

Upstream gaps (out of this repo's edit scope; relay to orchestrator): root `aerobeat/README.md` routing matrix
lacks a content-authoring row and still says "WebGL2 gameplay renderer" (`README.md:3,38`);
`aerobeat-web-video/README.md:9,35` still refers to WebGL2 drawing.

---

## Findings Count Per Page

| Page | Drift findings | Optional enrichments |
| --- | --- | --- |
| `docs/index.md` | 2 (I-1, I-2) | — |
| `docs/architecture/web-polyrepo-architecture.md` | 6 (A-1..A-6); A-7/A-8 verified no-drift | — |
| `docs/architecture/secure-testbed-serving.md` | 0 | S-1 |
| `docs/contributors/web-repo-map.md` | 5 (R-1..R-5) | — |
| `docs/contributors/documentation-handoff.md` | 0 | H-1 |
| `mkdocs.yml` | 0 | — |

Total drift findings: **13**.

## Hypothesis Verdicts

1. **Renderer PlayCanvas pivot; legacy WebGL2 removed not aliased** — CONFIRMED (`aerobeat-web-renderer/README.md:13,28`).
2. **Media/camera lifecycle split out of CV into `aerobeat-web-video` with `aero.video.media`** — CONFIRMED (video README `:16`; root README `:35`). Nuance: cv README wording retains "camera lifecycle" at permissions/frame-source level; describe boundary carefully.
3. **Vendor topology grew beyond movenet** — CONFIRMED (mediapipe production-only, onnxruntime + beatsaver exist).
4. **First-wave/future framing stale; content-authoring undocumented** — CONFIRMED both halves.
5. **CV phone-testable performance presets** — CONFIRMED (cv README `:17`, Performance Presets section).
6. **Release posture grew beyond raw `0.0.1` wording** — CONFIRMED (`0.0.34` package, `0.0.33` deterministic raw release proof, immutable older bytes, reproducible pack policy; pinned gameplay assets `0.0.2`; Test/Visual Test modes).

## Recommended Edit Order

1. **Architecture page routing table + vendor topology** (A-1, A-2, A-3, A-6) — largest contributor-facing error surface; fixes wrong-owner routing for media lifecycle and stale renderer engine claims.
2. **Architecture "First Wave" → current-family framing + Release Posture** (A-4, A-5) — converts historical framing to accepted-current posture using assembly/renderer truth.
3. **Repo map tables rebuild** (R-1..R-5) — promote built repos to Current, add video/content-authoring/vendor rows, label performance/assets/config/tools as planned, CV preset + production-vendor one-liners. Keep wording consistent with step 1.
4. **Index page** (I-1, I-2) — small wording fixes once family framing language is settled.
5. **Secure testbed serving** (S-1) — optional enrichment only; lowest priority.
6. Handoff page and mkdocs.yml — no edits required.

## Notes For QA / Coders

- Do not copy active-plan sections verbatim; summarize at contributor level (plan scope boundary).
- CV/video boundary language: video owns the browser media facade/streams (`aero.video.media`); CV consumes media surfaces for pose-frame production and vendor orchestration. Flag residual "camera lifecycle" wording in `aerobeat-web-cv/README.md:6-7` to the orchestrator instead of silently contradicting it.
- Keep "Do not host or redistribute unlicensed music content." (architecture `:90`) — still true; matches beatsaver README legal boundary.

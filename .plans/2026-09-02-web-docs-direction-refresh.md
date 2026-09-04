# AeroBeat Web Docs Direction Refresh

**Date:** 2026-09-02
**Status:** In Progress (approved 2026-09-02)
**Last Updated:** 2026-09-02 — restructuring recorded below
**Blocked Reason:** None
**Agent:** cookie (orchestrator)

---

## Goal

Bring `aerobeat-web-docs` in line with the accepted current AeroBeat web direction: it was seeded on 2026-08-23 at first-wave planning time and has not been touched since, while the web polyrepo family advanced through CV/input proof, PlayCanvas renderer adoption, a video/media lifecycle split, audio/content/gameplay/assembly buildout, and vendor adapter additions.

This is also the deliberate real-work stress workload Derrick requested for the local model: broad multi-repo read-and-synthesize documentation work executed through the coder/QA/auditor delegation loop with a strict `mkdocs build --strict` gate.

---

## Overview

The docs repo contains five content pages plus `mkdocs.yml`, all authored against the archived 2026-08-23 polyrepo architecture plan. Since then the implementation repos accumulated audited commits (2026-08-25 through 2026-09-02) that materially changed contributor-facing truth:

1. **Renderer engine pivot.** `aerobeat-web-renderer` is now a PlayCanvas-based renderer (`aero.renderer.playcanvas`); the legacy WebGL2 renderer and its service ID were removed, not aliased. The docs still describe the renderer as "WebGL2 gameplay renderer."
2. **Media lifecycle split.** `aerobeat-web-video` exists as its own repo owning browser camera/media-stream/video/replay lifecycle (`aero.video.media`), split out from CV. Docs fold camera lifecycle into `aerobeat-web-cv` and never mention the video repo.
3. **Vendor topology grew.** `aerobeat-web-vendor-mediapipe`, `aerobeat-web-vendor-onnxruntime`, and `aerobeat-web-vendor-beatsaver` exist behind adapter boundaries; docs mention only `vendor-movenet`.
4. **"First wave" framing is stale.** Docs present audio, renderer, gameplay, content, assembly as "future or adjacent"; all of them are now active with closed audited work. `aerobeat-web-content-authoring` exists and appears in no doc page.
5. **CV performance posture grew.** CV exposes phone-testable performance presets (direct full/downscale, experimental worker variants) matching the mobile-CV-responsiveness direction; contributor docs should reflect that at summary level.
6. **Release posture grew.** Assembly now pins canonical gameplay assets (`0.0.2`, Derrick-approved) and owns Test/Visual Test presentation modes; release-posture prose should be re-checked against assembly truth rather than the 2026-08-23 raw `0.0.1` wording.

Scope boundaries: edit only in-repo pages plus `mkdocs.yml` nav if needed; no new top-level pages without orchestrator sign-off; do not copy active-plan sections verbatim; leave legacy `aerobeat-docs` untouched; the untracked aerobeat root README is outside this repo's commit scope. The broken docs-native venv (created under the old `.openclaw` path) was already rebuilt with `uv` as local prep and baseline `mkdocs build --strict` passes on the pre-change tree.

---

## REFERENCES

| ID | Description | Path |
| --- | --- | --- |
| `REF-01` | Current routing truth for web domains (root README, includes video split) | `/home/derrick/.dsh/projects/aerobeat/README.md` |
| `REF-02` | Renderer truth: PlayCanvas adoption, WebGL2 removal | `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-renderer/README.md` |
| `REF-03` | Video facade truth: media lifecycle ownership | `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-video/README.md` |
| `REF-04` | CV truth: camera/CV boundary, performance presets | `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-cv/README.md` |
| `REF-05` | Assembly truth: `<aero-game>` shell, Test/Visual Test, pinned assets | `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-assembly/README.md` |
| `REF-06` | Content-authoring truth: conversion and package export boundary | `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-content-authoring/README.md` |
| `REF-07` | Docs placement rules for this repo (what belongs here vs repo-local) | `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-docs/README.md` |
| `REF-08` | Archived first-wave architecture plan the docs were written against | `/home/derrick/.dsh/projects/aerobeat/.plans/archive/2026-08-23-aerobeat-web-polyrepo-architecture.md` |

---

## DSH Goal

**Goal ID:** `goal-0dbef3bf-e6af-4858-903e-439e3b96d41f`
**Objective:** Execute `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-docs/.plans/2026-09-02-web-docs-direction-refresh.md` in `/home/derrick/.dsh/projects/aerobeat/aerobeat-web-docs` for the docs-refresh Beads. Milestones: [pending] 1) drift audit across web repos; [pending] 2) refresh architecture pages; [pending] 3) refresh contributor/index pages; [pending] 4) QA strict build and consistency pass; [pending] 5) commit, push, audit verification. Complete when the plan is updated, `mkdocs build --strict` passes, completed Beads are closed, and intentional changes are committed/pushed to `origin/main`; block only when the same concrete blocker persists across the configured goal rounds.
**DSH Task List Mirror:** Created (all pending)
**Max Goal Rounds:** Deployment default
**Continuation Status:** Complete (goal closed by orchestrator after all milestones verified)

---

## Tasks

> **Restructuring decision (round 9):** the drift-audit child ran long without artifacts; rather than idle-block, both coder children were launched directly from REF-backed truth and the audit was demoted to a supplementary QA input. Task prompts below reflect the adjusted dependency.

### Task 1: Drift audit against current repo truth

**Bead ID:** `aerobeat-web-docs-yb5`
**SubAgent:** standalone `subagent` `867d3427-cc98-4884-8629-c381eefd6fa2` — launch verified via `list_agents` (running)
**Role:** `research`
**References:** `REF-01`..`REF-08`, all docs pages
**Prompt:** Read every page under `docs/` plus `mkdocs.yml` in the docs repo and every `aerobeat-web-*` README named in REFs; produce a per-page drift findings report (stale claim → current truth → source file) written to `.plans/review/2026-09-02-drift-findings.md`. Do not edit content pages.

**Status:** Complete — Bead closed. Findings at `.plans/review/2026-09-02-drift-findings.md` (13 findings; all six hypotheses confirmed with file+line evidence). Release posture truth: assembly package `0.0.34`, deterministic raw release proof `0.0.33`, pinned gameplay assets `0.0.2`; production CV composes vendor-mediapipe only (movenet/onnxruntime research/reference). Follow-up filed outside plan scope: `aerobeat-web-video-9jq` (stale WebGL2 wording in video README); root `aerobeat/README.md` also stale (WebGL2 line 3, missing content-authoring row) but is untracked glue — flagged to Derrick at wrap-up.

---

### Task 2: Refresh architecture pages

**Bead ID:** `aerobeat-web-docs-cwr`
**SubAgent:** standalone `subagent` `8f3c387d-22c8-4a13-9150-4f4f6572e75a` (coder A) — FAILED after partial work (routing-table fix applied: video/CV split, PlayCanvas renderer line; empty closing message). Reconciled via `git diff`; retired. Idempotent retry launched: `8fe51262-390f-4e7e-a9dc-468bfa07de31` (verified running) with findings report as supplementary input.
**Role:** `coder`
**References:** `REF-01`, `REF-02`, `REF-03`, `REF-04`, `REF-05`, `REF-08`; Task 1 findings
**Prompt:** Update `docs/architecture/web-polyrepo-architecture.md` (renderer engine truth, video/CV split in routing table, vendor topology, drop first-wave-only framing, release posture vs assembly truth) and `docs/architecture/secure-testbed-serving.md` if the findings show drift. Contributor-level summaries only; no active-plan copying; no new pages; do not touch `mkdocs.yml`; do not run `mkdocs build`; do not commit.

**Status:** Implemented via idempotent retry; Bead open pending QA + audit closure.

**Results:** failed child's routing fixes preserved (video/CV split, PlayCanvas row); retry added content-authoring row (A-3), Repo Family reframing with vendor topology and planned-domain labels (A-4/A-6), forked-vendor annotation (A-7), Release Posture rewrite against assembly truth — raw release proof `0.0.33`, immutable older bytes, reproducible npm-pack policy, pinned gameplay assets `0.0.2` (A-5). secure-testbed-serving verified zero-drift plus S-1 enrichment (phone secure-context as routine QA gate, `tailscale serve` path). Orchestrator verification: no stale WebGL2 claims; single content-authoring row; duplicate fixed. Contradictions relayed upstream (cv README lifecycle wording; root/video WebGL2 wording; root missing content-authoring row).

---

### Task 3: Refresh contributor and index docs pages

**Bead ID:** `aerobeat-web-docs-vzt`
**SubAgent:** standalone `subagent` `6d4da984-8203-437b-b15c-85a3ab430a8d` (coder B) — launch verified running
**Role:** `coder`
**References:** `REF-01`, `REF-05`, `REF-06`, `REF-07`; Task 1 findings
**Prompt:** Update `docs/index.md`, `docs/contributors/web-repo-map.md`, and `docs/contributors/documentation-handoff.md`: promote built repos from "future or adjacent" to current, add video/content-authoring/vendor rows, replace first-wave framing with the current family map, keep the contributor checklist. Do not touch `mkdocs.yml` or architecture pages; do not run `mkdocs build`; do not commit.

**Status:** Implemented — child settled clean; Bead open pending QA + audit closure.

**Results:** web-repo-map rebuilt (Current Repos = 12 built impl repos incl. video + content-authoring; Vendor Repos section with mediapipe-only production CV truth, movenet/onnxruntime research-reference; Planned Repos performance/assets/config/tools verified absent on disk; docs own micro-table; checklist preserved verbatim). index refreshed: WebGL2 → "WebGL-based rendering through PlayCanvas", current-family framing. documentation-handoff: zero drift verified rule-by-rule, one optional enrichment line. Orchestrator grep verification: no stale "first wave"/"WebGL2" in contributor pages or index. Follow-ups relayed: residual cv README camera-lifecycle wording; root README WebGL2 + missing content-authoring row (untracked glue).

---

### Task 4: QA strict build and consistency pass

**Bead ID:** `aerobeat-web-docs-scj`
**SubAgent:** standalone `subagent` `0500d23c-6045-4f07-b45a-dd0d96a653b7` (qa) — launch verified running
**Role:** `qa`
**References:** `REF-01`..`REF-08`, Task 1 findings
**Prompt:** After both coder tasks land, run `venv/bin/mkdocs build --strict` in the docs repo (venv is rebuilt and local). Verify nav integrity, internal links, no stale WebGL2/first-wave claims remain, cross-page consistency between architecture and contributor pages, and fidelity to REF sources. Report pass/fail per page with evidence; fix trivial link/nav defects directly, escalate content gaps.

**Status:** Pass — strict build exit 0 twice; all 13 findings verified resolved; consistency checks pass (no stale WebGL2, identical vendor topology/planned labels, no duplicate rows, nav covers exactly 5 pages). QA applied one trivial fix (tailscale serve wording aligned to assembly `docs/secure-context.md` / checkpoint plan: AeroBeat fronts on its own port, e.g. `--https=8443`, preserving shared 443). Escalated gaps recorded: upstream README staleness (root WebGL2 rows, missing content-authoring row, video README lifecycle wording) — docs deliberately diverge per plan; low-priority note that package versions sit at `0.1.0` while the "start private at 0.0.0" policy line remains accurate. Bead left in_progress for auditor closure.

---

### Task 5: Commit, push, audit verification

**Bead ID:** `aerobeat-web-docs-div`
**SubAgent:** orchestrator commit `d3cdc4d` + push `bf0a376..d3cdc4d main -> main` (status clean vs origin/main) + standalone `subagent` audit `6d8da766-d972-4cf8-955d-47e9c8436e24` — FAILED after ~2h with empty closing message (server-side long-prefill kill, since fixed by Derrick to a 1-hour cap). Reconciled: no beads closed, no file edits beyond orchestrator-owned plan record. Retired; idempotent retry launched `0d97dbdb-f5f3-4fb0-a4f1-fc28d2025ff3` (verified running) with incremental-report instruction so partial results survive. That child then terminated abnormally fast after only announcing skill loading (no checks run, no closures, no edits — reconciled same as before); resumed via `send_message` continuation on the same child (delivery confirmed) rather than relaunching. That child reported chunks 1–5 PASS-with-caveat incrementally but was interrupted before closures; orchestrator session also interrupted; closure instruction re-queued to the same child after reconciliation (`cwr/vzt/scj` in_progress, `div` claimed, `yb5` closed, follow-up `fiq` open).
**Role:** `orchestrator`, `auditor`
**References:** all REFs, final diff
**Prompt (orchestrator):** On QA pass, commit the intentional docs changes and push to `origin/main`; verify with `git status --short --branch`. **Prompt (auditor):** Independently verify final diff against plan tasks, Beads state, findings coverage, commit/push status, and absence of secrets or copied active-plan sections; report any mismatch before Bead closure.

**Status:** Complete. Commit `d3cdc4d` pushed and verified (`HEAD == origin/main`, tree clean except this record). Audit verdict: chunks 1–5 all PASS-with-caveat per child `0d97dbdb` (commit scope exact 8 files, no secrets, no venv/site artifacts; pushed state verified; independent strict build exit 0; truth spot-checks pass — release-posture numbers accurate at commit time, upstream advanced since to raw proof `0.0.35` / gameplay assets `0.0.3`, ruled upstream drift per Derrick and tracked as `fiq`). **Role deviation (documented):** the audit child completed its verification but stalled three times on the final mechanical closure step (two model-side failures plus one post-interruption idle); orchestrator closed `cwr`/`vzt`/`scj` directly citing the child's per-check evidence in closure reasons. `div` closed by orchestrator after this record's commit/push verification.

---

## Final Results

**Status:** Complete

**What We Built:** The public web docs site (`aerobeat-web-docs`) now reflects the accepted current AeroBeat web direction: PlayCanvas renderer truth (WebGL2 removed, not aliased), the video/CV media-lifecycle split, the full current repo family (12 built implementation repos including video + content-authoring), vendor topology with mediapipe-only production CV, clearly-labeled planned domains, and release-posture prose matching assembly truth at commit time. Five pages updated, strict build green, all 13 audited drift findings resolved.

**Reference Check:** `REF-01`..`REF-08` all satisfied by the final pages (QA per-finding verification + auditor truth spot-checks). Deliberate deviations: docs state PlayCanvas/current routing while upstream root README and video README carry stale wording (tracked as follow-ups, not edited in this scope); Release Posture version numbers lag upstream by design (Derrick: future passes handle drift) with `fiq` filed to de-pin the wording.

**Commits:**
- `d3cdc4d` - Refresh web docs for PlayCanvas, video-split, and current vendor truth (5 docs pages + this plan record + findings report + Beads ledger)
- plan-record follow-up commit (this final update + archive move; see `git log`)

**Lessons Learned:** (1) Local-model child runs are 1-3h wall-clock per role on this stack — parallel coder fan-out wins; expect slow writes. (2) Two model-side child failures (long-prefill kills) both recovered cleanly via reconcile-then-retry/continue with idempotent, chunked, incremental-report prompts — partial results survived every failure. (3) Pinning exact upstream version numbers into contributor docs creates a permanent drift treadmill; prefer policy language (filed as `fiq`). (4) When a verified child completes its checks but stalls on mechanical closure, the orchestrator may close with the child's evidence cited rather than re-delegate — document the deviation.

**Remaining Work (tracked):** `aerobeat-web-docs-fiq` (reword Release Posture without pinned version numbers); upstream README staleness relayed for the owning repos (root README untracked glue — Derrick to decide); `aerobeat-web-video-9jq` (stale WebGL2 wording in video README).

*Completed 2026-09-03 by cookie (orchestrator) — stress-test workload for local-model delegation, executed via the coder/QA/auditor loop.*

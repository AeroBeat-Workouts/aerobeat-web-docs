# Documentation Handoff

The active plan is the orchestration record. `aerobeat-web-docs` is the public contributor surface for accepted web architecture decisions.

## Put It Here

Mirror or summarize a decision in this repo when it:

- affects more than one `aerobeat-web-*` repo
- changes public repo routing or package boundaries
- defines contributor-facing validation expectations
- defines a public API, service, event, or data-shape rule after it is accepted
- changes secure testbed serving, release posture, or browser validation rules

## Keep It Repo-Local

Keep documentation in the implementation repo when it:

- explains internal source layout or private helpers
- records a spike log or narrow decision for one repo
- documents local scripts, fixtures, or debug data
- describes implementation details that are not yet accepted as cross-repo policy

Use each repo's `docs/` folder for local notes and `docs/decisions/` for local decisions.

## Avoid Duplication

Do not copy entire active-plan sections into this repo. Summarize accepted rules at contributor level and link readers to the owning repo or contract package when details are implementation-specific.

Shared IDs, event names, custom element names, and schema/data shapes belong in `aerobeat-web-contracts`; this docs repo explains how contributors should use those contracts after they stabilize.


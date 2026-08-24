# aerobeat-web-docs

Public and contributor-facing documentation for the browser-native AeroBeat web port.

This repo is the web-specific documentation home for accepted architecture rules that affect multiple `aerobeat-web-*` repos. Keep implementation-repo-local notes, spike logs, and narrow decisions in the owning repo's `docs/` folder.

## Relationship To `aerobeat-docs`

`aerobeat-docs` remains the legacy/general AeroBeat documentation site for broad product, design, licensing, and historical technical docs. `aerobeat-web-docs` is narrower: it documents the accepted browser-native web architecture, repo routing, contributor rules, and public handoff material for the web polyrepo family.

If a web rule affects several repos or needs to be published for contributors, mirror or summarize it here after it is accepted. If a note only explains how one implementation repo works internally, keep it in that repo.

## Local Development

This repo uses a docs-native MkDocs shape rather than the standard package `.testbed/` shape.

```bash
python3 -m venv venv
. venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Then open `http://127.0.0.1:8000/aerobeat-web-docs/`.

## Validation

Run before handoff:

```bash
mkdocs build --strict
```

This validates navigation, links, and MkDocs configuration for the public docs site.

## Documentation Boundaries

- Public web architecture and contributor docs belong here.
- Repo-local implementation decisions belong in each `aerobeat-web-*` repo under `docs/`.
- Shared IDs, event names, and data shapes belong in `aerobeat-web-contracts`; this repo explains them at contributor level after they are accepted.
- Do not duplicate every active-plan detail here. The active plan remains the orchestration record; this repo is the published contributor surface.


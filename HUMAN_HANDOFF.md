# Human handoff: ENTRANCE F1 Data

This file is the short, current handoff: what the repository is, how data
arrives, where each contract lives and how to verify it. It does not keep
history:

- **New entries** go to `docs/handoff/log/<year>-<month>.md`, newest first.
- **Everything up to 2026-10-06** (handoff v40, the full human log and the
  legacy `SESSION_HANDOFF.md`) is kept byte-for-byte in `docs/handoff/archive/`.
  Search it; do not read it whole.

`docs/handoff/README.md` explains the arrangement.

## What this repository is

The public, static JSON data for ENTRANCE, served from
`https://kwondalp.github.io/entrance-f1-data/` and read directly by the website
and the app. Data only: no application code, scraping or pipeline logic, and no
runtime dependencies (`PROJECT_RULES.md`, `AGENTS.md`).

## How data arrives

- **Automatically, through Tools.** `entrance-f1-data-tools` runs the
  owner-approved publishers: the post-session publisher after each qualifying,
  sprint and race (approval `OWNER-20260827-UNATTENDED-PUBLICATION-02`), the
  session, statistics, team, Power and Value publishers that follow it, and the
  Paddock feed every two hours. Each validates fully and pushes here last.
  Expect frequent automated commits to `main`; fetch before working.
- **By hand, only through an approved workflow.** Nobody copies tooling output
  into this repository or edits a generated statistic. A manual post-race fix
  follows `POST_RACE_UPDATE_RULES.md`: a draft diff first, applied only after
  approval.

## Start here

1. Read Git, not a handoff: `git status -sb`, `git log -5 --oneline`, `git fetch`.
2. Read `PROJECT_RULES.md`, `AGENTS.md` and `AI_HANDOFF.yaml`.
3. Read `docs/maintenance.md`: every contract's entry point, scope authority
   and the validation commands (run from Tools).
4. Before any post-race work, read `POST_RACE_UPDATE_RULES.md`.

When a piece of work is done, write it up in the log and change only the
affected handoff entries, then check the sizes (`docs/handoff/README.md`).

## Where things are

| Contract | Path | Scope authority |
| --- | --- | --- |
| Current season | `data/`, `data/f1/`, `f1/current/v1/` | `f1/current/v1/manifest.json` |
| Results Archive | `f1/results-archive/` | `f1/results-archive/current/manifest.json` |
| Stats | `f1/stats-lab/v1/`, `f1/stats-core/v1/`, `f1/stats-metric-backfill/v1/`, `f1/stats-catalogue-completion/v1/` | Each package's manifest |
| Session inputs | `f1/session-results/v1/`, `f1/session-statistics/v1/`, `f1/statistics-inputs/v1/` | Each manifest |
| Rankings | `f1/rankings/` | Each versioned manifest |
| Profiles, circuits, social | `f1/profiles/`, `f1/profile-statistics/v1/`, `f1/circuits/v1/`, `f1/social/v1/` | Each manifest |
| Historical Records | `schemas/published-historical-records.v1.schema.json` | Schema only; no dataset |

A package's cutoff, coverage and checksums come from its manifest, never from a
handoff or an old candidate note.

## Verifying

```console
python -c "import json, pathlib; [json.loads(p.read_text(encoding='utf-8')) for p in pathlib.Path('.').rglob('*.json')]"
git diff --check
git status -sb
```

Then the Tools audits listed in `docs/maintenance.md`. Preserve exact UTF-8/LF
bytes (`.gitattributes`), and check the served endpoint after publication before
claiming new coverage is live.

## Open work

`AI_HANDOFF.yaml` `pending`, `blocked` and `nextActions` are the full lists:
Historical Records stay schema-only until the producer has an eligible,
approved record, and the retained Beta contracts need review before any further
authority is granted.

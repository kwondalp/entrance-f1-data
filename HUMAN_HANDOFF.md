# Human handoff: ENTRANCE F1 Data

## Project purpose

This repository owns the stable static JSON contracts published for ENTRANCE consumers. It is a published-data repository, not an API server, application, scraper, transformation pipeline, or historical ingestion system.

## Current published contract

Approved current-season files are served from `https://kwondalp.github.io/entrance-f1-data/data/`. A direct read of that endpoint verified 2026 race results through round 7, `barcelona-catalunya`, with `updatedAt: 2026-06-16T08:43:46Z`. The public driver standings have the same update timestamp.

The repository also contains newer current-season candidate content through round 9, `great-britain`, with standings, driver statistics, and race results updated at `2026-07-10T03:08:35Z`. Do not describe that candidate content as publicly published until the public endpoint is verified after an approved promotion.

`f1/stats-lab/v1/` is a separate historical preview package. Its manifest says `publish_candidate`, `notApprovedForProduction: true`, `approvalRequiredBeforePublish: true`, and `publishApproved: false`. The public Stats Lab v1 manifest URL currently returns 404, so the candidate is not a public production contract.

## How data reaches this repository

`entrance-f1-data-tools` owns ingestion, normalization, canonical data construction, audit reports, validation, and derived package preparation. It may produce candidate files and a destination plan, but it must not write this repository automatically.

The safe sequence is:

1. Produce and audit candidate data in `entrance-f1-data-tools`.
2. Resolve conflicts and retain source provenance in the tools workflow.
3. Review the proposed destination diff and obtain explicit approval.
4. Apply only the approved data changes in this repository.
5. Validate JSON, stable identities, public shapes, and manifest checksums as applicable.
6. Commit and publish only with explicit approval.
7. Synchronise `entrance-project-control` only after the product commit exists.

## Datasets and consumers

| Contract | Purpose | Verified repository state |
| --- | --- | --- |
| `data/schedule.json` | 2026 schedule and UTC session times | 22 rounds |
| `data/drivers.json` | Stable current driver identities | 22 drivers |
| `data/constructors.json` | Stable constructor identities | 11 constructors |
| `data/driver-standings.json` | Driver championship order and points | 22 entries |
| `data/constructor-standings.json` | Constructor championship order and points | 11 entries |
| `data/driver-stats.json` | Per-driver season and career values | 22 entries |
| `data/race-results.json` | Current-season classifications and constructor points | Candidate content has 9 rounds |
| `data/f1/current-grid.json` | Driver-to-constructor current-grid mapping | 22 entries |
| `data/f1/stat-metrics.json` | Current Stats Lab metric definitions | 7 metrics |
| `f1/stats-lab/v1/` | Historical derived preview package | 77 seasons; not production-approved |

`entrance-web` and `ipgutest` fetch the published current-season base URL directly. `entrance-web` can also load Stats Lab v1 from an explicit base URL and otherwise uses its own limited fallback fixture.

## Schema and provenance decisions

- Existing driver, team, constructor, race, and session IDs and public JSON shapes are stable contracts.
- Current-season contracts are represented by the existing JSON file shapes; this repository has no repository-local JSON Schema files.
- Current-season files contain `updatedAt` timestamps but do not embed source URLs or audit IDs. Source and approval evidence must therefore be checked in the approved update workflow.
- Stats Lab v1 is versioned by `manifest.json`, which records artifact paths, byte sizes, SHA-256 checksums, source snapshot checksum, audit paths, unsupported metrics, and approval flags.
- The Stats Lab canonical snapshot is intentionally excluded from the browser-facing package because of its size.
- Post-race updates follow the two-step draft-then-approved-apply process in `POST_RACE_UPDATE_RULES.md`.

## Current blockers and risks

- Public current-season race results stop at round 7 while repository candidate content reaches round 9.
- The local schedule lists Belgium as round 10 at `2026-07-19T13:00:00Z`, but `race-results.json` has no round 10 entry. Official results and standings must be verified before even drafting an update.
- Stats Lab v1 has not been approved for production and has `asOfRaceDate: 2026-06-14`, earlier than the current-season candidate coverage.
- The required approval history for prior candidate data changes is not encoded in the production JSON itself.
- There is no repository-native validation script, so validation must combine JSON parsing, targeted integrity checks, Git diffs, manifest checksum verification, and the audited producing workflow.

## How to verify data before publishing

1. Read `PROJECT_RULES.md` and, for post-race work, `POST_RACE_UPDATE_RULES.md`.
2. Verify official source URLs and compare only factual numerical values.
3. Preserve stable IDs, race keys, session keys, schema shapes, and UTC timestamps.
4. For post-race work, prepare a no-write draft diff and wait for explicit approval.
5. Parse every JSON file and run targeted reference checks for modified files.
6. For Stats Lab, verify every manifest file size and SHA-256 checksum and preserve all preview flags.
7. Confirm `git diff -- data f1/stats-lab/v1` contains only the approved production changes.
8. Re-read the public endpoint after publication before claiming new coverage is live.

Baseline read-only validation commands:

```console
python -c "import json, pathlib; [json.loads(path.read_text(encoding='utf-8')) for path in pathlib.Path('.').rglob('*.json')]"
git diff --check
git diff -- data f1/stats-lab/v1
git status -sb
```

Validate the AI handoff from the sibling control repository without writing control state:

```console
python ../entrance-project-control/scripts/sync_status.py --print
```

## How to resume on another computer

1. Clone `entrance-f1-data`, `entrance-f1-data-tools`, `entrance-project-control`, `entrance-web`, and `ipgutest` as sibling repositories.
2. Pull each repository independently; do not use submodules, subtrees, or copied source.
3. In this repository, read `PROJECT_RULES.md`, `AGENTS.md`, `AI_HANDOFF.yaml`, and this file. Read `POST_RACE_UPDATE_RULES.md` before post-race work.
4. Verify Git state with the commands below instead of trusting durable handoff text.
5. Install project-control's Python environment if handoff/schema validation is needed.
6. Finish, validate, and commit product work first with explicit approval.
7. Regenerate and separately review project-control status only after the product commit.

## Commands to verify Git state

```console
git status -sb
git log -1 --oneline
git branch --show-current
git remote -v
```

## Do-not-do list

- Do not invent, infer, or manually patch race facts or statistics.
- Do not update production JSON without verified sources, required provenance, validation, and approval.
- Do not add application, website, scraping, ingestion, transformation, or pipeline code.
- Do not add dependencies or change stable IDs, race keys, session keys, or JSON schemas without approval.
- Do not treat data-tools output or Stats Lab preview files as automatically published data.
- Do not modify sibling repositories from this repository.
- Do not store secrets, personal paths, HEAD hashes, branch names, or working-tree state in handoffs.
- Do not stage, commit, merge, push, or deploy without explicit approval.

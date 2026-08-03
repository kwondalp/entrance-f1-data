# Human handoff: ENTRANCE F1 Data

## Project purpose

This repository owns the stable static JSON contracts published for ENTRANCE consumers. It is a published-data repository, not an API server, application, scraper, transformation pipeline, or historical ingestion system.

## Current published contract

### Results Archive v1 release package

The additive package under `f1/results-archive/v1/` contains the audited 2026
classification contract through Belgian Round 10: 10 races and 220 rows. The
manifest binds the season by exact byte size and SHA-256, and the tracked Draft
2020-12 schemas define explicit classification, winner, shared-drive, and
dead-heat fields. Existing `data/` and Stats Lab files were not changed.
Seasons 1950–2025 remain absent because structural completeness is not
archive-specific factual review or publication approval. See
`docs/RESULTS_ARCHIVE_V1.md`. The manifest's `applicationState` is immutable
generation-time provenance, not live release status; read current Git and
canonical-endpoint state directly.

Approved current-season files are served from `https://kwondalp.github.io/entrance-f1-data/data/`. Direct endpoint verification on 2026-08-02 found 2026 race results through round 10, `belgium`, with `updatedAt: 2026-07-26T10:54:55Z`; all 17 protected public contract files were byte-identical to the committed Git baseline.

The current-season results, standings, and driver statistics contain 10 completed rounds through Belgium and preserve the prior official-result corrections for tied standings and `NC`/`DNS` classifications. Hungary and the Netherlands remain outside the completed-race cutoff.

`f1/stats-lab/v1/` is a separate historical package. Its official-pole values have passed both the production-data application and the separately authorised Belgian-cutoff publication integration. The manifest says `production_ready`, `productionApplicationApproved: true`, `approvalRequiredBeforePublish: true`, and `publishApproved: true`. The checksum-portability maintenance rebinds only its manifest checksum and size metadata to committed UTF-8 LF bytes; `mainMergeApproved: false` and `deploymentApproved: false` retain their historical meaning.

The publication composes the approved Round-7 baseline of 1,156 driver and constructor attributions with exactly three official Grand Prix pole overlays for rounds 8-10. Final totals are 1,159 on both sides with 107 driver and 50 constructor holders. The single canonical historical Mercedes identity advances from 151 to 154. The official-pole field cutoff is the 2026 Belgian Grand Prix on 2026-07-19; Sprint sessions and Hungary are excluded.

`schemas/published-historical-records.v1.schema.json` defines the future public contract for eligible Historical Records. Phase 9A adds only the schema and its documentation: no `published-historical-records.v1` dataset exists in this repository, no historical record has been published, and no empty or provisional placeholder dataset should be created.

## How data reaches this repository

`entrance-f1-data-tools` owns ingestion, normalization, canonical data construction, audit reports, validation, and derived package preparation. It may produce candidate files and a destination plan, but it must not write this repository automatically.

The safe sequence is:

1. Produce and audit candidate data in `entrance-f1-data-tools`.
2. Resolve conflicts, canonical approval, human review, and source provenance in the tools workflow.
3. Export only production-eligible records through `historical-records-api-contract.v1`, with the public producer attestation `all_required_gates_passed`.
4. Review the proposed destination diff and obtain separate publication approval.
5. Apply only the approved data changes in this repository.
6. Validate JSON, stable identities, public shapes, manifest checksums, and the published contract as applicable.
7. Commit and publish only with explicit approval.
8. Synchronise `entrance-project-control` only after the product commit exists.

This repository validates the public boundary. It must not reinterpret producer-internal evidence, review queues, canonical decisions, or builder state.

## Datasets and consumers

| Contract | Purpose | Verified repository state |
| --- | --- | --- |
| `data/schedule.json` | 2026 schedule and UTC session times | 22 rounds |
| `data/drivers.json` | Stable current driver identities | 22 drivers |
| `data/constructors.json` | Stable constructor identities | 11 constructors |
| `data/driver-standings.json` | Driver championship order and points | 22 entries |
| `data/constructor-standings.json` | Constructor championship order and points | 11 entries |
| `data/driver-stats.json` | Per-driver season and career values | 22 entries |
| `data/race-results.json` | Current-season classifications and constructor points | Public baseline has 10 rounds through Belgium |
| `data/f1/current-grid.json` | Driver-to-constructor current-grid mapping | 22 entries |
| `data/f1/stat-metrics.json` | Current Stats Lab metric definitions | 7 metrics |
| `f1/stats-lab/v1/` | Historical derived package | 77 seasons; official-pole publication approved; endpoint verified 2026-08-02 |
| `schemas/published-historical-records.v1.schema.json` | Future Historical Records publication contract | Schema ready; published dataset absent |

`entrance-web` and `ipgutest` fetch the published current-season base URL directly. `entrance-web` can also load Stats Lab v1 from an explicit base URL and otherwise uses its own limited fallback fixture.

## Schema and provenance decisions

- Existing driver, team, constructor, race, and session IDs and public JSON shapes are stable contracts.
- Current-season contracts remain represented by their existing JSON file shapes. The repository-local `published-historical-records.v1` JSON Schema applies only to the future Historical Records dataset and does not change any current production JSON contract.
- Current-season files contain `updatedAt` timestamps but do not embed source URLs or audit IDs. Source and approval evidence must therefore be checked in the approved update workflow.
- Stats Lab v1 is versioned by `manifest.json`, which records relative artifact paths, byte sizes, SHA-256 checksums, stable producer and source digests, unsupported metrics, production-application approval, the approved Round 8-10 overlay, and the separate main-merge and deployment boundaries.
- The Stats Lab canonical snapshot is intentionally excluded from the browser-facing package because of its size.
- Post-race updates follow the two-step draft-then-approved-apply process in `POST_RACE_UPDATE_RULES.md`.
- Historical Records publication is fail-closed: blocked, provisional, unreviewed, or unapproved records are omitted completely rather than represented as null, empty, or blocker-bearing public rows.
- A valid published Historical Records dataset must contain at least one eligible record and a separate publication approval. If zero records are eligible, no dataset file is created.
- Consumers may accept additive optional fields within API major version 1. Removing or changing required fields, identifiers, or semantics requires a new major contract version.

## Current blockers and risks

- The public current-season endpoint was verified through round 10 on 2026-08-02. Re-read it after any later separately authorised publication or deployment before claiming newer coverage.
- Stats Lab v1 keeps the general derived package `asOfRaceDate: 2026-06-14`, while the additive `officialPoleAsOfRaceDate` is `2026-07-19`. Consumers must use the field-specific cutoff for official-pole values.
- Existing publication approval metadata does not grant new merge or deployment authority; this checksum-portability repair changes no approval meaning.
- Historical Records currently has zero publication-eligible records, so only its schema and documentation exist; there is no dataset to publish.
- The required approval history for prior candidate data changes is not encoded in the production JSON itself.
- There is no repository-native validation script, so validation must combine JSON parsing, targeted integrity checks, Git diffs, manifest checksum verification, and the audited producing workflow.

## How to verify data before publishing

1. Read `PROJECT_RULES.md` and, for post-race work, `POST_RACE_UPDATE_RULES.md`.
2. Verify official source URLs and compare only factual numerical values.
3. Preserve stable IDs, race keys, session keys, schema shapes, and UTC timestamps.
4. For post-race work, prepare a no-write draft diff and wait for explicit approval.
5. Parse every JSON file and run targeted reference checks for modified files.
6. For Stats Lab, verify every manifest file size and SHA-256 checksum, require `productionApplicationApproved: true`, `approvalRequiredBeforePublish: true`, `publishApproved: true`, and preserve `mainMergeApproved: false` plus `deploymentApproved: false`.
7. For Historical Records, validate the producer payload against `schemas/published-historical-records.v1.schema.json`, reject unsupported API major versions, reject empty datasets and ineligible records, and verify deterministic canonical serialization.
8. Confirm `git diff -- data f1/stats-lab/v1` contains only the approved production changes.
9. Re-read the public endpoint after publication before claiming new coverage is live.

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
- Do not create an empty, provisional, blocker-bearing, or otherwise production-looking Historical Records placeholder dataset.
- Do not copy producer-internal evidence IDs, review-queue IDs, canonical decision state, builder metadata, or blocker details into a public Historical Records record.
- Do not modify sibling repositories from this repository.
- Do not store secrets, personal paths, HEAD hashes, branch names, or working-tree state in handoffs.
- Do not stage, commit, merge, push, or deploy without explicit approval.

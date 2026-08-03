# entrance-f1-data

This repository is the stable static JSON data source for ENTRANCE consumers.

It contains no API server, application runtime, or automatic publishing step. Clients fetch approved files directly, and promotion from `entrance-f1-data-tools` remains a manual, reviewed operation.

## Contents

- [data/schedule.json](data/schedule.json) — season race schedule
- [data/drivers.json](data/drivers.json) — driver roster
- [data/constructors.json](data/constructors.json) — constructor roster
- [data/driver-standings.json](data/driver-standings.json) — driver championship standings
- [data/constructor-standings.json](data/constructor-standings.json) — constructor championship standings
- [data/driver-stats.json](data/driver-stats.json) — per-driver season and career stats
- [data/race-results.json](data/race-results.json) — current-season race classifications used by app recent-form views
- [data/f1/current-grid.json](data/f1/current-grid.json) — current-grid mapping for data consumers
- [data/f1/stat-metrics.json](data/f1/stat-metrics.json) — current Stats Lab metric definitions

## Stats Lab production-ready package

`f1/stats-lab/v1/` is separate from the approved current-season files under `data/`. Its `manifest.json` defines the file list, sizes, SHA-256 checksums, schema version, provenance paths, unsupported metrics, and approval flags.

The current package has passed the separately authorised official-pole production-data application and Belgian-cutoff publication integration. It is marked `production_ready` with `productionApplicationApproved: true`, `approvalRequiredBeforePublish: true`, and `publishApproved: true`.

The approved publication composes the audited Round-7 historical baseline of 1,156 official poles with three verified Grand Prix overlays for Austria, Great Britain, and Belgium. The resulting driver and constructor totals are both 1,159; Mercedes has 154 under its single canonical historical identity. Current-season distribution through Belgium is George Russell 4, Kimi Antonelli 6, Lando Norris 0, Mercedes 10, and McLaren 0. Sprint sessions and Hungary are outside this cutoff.

Direct endpoint verification on 2026-08-02 found the same Belgian-cutoff current-season data and all 17 protected public contract files byte-identical to the committed Git baseline. The checksum-portability maintenance changes only the Stats Lab manifest's byte binding and path-scoped EOL policy. Historical approval metadata remains unchanged: `mainMergeApproved: false` and `deploymentApproved: false`; repository presence must not be reinterpreted as new merge, publication, or deployment authority.

## Historical Records publication contract

`schemas/published-historical-records.v1.schema.json` defines the future static
publication shape for approved Historical Records data. Phase 9A adds only the
schema and contract documentation; no Historical Records dataset is present or
published.

Blocked, provisional, unreviewed, canonically unapproved, or publication-
unapproved records are omitted completely. When no record is production
eligible, no placeholder dataset is created. See
`docs/PUBLISHED_HISTORICAL_RECORDS_CONTRACT.md` for the publication and
compatibility rules.

## Results Archive v1

The additive `/f1/results-archive/v1/` package publishes manifest-first,
checksum-bound race classifications. Current audited coverage is 2026 through
Belgian Round 10: 10 races and 220 classification rows. No historical season is
included because archive-specific official review and publication approval are
still missing. See `docs/RESULTS_ARCHIVE_V1.md` for paths, version handling,
null/zero semantics, and consumer requirements.

## Update safety

Current-season post-race changes must follow `POST_RACE_UPDATE_RULES.md`. Preserve all stable IDs and public shapes, validate every changed JSON file, and never infer missing Formula 1 facts from an ingestion API.

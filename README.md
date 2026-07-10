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

## Stats Lab publish candidate

`f1/stats-lab/v1/` is separate from the approved current-season files under `data/`. Its `manifest.json` defines the file list, sizes, SHA-256 checksums, schema version, provenance paths, unsupported metrics, and approval flags.

The current package is explicitly marked `publish_candidate`, `notApprovedForProduction: true`, and `approvalRequiredBeforePublish: true`. Its presence in a candidate branch is not production approval. Consumers must keep that preview status visible, and no tool may promote or overwrite these files automatically.

## Update safety

Current-season post-race changes must follow `POST_RACE_UPDATE_RULES.md`. Preserve all stable IDs and public shapes, validate every changed JSON file, and never infer missing Formula 1 facts from an ingestion API.

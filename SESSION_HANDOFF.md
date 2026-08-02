# SESSION_HANDOFF.md

## Repository role

This repository stores ENTRANCE public static JSON. It does not own ingestion code, website UI, Expo application code, or automatic promotion.

## Current data layout

- `data/`: approved current-season schedule, entities, standings, driver statistics, and race results consumed by the Expo app.
- `data/f1/`: current-grid and metric-definition contracts.
- `f1/stats-lab/v1/`: production-ready derived historical Stats Lab package with separately recorded publication approval; main-merge and deployment approval fields remain false.

## Verified audit state

- All tracked JSON parses successfully.
- Current-season driver, constructor, standings, grid, schedule, stats, and race-result references are internally consistent.
- Stats Lab manifest paths, file sizes, and SHA-256 checksums match all six listed derived artifacts.
- No application runtime or dependency configuration is present.

## Promotion boundary

`entrance-f1-data-tools` may prepare a package and destination plan only under its ignored `output/` tree. A human must review conflicts, provenance, validation reports, checksums, and the destination diff before manually applying any approved package here. No audit or tooling command may commit, push, deploy, or promote automatically.

## Next required action

Review the local Stats Lab checksum-portability repair, which binds the manifest to committed UTF-8 LF bytes without changing any sporting fact or approval meaning. Any later merge, publication, or deployment still requires separate authority. Do not perform a post-race update as part of structural maintenance.

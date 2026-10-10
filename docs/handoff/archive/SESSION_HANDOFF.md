# SESSION_HANDOFF.md

## Repository role

This repository stores ENTRANCE public static JSON. It does not own ingestion code, website UI, Expo application code, or automatic promotion.

## Current data layout

- `data/`: approved current-season schedule, entities, standings, driver statistics, and race results consumed by the Expo app.
- `data/f1/`: current-grid and metric-definition contracts.
- `f1/stats-lab/v1/`: authoritative production Stats Lab package with a formal 301-statistic catalogue, 157 public metric contracts, lazy metric and detail shards, and exact range capability.
- `f1/stats-lab/beta/v1/`: one retired compatibility manifest pointing to the production v1 manifest; it no longer serves independent ranking data.

## Verified audit state

- All tracked JSON parses successfully.
- Current-season driver, constructor, standings, grid, schedule, stats, and race-result references are internally consistent.
- Stats Lab manifest paths, file sizes, and SHA-256 checksums match all 228 listed payloads plus the manifest itself.
- All 157 metric summaries and 71,030 rows reconcile to detail; the formal registry classifies 144 remaining metrics as external-evidence-blocked and leaves zero evidence-complete actionable metrics unpublished.
- No application runtime or dependency configuration is present.

## Promotion boundary

`entrance-f1-data-tools` owns generation and audit. Cross-repository application is allowed only through its guarded publisher with exact source, destination, manifest, dirtiness, checksum, and rollback gates. Repository commits and pushes remain separate Git actions even when the package application itself is approved.

## Next required action

Preserve the single production channel, the retired Beta pointer, exact summary/detail reconciliation, and stable Results Archive v1 byte identities. Future metrics may move from external-evidence-blocked to public only after new evidence and a fully audited deterministic regeneration; do not patch published rankings manually.

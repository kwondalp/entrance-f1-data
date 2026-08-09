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

The accuracy-audited package is bound to Results Archive v2 through the 2026 Hungarian Grand Prix, Round 11. Its formal catalogue retains all 301 products: 157 evidence-complete public metrics and 144 explicitly blocked products. Independent reconstruction from the official archive reconciles all 157 public products with zero blockers; compared with the previous package, 155 are corrected and 2 remain unchanged at the metric-row level.

Constructor statistics use a declared chassis-identity policy rather than engine-suffixed or organisation-lineage grouping. Original result identities remain available in detail evidence. Driver display policy uses `Kimi Antonelli` publicly while preserving source aliases. The blocked-product reassessment records 112 partial-evidence products, 32 products for which no complete official historical source was found, and zero evidence-complete actionable products left unpublished.

The current-season contracts under `data/` are generated from the same official Hungary reconciliation: race winner Lando Norris, pole Lando Norris, fastest lap Charles Leclerc, and the FIA post-race championship standings. Publication and endpoint verification remain separate from repository-candidate validation and must be performed after the normal push sequence.

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

## Results Archive v1 and v2

The additive `/f1/results-archive/v1/` package publishes manifest-first,
checksum-bound race classifications. Current audited coverage is 2026 through
Belgian Round 10: 10 races and 220 classification rows. No historical season is
included because archive-specific official review and publication approval are
still missing. See `docs/RESULTS_ARCHIVE_V1.md` for paths, version handling,
null/zero semantics, and consumer requirements.

Stable Results Archive v1 is frozen and byte-identical. The append-only
`f1/results-archive/v2/` package is the current verified race-classification
archive: 77 seasons, 1,160 Grands Prix, and 26,143 classification rows through
Hungary on 2026-07-26. `f1/results-archive/current/manifest.json` points to v2.
All historical race rows reconcile to retained Formula1.com official evidence,
and the 2026 Hungary boundary additionally records Formula1.com and FIA final
classification evidence. Historical non-champion final standings remain
explicitly provisional until season-aware chassis-versus-entrant identities are
resolved; only official champion identities are promoted from those tables.
See `docs/RESULTS_ARCHIVE_V2.md` for the consumer and status contract.

## Results Archive Beta v1 and Stats Lab Beta v1

The additive Beta namespaces publish a full-history lane without modifying
either stable v1 package:

- `f1/results-archive/beta/v1/`: 77 seasons, 1,159 races, and 26,094
  classification rows from 1950 through 2026 Round 10. The current season is
  verified; 1950–2025 are explicitly provisional.
- `f1/stats-lab/beta/v1/`: all 301 permanent Master Catalogue products with
  per-product published, provisional, blocked, or unsupported status, plus
  checksum-bound Driver, Constructor, event, and metric-table data.

Consumers must verify manifest checksums, show Beta coverage/status, preserve
null and shared-drive semantics, and disable unsupported products or range
combinations rather than inventing values. See
`docs/RESULTS_ARCHIVE_BETA_V1.md` and `docs/STATS_LAB_BETA_V1.md`.

## Update safety

Current-season post-race changes must follow `POST_RACE_UPDATE_RULES.md`. Preserve all stable IDs and public shapes, validate every changed JSON file, and never infer missing Formula 1 facts from an ingestion API.

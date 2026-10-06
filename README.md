# entrance-f1-data

This repository is the stable static JSON data source for ENTRANCE consumers.

It serves static files without an API server. Tools workflows validate and publish owner-approved sporting, Stats and ranking contracts; clients fetch those releases directly. New source-review decisions, schema changes and research promotion require their separate review and approval.

The current cutoff is declared by the published manifest for each contract.
Historical candidate reports are not current status. Consumers should use
manifest hashes or HTTP ETags to invalidate cached payloads, preserve each
metric's declared evidence coverage, and never replace unknown values with zero.
See [contract maintenance](docs/maintenance.md) for the package map and checks.

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

The 2026 schedule contains 23 consecutive rounds. Round 16 is the Bahrain Grand Prix in
Malaysia at Sepang International Circuit on 2-4 October, retaining the stable `bahrain`
race key while using Malaysia as the host country. Session timestamps remain UTC strings in
the existing consumer contract.

## Stats Lab production-ready package

`f1/stats-lab/v1/` is separate from the approved current-season files under `data/`. Its `manifest.json` defines the file list, sizes, SHA-256 checksums, schema version, provenance paths, unsupported metrics, and approval flags.

The accuracy-audited base package is bound to the exact Results Archive v2 manifest declared in `generatedFrom`. The separate backfill and completion packages extend the base catalogue. Their manifests and availability fields determine current readiness; a blocked entry in the retained base catalogue is not the status of an independently approved supplement.

The additive Stats metric backfill manifest records the owner-approved
`fastest_ever_lap` semantic migration under
`OWNER-20260825-STATS-FASTEST-EVER-SEMANTIC-01`: the unpublished zero-row
`minimum_lap_time` contract is replaced by `maximum_average_speed` without
changing either Driver or Constructor metric ID or route. Its generated-source
metadata exposes the fixed F1DB v2026.11.0 release URL, tag-fixed CC BY 4.0
licence URL, creator attribution, and ENTRANCE filtering, canonical binding,
distance/time calculation, and exclusion changes.

Constructor statistics use a declared chassis-identity policy rather than engine-suffixed or organisation-lineage grouping. Original result identities remain available in detail evidence. Driver display policy uses `Kimi Antonelli` publicly while preserving source aliases. The blocked-product reassessment records 112 partial-evidence products, 32 products for which no complete official historical source was found, and zero evidence-complete actionable products left unpublished.

Current-season contracts under `data/` share the checksum-bound seven-file `f1/current/v1` snapshot. The approved publisher reconciles them against official results and standings. Endpoint verification remains separate from candidate validation and follows Data-last activation.

## Shared Stats Core v1

`f1/stats-core/v1/` is the additive, consumer-neutral career-statistics contract for the
website and future app consumers. Its exact-ID records cover 823 Drivers and 171
Constructors and retain raw numeric zeroes. Entity-level `starts` and `fastestLaps` are
`null` with a structured reason when the verified Results Archive cannot prove a complete
career total. The checksum manifest, coverage report, and Draft 2020-12 schema are published
beside `stats.json`; no browser or app consumer should recalculate these totals.

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

## Stats metric backfill v1

`f1/stats-metric-backfill/v1/` is an additive, versioned public contract for the
exact 144 Stats metrics that required evidence beyond the existing production
package. `catalogue.json` describes every metric and points only available metrics
to lazy payloads under `metrics/`; `inventory.json` records the exact A/B/C evidence
classification; `coverage.json` reports availability; `schema.json` defines the
contract; and `manifest.json` binds all files by byte size and SHA-256.

The current partition is 140 populated, zero permission-required, and four
unavailable. Twenty-five bounded Grand Prix leader products cover 795 positively
complete events from 1982 through 2026-07-26, with 357 pre-coverage events and
eight later incomplete or ambiguous events explicitly excluded. Four Sprint
fastest-lap products cover only ten events with unique explicit rank-one source
observations. The four unavailable objects require Sprint lap-position evidence,
which is absent from the pinned source; missing events are not zero.

Consumers must display raw numeric zero as zero, keep fractional values numeric,
and use each metric's status, cutoff, completeness, and reason fields. A missing
payload or blocked metric is not zero. Partial payloads exclude unknown evidence
rows and must be labelled as evidence-scoped; they must not be presented as
complete career totals. Existing Stats Core, Stats Lab, Results Archive, schedule,
and current-season URLs and semantics are unchanged.

The evidence extensions publish 140 metric payloads: the original 75, 21 partial
metrics derived from F1DB v2026.11.0 under CC BY 4.0, two
`complete_through_cutoff` fastest-ever-lap payloads for the Driver and
Constructor record holder, eight verified-configuration circuit-record payloads,
two complete winning-age payloads, two complete Grand Slam rankings, and one
bounded-partial first-across event ledger, plus 29 CC0 lap-position and Sprint
fastest-lap payloads. The fastest-ever payloads retain average
speed, lap time, session,
event, circuit configuration, distance, and canonical identities; their public
value is independently recalculated from licensed structured data and
corroborated by the official Formula 1 historical-record claim. Exact
canonical name-or-alias binding is required and unresolved identities are
excluded. Circuit records are explicitly partial: each payload reports the 159
observed configurations and its accepted/excluded configuration counts instead
of implying all-time completeness. Winning ages cover all 116 canonical credited
winners through 2026-07-26 with independently matching F1DB and Wikidata dates.
The other four metrics are `unavailable`; all retain a null data path and must
render as unavailable, never as numeric zero, because the retained corpus lacks
an explicit Sprint lap-position table. Formula 1/FIA lap charts and
restricted timing documents are not included or redistributed.

All files under `f1/stats-metric-backfill/v1/` are canonical UTF-8 without BOM,
LF-only, and final-LF. Their manifest sizes and SHA-256 values bind those exact
bytes across clean Windows and Git-tree checkouts.

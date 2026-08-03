# Results Archive Beta v1 public contract

`f1/results-archive/beta/v1/` is an additive Beta package. It does not replace
or change the stable `f1/results-archive/v1/` package.

## Files and coverage

- `manifest.json`: 77 newest-first season entries with exact byte size and
  SHA-256 for every shard
- `seasons/1950.json` through `seasons/2026.json`: race summaries,
  classifications, standings where derivable, and explicit field support
- Coverage: 1950 through 2026 Belgian Round 10, 1,159 races and 26,094
  classification rows

The 2026 shard is `verified` because it reuses the approved stable Results
Archive v1 classifications through Round 10. Seasons 1950–2025 are
`provisional`: they are bound to the canonical snapshot and automated audits,
but have not received complete row-by-row official-source publication review.

Consumers must display that status distinction. They must preserve nulls and
must not reinterpret constructor identity as entrant identity, entry as start,
or missing fastest-lap/laps-led evidence as zero.

## Compatibility and validation

The contract uses `results-archive-beta-manifest.v1` and
`results-archive-beta-season.v1`. Consumers may accept additive optional fields
within API major version 1. Required-field or semantic changes require a new
major version.

Before use, validate both schemas, require the exact Beta namespace, verify the
selected shard's byte size and SHA-256 from the manifest, and fail closed on an
unlisted season, invalid status, ordering error, or checksum mismatch.

Repository presence does not imply stable-v1 promotion, commit, publication, or
deployment approval.

# Results Archive v1 public contract

Results Archive v1 is an additive static JSON package for race summaries and
full classifications. Its current audited coverage is the 2026 season through
Round 10, the Belgian Grand Prix: 10 races and 220 classification rows.

## Paths

```text
/f1/results-archive/v1/manifest.json
/f1/results-archive/v1/seasons/2026.json
/schemas/results-archive-manifest.v1.schema.json
/schemas/results-archive-season.v1.schema.json
```

Consumers fetch the manifest first, reject unsupported major versions, select
only a listed season path, and verify its exact byte size and SHA-256 before
parsing or rendering the season. A season file maps named fields only; object
property order is not an interface.

Each classification row exposes a stable row ID, position, driver and
constructor identities, laps, time-or-retired text, numeric points, and
explicit shared-drive/dead-heat group metadata. `null` means the approved value
is unavailable; zero is a real numeric value. Duplicate numeric positions are
valid only with one explicit shared-drive or dead-heat group. Winner summaries
derive from position-one rows and support multiple drivers and constructors.

## Coverage and publication boundary

The package intentionally contains no 1950–2025 file. Those seasons are not
production-approved for this contract even when a provisional Tools checkpoint
is structurally complete. Existing current-season files under `data/` remain
unchanged. A later race or historical season requires a new deterministic
candidate, archive-specific official verification, exact approval, schema and
audit success, and a manifest checksum update.

The manifest `applicationState` records the immutable candidate-generation and
local-application checkpoint that produced the checksum-bound public bytes. It
is not a live deployment control plane. Current commit, remote, publication,
and deployment state must be established from Git and the canonical HTTPS
resources rather than inferred from that frozen provenance snapshot.

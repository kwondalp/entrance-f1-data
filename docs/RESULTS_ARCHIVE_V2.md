# Results Archive v2

Results Archive v2 is the append-only production archive used by Stats Lab.
Consumers should first fetch `f1/results-archive/current/manifest.json`, then
verify the referenced `f1/results-archive/v2/manifest.json` checksum before
loading season shards.

## Coverage

- Seasons: 1950-2026
- Grands Prix: 1,160
- Classification rows: 26,143
- Current cutoff: 2026 Hungarian Grand Prix, Round 11, 2026-07-26
- Stable v1: preserved byte-for-byte and never redirected or overwritten

Each race classification has retained official evidence bindings. Historical
rows reconcile to the approved Formula1.com display-fact archive. The Hungary
boundary additionally binds Formula1.com race, qualifying, starting-grid and
fastest-lap pages plus FIA final classification and championship-points
documents.

## Status boundaries

Race classifications and season champion identities are verified. Historical
non-champion final standings are retained as provisional even though the
official Formula1.com tables are archived. They are not promoted until a
season-aware identity policy resolves chassis and entrant labels such as
Lola/Larrousse, Venturi/Larrousse and MF1/Spyker. Consumers must not treat a
provisional standings row as verified or use it to unlock blocked Stats Lab
metrics.

Unknown values remain null or explicitly unavailable. They are never converted
to zero. Race finishes, classifications, retirements, exclusions and starts are
separate states. Constructor grouping in Stats Lab may use a declared chassis
identity, while each detail event retains the original source constructor ID.

## Integrity

The v2 manifest binds every public season shard and the official source index by
SHA-256 and byte size. JSON is canonical UTF-8 with LF line endings. Consumers
must fail closed on checksum mismatches, unsupported major versions, missing
shards or status values they do not support.

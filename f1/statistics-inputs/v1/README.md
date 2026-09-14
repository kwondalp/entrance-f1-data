# Verified current secondary statistics inputs

Tools collects each current F1DB release after official Results publication and
on an hourly server schedule. Data publishes only the validated, immutable
`inputs.<sha256>.json` payload selected by `manifest.json`. Web consumes the
derived Stats contracts, never a local export or this provider cache.

The manifest identifies the approved calculation policy separately from the
input fingerprint. Each payload binds its exact archive release, SHA-256,
CC-BY-4.0 licence file SHA-256 and attribution. Every current race must agree
with the published official classification on participants, constructor, car,
position, completed laps and points. Missing official details, partial source
tables, checksum failures and conflicting values preserve the prior release.

The payload extends the reviewed historical baseline with current qualifying,
fastest-lap, race, Sprint, engine, chassis and practice facts. Official session
facts take precedence in downstream calculations. Exact published names or
aliases bind identities; an otherwise unresolved current driver can bind only
through the same official event car number and provider permanent number, with
all matching event observations recorded. Unbound practice participants remain
excluded. Birth dates, nationality and historical identity decisions are not
imported or approved through this contract.

`officialEvents` binds each event's original official classification. A result
correction invalidates that event's old secondary facts until collection and
validation succeed again. The generator reports held rounds instead of mixing
the old facts into corrected statistics. Unchanged verified input leaves the
manifest and retrieval timestamp unchanged. Independent publication uses a
normal fast-forward push with bounded retries; a core transaction takes priority.

The F1DB licence is attribution-based. Attribution and source bindings remain
inside the published data and generated Stats provenance. This contract does
not change the model or salary policy of Power or Value.

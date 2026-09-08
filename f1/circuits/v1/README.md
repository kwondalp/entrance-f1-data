# Circuit facts v1

The normal Race Weekend consumer loads `manifest.json`, verifies the named
snapshot's byte size and SHA-256, and joins its 23 circuits by stable `raceId`.
This additive contract supplies circuit length, first Grand Prix year, scheduled
race laps and distance, Track record, and Lap record. It is independent of the
driver/team profiles feed.

The snapshot is source-checked through 2026-09-06, with specifications observed
on 2026-09-08. All 136 established fields are populated; the two Madring record
fields are null because its first F1 weekend is still ahead. Race distance is
the published race specification, not circuit length multiplied by laps.

Track record means the fastest valid lap across official GP weekends on the
relevant configuration, including practice, qualifying and Sprint sessions.
Lap record means a Grand Prix race lap; Sprint races are excluded. Independent
record references corroborate all 22 existing track records, alongside official
timing evidence. Verification does not claim a fresh exhaustive ingestion of
every historical session; that scope is retained explicitly in `coverage`.

Each field has source IDs and every source has its URL, acquisition time and
SHA-256. The producer replays 437 retained official sources and three independent
record references. A secondary Spa digit transposition is rejected in favour of
Formula 1's exact 1:40.510 Sprint qualifying result. Austria's 1:05.619 Sainz race
lap agrees with the official Styrian results and the circuit operator; the
operator explains that the changed length comes from remeasurement. Current
2026 distance and historical record are separate facts.

Producer: `scripts/build_circuit_release.py` in `entrance-f1-data-tools`.
Tracked inputs: `fixtures/circuit-facts-evidence-20260908.v1.json` and
`fixtures/circuit-facts-release-20260908.v1.json` in that repository.
The schema is `schema.json`; source replay results are in `audit.json`.
The owner requested these facts on the normal website after the earlier local
preview proved insufficient. This package changes no current race result,
standings, historical canonical approval or driver/team profile.

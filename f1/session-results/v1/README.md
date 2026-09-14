# Session results

`manifest.json` lists independently completed sessions. Each entry identifies season, round, stable race slug, session type, start time, semantic input fingerprint, and a checksum-bound immutable `sessions/<sha256>.json` payload. Qualifying, Sprint Qualifying, Sprint and Race have separate keys. A qualifying entry never implies a completed Race.

Tools accepts two stable official classifications with complete canonical identities before core publication. `run_session_results.py` publishes accepted ledgers after core completion and on a server schedule, fills missing historical sessions from the actual official source in bounded batches, and rotates daily correction checks. Corrupt payloads fail closed; older retained ledgers cannot overwrite a newer correction. Sessions remain independently available when another session is pending.

Web Results links to each calendar weekend's `#session-results` section. `EntranceSessionResults` verifies manifest schema, publication state, byte size, checksum and session identity before rendering a classification.

The additive `startingGrid` field includes the actual official Sprint grid as
well as Race grids. A Sprint qualifying classification cannot substitute for
the starting grid. Race payloads can also carry `fastestLaps`, the complete
official personal fastest-lap table, while retaining the existing rank-one
`fastestLap` interface. Each row binds Driver, Constructor, lap number and time.
These fields share the session's immutable checksum and semantic fingerprint;
missing historical fields trigger bounded automatic detail recovery.

For the current Sprint preceding the next GP, core publication reconciles both official championship tables against the previous GP plus that Sprint. The seven-file current snapshot includes a `championshipSession` boundary in standings and driver statistics. Corrections replace the previous Sprint contribution. The GP generator restores the saved GP baseline before applying its complete Race-and-Sprint fixture, avoiding duplicate points. Value reads that verified championship boundary; GP event counts and Results archive coverage remain at the latest completed GP.

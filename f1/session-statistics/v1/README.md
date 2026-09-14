# Verified session timing for Stats

This additive contract supplies automatically collected timing facts to the
Tools Stats generators. Web consumes the resulting Stats releases. It does not
read a developer checkout, timing cache or provisional model output.

`manifest.json` has schema `entrance-session-statistics-manifest.v1`, approved
publication status, verified data status, the fixed calculation policy and its
SHA-256, and one entry per `(season, round, session)` for Race or Sprint.
Every entry binds a relative immutable JSON path, exact byte size and SHA-256,
its official session input fingerprint, calculation policy fingerprint and
normalised result fingerprint. `sessions/<sha256>.json` contains:

- Season, round, session type and the existing stable race slug.
- Official completed-lap count and contiguous lap-end leader segments.
- Recorded, non-deleted personal fastest laps and known starting-grid places.
- Existing Driver and Constructor IDs from the matching official session.
- Source library/version, retrieval time and the separately published official
  session binding. No DOB, nationality, salary or unknown record is inferred.

The producer requires the official and timing session dates, winning car and
completed-lap counts to agree. Every completed winner lap must have exactly one
leader; unknown car numbers, conflicting Driver identity, duplicate/missing
leaders and a conflicting official fastest lap withhold that timing session.
Unknown deletion status cannot establish a timed-lap record.

Tools runs this publisher after Session results publication and on its own
hourly server schedule, in bounded batches. A failed timing session preserves
its last valid entry; independent Results, Standings, Power and Value continue.
Normal source changes affect the input fingerprint. Policy changes have a
separate fingerprint. Rechecking unchanged facts leaves all published bytes
unchanged, including retrieval metadata. Concurrent Data advancement is retried
from a fresh checkout using a normal push; force updates are not used.

FastF1 3.8.3 supplies timing. Its MIT licence applies to the software, not to
upstream Formula 1 timing data. The publisher retains normalised facts and
provenance; raw provider caches remain outside this repository.

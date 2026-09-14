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
  The GP fallback certifies only times from the official fastest classification;
  other personal lap times remain unknown.
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
upstream Formula 1 timing data. When live timing is unavailable, GP lap leaders
can come from Jolpica's explicit per-lap position observations. Every source car,
name, classified position and completed-lap count must match the official result;
the session date must match, every winner lap needs one leader, and source pages
must be complete. Source URLs, HTTP failures of the primary provider and
checksums remain in provenance. Unknown lap-deletion status never certifies a
fastest-lap record. Raw provider caches remain outside this repository.

Stats consumers can reuse a timing release after an official detail-only update
only when the original immutable official payload still has exactly the same
season, round, event, session and classification. Sporting corrections invalidate
that reuse. This permits adding an official grid or personal fastest-lap table
without discarding independently verified, unchanged leader observations.

For Sprint sessions, the FIA event timing page supplies exact lap-chart and
fastest-lap PDFs when live timing is unavailable. The producer requires the
matching season, round, event and session, one explicit leader for every official
winner lap, and exact official car identities. The fastest table requires unique
ordered ranks and valid recorded times/laps. PDF URLs and hashes are retained;
raw documents stay in the producer cache. Manifest policy history preserves the
original policy binding of older valid session payloads.

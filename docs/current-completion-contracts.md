# Current profile and catalogue completion candidates

The two additive packages `f1/profiles/v1/` and
`f1/stats-catalogue-completion/v1/` are technically verified feature candidates.
Their manifests explicitly retain `publicationStatus: candidate`. No main
integration or production publication is approved by these files.

Both bind the 2026-09-06 Italian Round 13 Archive and current base Stats inputs.
The profile contains 23 identities, 22 race seats, 11 teams and 23 circuits.
The Stats supplement contains 169 payloads and 65,852 rows; source-specific
historical limits and unavailable evidence remain explicit. Exact immutable
producer and input references are in `current-completion-provenance.json`.

Existing production results, standings, Archive, Stats Core, base Stats,
metric backfill and circuit files are preserved. The only public-data additions
are the two packages and their shared supporting schema. Generation and source
replay remain in entrance-f1-data-tools, with no runtime dependency added here.

The FIA Italian entry list and subsequent official Formula 1 announcements
support Lawson at Red Bull and Tsunoda at Racing Bulls. Reserve affiliation is
independent of a temporary race seat. Hadjar is an inactive race driver due to
injury, with no fabricated reserve appointment. `seasonTeamId` preserves season
participation and is not proof of a current seat. The still-unpublished v1
contract adds `role: inactive` and `reserveTeamIds`; Web's existing blanket
non-race-to-reserve label needs correction before integration. Statistical
coverage stays September 6 even when an affiliation announcement is later.

Antonelli's seven season fastest laps are supported by the official annual
event table and the approved event-derived snapshot, with the conflicting
zero on his official profile recorded explicitly. Tsunoda's unavailable F1
profile uses sourced identity evidence and the exact audited published
statistics fallback; no new canonical age-record approval is implied.

Validation covers exact bytes/SHA-256/content addresses, complete reference
chains, schemas, source hashes, mixed-coverage rejection, factual controls and
two clean byte-identical regenerations on Windows. Web main passes 201/201;
the tested Web candidate passes 218/224 with the obsolete Tsunoda assertion and
five older baseline expectations failing. Static sync writes two directories
and 34 detail pages; 35 files actually change because Teams directory output
is already identical. No Web commit or push is part of this delivery.

After separate production approval, verify the public package bytes before
Web integration. Connect recurrent refresh only after the necessary Web helper
and role handling are integrated. The current production publisher and Pages
settings remain unchanged; existing publication can advance other packages
independently, so refresh and validate bindings again before promotion.

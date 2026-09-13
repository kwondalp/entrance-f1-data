# Power model research contract

`power/v1/manifest.json` is an explicitly unpublished current-season research
pointer. It is separate from the approved `../power/v1` contract. Normal
production clients must reject it; an explicitly marked review surface can use
its pinned, checksum-bound bytes. It does not change official sporting data.

The producer is Tools' `gp-weighted-driver-car-season-ridge-v1`, configuration
`driver-car-season-pace-research-v4`. Power is the sum of same-model Driver and
constructor-season Car effects, in log-time percentage points, lower faster.
The recorded benchmark defines zero; these are not probabilities, causal ability
measurements or qualifying/retirement outcome ratings. Only 2026 is displayed.

The model has 111 source-bound GP entries from 2019 and 2022–2026, with 98 GP
groups containing eligible measurements. Its current 24 driver/car combinations
support 9 Power values, 22 Driver values (21 distinct drivers) and 18 Car values
(8 distinct constructors). Other values remain null with their exact evidence
reason. Historical nuisance parameters still have one unidentified direction;
every displayed current contrast separately passes the identification and
GP-bootstrap gates. A unique ridge solution alone is insufficient.

`modelEvidence` contains the reference population, parameter selection,
identification audit, evaluation and a hash binding to the retained fitted-model
artifact. Every row's `componentEvidence` records independent GP count, 90%
interval, prior sensitivity and bootstrap identification fraction. Raw timing
and diagnostic fitted coefficients are retained externally, not copied here.
The additional schema is `../schemas/power-components.v1.schema.json`.

The model is **not promoted**. The 2025 retrospective loss improvement is 2.82%,
but its paired GP interval includes no improvement. The 2026 model is 9.07% worse
than the strongest tested baseline, and predictive interval coverage is 72.72%.
Transfer and weather subgroup gates also fail or lack evidence. The benchmark
was revised after diagnostics; these replays cannot establish fresh independent
validation. Source integrity, supported conditional estimates, model validation,
publication approval, manual execution and scheduled execution are separate.

Attribution: [OpenF1](https://openf1.org/) and
[FastF1](https://github.com/theOehrly/Fast-F1), with Formula 1 historical timing
and published ENTRANCE Archive identities. OpenF1 states non-commercial/share-alike
terms. Software licensing does not grant additional rights to underlying timing.
This derivative research contract does not authorise production promotion.

Validate the ordinary contracts plus this namespace with Tools:
`python scripts/validate_rankings.py --root DATA_ROOT --include-model-review`.
The reproducible producer, source policy, revision history and refresh commands
are documented in Tools' `docs/power-decomposition-model.md`.

# Power Rating contract v2

This is the explicit migration from the descriptive `power/v1` contract and
the separate `model-review` experiment. Those contracts remain unchanged.
The owner approved operational publication under
OWNER-20260913-POWER-RATING-V1-OPERATIONAL-01. Web `loading` consumes v2;
the production website remains on its existing contract.

`manifest.json` is the only current-release pointer. Fetch it without using a
stale HTTP cache, then verify its SHA-256 and byte count before reading its
`path`. Artifacts are immutable, content-addressed JSON. The release binds
methodology, source-derived evidence, current canonical roster, empirical
evaluation, fitted model, coverage ledger and consecutive GP snapshots.
`seed.json` bootstraps the cloud producer and is not a consumer release.

Values and global ranks come from the producer. Never transform the values into
a different index or fit a second model in the browser. The shared unit is
points: baseline 1000, 100 points per negative log-time percentage point,
higher stronger, no upper cap or per-release rescaling. Overall equals Driver
plus Car minus 1000 within numerical tolerance. Driver/car separation is
conditional on explicit priors, not complete causal separation.

`rows` contains every current race-seat holder with canonical driver and
constructor IDs, public profile/team IDs and three `components`. Each component
has value, global rank, status, 90% model-conditional interval, contributing GP
count, current-pair GP count, posterior/prior variance fraction and comparable
movement. Team views deduplicate the shared `car` component by constructor ID.

Supported statuses are `rated`, `provisional`, `prior-only` and `unavailable`.
Prior-only/unavailable values and ranks are null; they are not zero points.
Provisional is a ranked, evidence-supported estimate with limited information.
Filtering must not recalculate global ranks. Changes use comparable GP snapshots;
source corrections and methodology revisions suppress sporting movement.

The cutoff is the latest included verified completed GP. `lastInformativeCutoff`
separately identifies the last GP with at least two retained drivers. Missing
or corrupt new input preserves the last valid manifest and its actual cutoff.
Consumers should show that cutoff and retain a stale/error indication if refresh
fails. A repeated run with unchanged scientific inputs does not change release
ID or publication timestamp.

This v1 measures conditional dry race pace. Qualifying, reliability, incident
responsibility and unreported damage are not silently assigned points. Source
timing is attributed to OpenF1 and FastF1; raw timing is not redistributed.
OpenF1's non-commercial/share-alike terms apply to derived timing evidence.
Official Archive/Profiles contracts supply verified identities and completion
prefixes. The historical sufficient statistics are reproducible from their
checksum-bound retained sources. Full formulas, matching conditions and all
weights are in the immutable methodology artifact and producer documentation.

The empirical artifact explicitly records reused retrospective evaluation,
not a fresh independent holdout. It includes simple baselines, grouped GP
uncertainty, selection/evaluation cutoffs and the actual failure/repair audit.
An active schedule, a dispatched run, an observed scheduled execution and
verified publication are separate facts recorded in operational run reports.

# Current-strength qualifying/race research

This namespace is **research only**. It is not a production endpoint and has no mutable current pointer. The approved Power v2 namespace still serves model v1.

The generated bundle binds eight files: executable methodology, canonical joined evidence, current roster, GP-ordered evaluation, coverage ledger, fitted state, component ratings and thirteen current-season snapshots. `manifest.json` records exact producer identity, input fingerprint, file checksums, actual race cutoff and separate generation time. The Data repository contains no acquisition or calculation code.

Current evidence ends at the 2026 Italian GP, round 13, on 2026-09-06. There are 126 GP evidence groups with 124 acquired race sessions and 82 qualifying sessions across the declared history. One historical qualifying acquisition remains unavailable. All thirteen current qualifying sessions were acquired. Raw provider timing remains in the producer cache, not this publication.

All three frozen candidates failed. Dynamic qualifying MAE was 0.26278 log-time percentage points versus 0.30397 for the best simple baseline, but retained evaluation qualifying coverage was only 97/260 (37.31%), below the required 50%. Race passed the frozen gates. The two-axis result cannot be promoted because the combined acceptance requires both axes. Numeric research estimates and uncertainty do not establish public model approval.

Overall = DriverRating + CarRating − 1000, using 30% qualifying and 70% race effects in identical units. No pole/win bonuses, cumulative score, salary, execution guess or mechanical DNF penalty is added. The methodology file records priors, uncertainty, omitted causal axes and exact coverage rules.

The producer completed a real cached-source end-to-end generation and an identical-input no-op. Consecutive round-12/13 snapshots have distinct source hashes and changed estimates for all 22 current drivers. Tests protect prior bundles on corrections, partial inputs, hash/identity errors and false activation. These are implemented and observed local research operations; no new research schedule or production activation has been observed.

Producer: `entrance-f1-data-tools/scripts/run_power_strength.py`. Default-branch workflow integration and any future passed-model promotion require separate review. Do not point a normal Web consumer at this failed research namespace.

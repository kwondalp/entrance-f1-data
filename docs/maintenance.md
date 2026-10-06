# Published contract maintenance

This repository contains public data and contract documentation. Run ingestion,
calculation and audit code in `entrance-f1-data-tools`; never hand-edit generated
statistics to match a desired value or copy a research candidate into production.

| Contract | Entry point | Scope authority |
| --- | --- | --- |
| Current data | `f1/current/v1/manifest.json` | `cutoff`, exact seven-file bindings |
| Results Archive | `f1/results-archive/current/manifest.json` | Bound v2 manifest, season coverage and latest cutoff |
| Base Stats | `f1/stats-lab/v1/manifest.json` | Archive binding, exact file set and evidence |
| Stats backfill | `f1/stats-metric-backfill/v1/manifest.json` | Per-metric evidence and coverage |
| Stats completion | `f1/stats-catalogue-completion/v1/manifest.json` | Approved availability contract and bound catalogue |
| Session results | `f1/session-results/v1/manifest.json` | Independent session identity and immutable detail payloads |
| Session timing | `f1/session-statistics/v1/manifest.json` | Accepted event classification, timing coverage and policy |
| Secondary Stats inputs | `f1/statistics-inputs/v1/manifest.json` | Reviewed provider release, official event checks and policy |
| Profiles and circuits | Their respective versioned manifests | Separately reviewed source cutoffs; never relabelled by a Stats refresh |
| Power / Value / team statistics | Their respective versioned manifests | Approved model, points/cost or event-evidence inputs |

Session results, timing and secondary-input publications can finish after the
core race publication. All three request Tools' bounded change-only Stats refresh
after a successful changed push. It uses the same full candidate validation and
Data-last publication transaction. An unchanged fingerprint skips expensive work;
the follow-up cannot restart the collection chain.

## Validation

From the Tools repository, run its native tests and the read-only public audits:

```text
python scripts/validate_stats_release_candidate.py --data-root ../entrance-f1-data --web-root ../entrance-web --output output/review/stats-scope.json
python scripts/audit_stats_lab_production_candidate.py ../entrance-f1-data --archive-root ../entrance-f1-data/f1/results-archive/v2
```

Validate changed JSON, all manifest hashes/byte sizes and archive/evidence
bindings. Preserve exact UTF-8/LF source bytes. Check the served public release
after publication; a successful commit alone does not prove hosting convergence.
This data-only repository has no application build, runtime tests or lint command.

The 6 October review validates the published October 4 race boundary, 157 base
metrics with 71,579 rows, and 169 available supplementary metrics with zero
pending entries. These are dated observations, not permanent expected counts.
Current freshness must be read from the manifests and producer publication state.
The review changes documentation only; fresh generated data is published through
the already approved Tools workflow and recorded separately in the handoff.
The requested refresh completed successfully in
[run 37286577426, attempt 2](https://github.com/kwondalp/entrance-f1-data-tools/actions/runs/37286577426/attempts/2),
with full candidate validation, 340 live Data file checks and all 144 Stats routes.
The post-publication scope audit and public desktop/mobile browser checks pass;
unchanged input is now a no-op.

The later automatic
[refresh 37452192212](https://github.com/kwondalp/entrance-f1-data-tools/actions/runs/37452192212)
incorporates the subsequent session-results and timing publications, including
Grand Slam evidence. It verifies nine live Data paths and all 144 Stats routes.
The final scope audit and 15 public browser checks pass; the published input
fingerprint matches durable state. Tools' review records the startup-race fix
discovered during this real execution.

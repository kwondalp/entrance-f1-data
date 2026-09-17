# Stats availability contract (controlled release)

This is an explicit revision of the existing v1 completion contract, identified by
`availabilityContract: stats-availability.v1` in both the manifest and catalogue.
Consumers must require this identifier and validate the archive/base catalogue
bindings. A missing, stale, mismatched or corrupt supplement is an error; it must
never reactivate an older ranking as a fallback.

Each catalogue entry retains its entity, statistic ID, metric ID, route, definition,
coverage, source provenance and content-addressed payload binding:

- `availability: available` uses the existing numeric/record-table payload and
  integer row count. Existing metric coverage restrictions remain in force.
- `availability: verification_pending` has a null catalogue row count and a
  `stats-catalogue-unavailable.v1` payload. It contains identity, coverage,
  exclusions and `message: Data verification in progress`; rows, values, ranks
  and result counts are forbidden. It is neither a zero nor an empty successful
  ranking. Research implementations and source facts are retained in Tools and
  on the original candidate branches, outside the public ranking projection.

The producer derives availability from the existing evidence assessment, never
from the winner, a narrowed population, or a manual generated-data patch. The
validator rejects an available metric with incomplete evidence, inaccurate
availability counts, and a mixed package labelled fully verified.
`dataStatus: mixed` declares coexisting available and unavailable metrics.
`publicationStatus: candidate` remains until an explicit owner release approval;
this contract change grants no approval and copies no old signature.

The prepared snapshot has 155 available and 14 verification-pending completion
entries; four pre-existing unsupported definitions remain without result payloads.
The earlier 36/50 repair tally concerns a different, smaller investigation scope.
Complete public metrics outside that scope retain their existing definitions and
coverage. Race metrics needing lap order still use their separate chart coverage.

The Web consumer keeps direct routes and catalogue links, labels the pending
entries, rejects pending metric/detail/table-result reads, and ignores cached
values. In a Custom Table, available selections still render and withheld
selections are named explicitly. A pending-only table shows the unavailable
state. No CSV/file export feature exists in the affected Stats pages; result
reader guards also prevent a future export from reading pending cached rows.
Copy-link navigation preserves the selection and applies the same checks.

Both existing automatic completion publication entry points require an approved
initial availability contract, then run the same generator and validator on every
update. They cannot restore provisional rows. Profile evidence remains independently
approved through 2026-09-06 with its preserved archive, driver-stat and circuit
bindings. The selected statistics snapshot extends through 2026-09-13; no profile
or circuit cutoff is relabelled. The source-review registry is unchanged.

Integration after owner approval is Tools, compatible Web, then Data. Prepare the
reviewed Data approval update before activation, keep the production checks, and
verify exact served manifest hashes after Data publication. Web deliberately fails
closed against an older availability contract during a mismatched rollout. This
preparation does not merge, publish, deploy or dispatch a production workflow.

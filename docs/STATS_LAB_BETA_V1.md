# Stats Lab Beta v1 public contract

`f1/stats-lab/beta/v1/` is derived solely from Results Archive Beta v1. It is a
separate Beta lane and does not alter stable `f1/stats-lab/v1/`.

## Package

The checksum-bound manifest lists five derived documents:

- Driver statistics
- Constructor statistics
- event index
- the complete 301-product metric-status inventory
- precomputed metric tables

Coverage is 77 seasons, 1,159 races, and 26,094 classification rows through
2026 Round 10. The package contains 160 Driver and 141 Constructor products.
Each product is explicitly `published`, `provisional`, `blocked`, or
`unsupported`, with a reason, methodology, coverage, known exclusions, and
Custom Table capability.

## Consumer rules

- Display Beta status and declared coverage next to results.
- Never turn blocked or unsupported products into a zero ranking.
- Exclude unknown start attributions from start and DNF counts.
- Do not allocate shared-drive car laps independently to each driver.
- Do not infer fastest laps, laps led, age, Sprint, qualifying, engine, model,
  or teammate values when their source dependency is absent.
- Custom Tables currently allow the all-time 1950–2026 cutoff for supported
  scalar products. Disable grouped products and unsupported range combinations
  with their published reason.

Consumers must verify every file's byte size and SHA-256 before rendering and
fail closed on a schema, catalogue, count, or checksum mismatch. A passing Beta
package does not change the stable Stats Lab approval state.

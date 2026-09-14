# Current data snapshot v1

`manifest.json` binds the existing seven `data/*.json` response shapes to one
verified Results Archive cutoff. Each entry names an immutable
`payloads/<sha256>.json` file and declares its exact byte length and SHA-256.
Clients fetch the pointer with revalidation, verify every payload, and publish
the snapshot to the UI only after all seven files pass. A corrupt or incomplete
snapshot cannot be mixed with independently fetched mutable files.

The existing `data/` URLs remain compatible. Clients may use them only when this
additive manifest returns 404 during rollout. The season identity documents keep
their existing shapes and do not acquire an artificial `season` property.

`cutoff` is the last confirmed race. Individual `updatedAt` values are acquisition
timestamps; a qualifying-only schedule update does not advance race coverage.
The generator is `entrance-f1-data-tools/current_data_snapshot.py`, called by the
existing post-session candidate transaction. Identical inputs do not rewrite the
pointer. Old payloads remain immutable. Feature preparation does not activate the
production branch or website.

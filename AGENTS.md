# Repository instructions

Read these files before working:

1. `PROJECT_RULES.md`
2. `AGENTS.md`
3. `AI_HANDOFF.yaml`
4. `HUMAN_HANDOFF.md` for how data arrives, the contract map and how to verify
5. `POST_RACE_UPDATE_RULES.md` before any post-race work

History lives in `docs/handoff/log/` (recent) and `docs/handoff/archive/` (through 2026-10-06, unchanged). Search them for a specific decision; do not read them whole. `docs/handoff/README.md` explains the arrangement.

This is the published ENTRANCE F1 data repository, not a transformation or tooling repository. Accept only audited data from approved workflows. Do not add HTML, JavaScript, CSS, application code, scraping code, pipeline logic, runtime dependencies, or copied code from sibling repositories.

Do not invent statistics or manually patch them from memory. Do not update production data without verified sources, recorded provenance in the approved workflow, an approved diff when required, and validation. Preserve stable IDs, keys, timestamps, public shapes, and schema boundaries defined by `PROJECT_RULES.md`.

Read branch, HEAD, upstream, and working-tree facts from Git; do not store them as durable handoff facts. Do not commit, merge, push, or deploy without explicit user approval.

Whenever a material publish contract or dataset state changes, add a dated entry to `docs/handoff/log/<year>-<month>.md` and update only the affected entries of `AI_HANDOFF.yaml` (and `HUMAN_HANDOFF.md` when how data arrives, the map or verification changes); never edit `docs/handoff/archive/`. Write the record in the log, not in the handoff files, then check the sizes as `docs/handoff/README.md` describes. Keep published, proposed, and provisional data clearly separated. Synchronise `entrance-project-control` only after the product change has been committed, and never modify sibling repositories from this repository.

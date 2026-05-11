# PROJECT_RULES.md

## Repository Purpose

This repository stores remote JSON data for the ENTRANCE F1 app.

Data correctness is more important than speed. When source data is incomplete, inconsistent, or uncertain, stop and report the uncertainty instead of guessing.

This repository is data-only. It must not contain app code, app configuration, runtime dependencies, or application implementation changes.

## Allowed Work

- Updating existing JSON files in `data/` when the task explicitly requires it.
- Adding approved JSON files.
- Validating JSON files.
- Updating documentation and working rules.

## Forbidden Work

- Modifying app code.
- Adding dependencies.
- Changing JSON schemas without approval.
- Renaming existing `driverId`, `teamId`, `constructorId`, race keys, or session keys.
- Using Jolpica, OpenF1, Ergast, memory guesses, or training-data guesses for official post-race updates.
- Copying F1.com commentary, wording, descriptions, article text, or other copyrighted prose.

## Timestamp Rules

- Internal timestamps must use UTC ISO 8601 strings.
- Race and session UTC timestamps should match `data/schedule.json`.

## Data Identity Rules

- Preserve existing `driverId`, `teamId`, `constructorId`, race keys, and session keys.
- If a value is uncertain, leave the field unchanged and report the uncertainty.

## Post-Race Update Rules

Post-race updates must follow `POST_RACE_UPDATE_RULES.md`.

Every post-race update must use this two-step process:

1. Draft diff only, no file writes.
2. Apply approved diff only.

Do not apply a post-race update until the draft diff has been approved.

Validate every modified JSON file before completing an apply step.

# POST_RACE_UPDATE_RULES.md

## Required Update Context

Each post-race update must include:

- Season
- Round
- Official GP name
- Race session UTC

Race session UTC must match the relevant race session in `data/schedule.json`.

## Files To Inspect

Always inspect these files before drafting a post-race update:

- `data/schedule.json`
- `data/drivers.json`
- `data/constructors.json`
- `data/race-results.json`
- `data/driver-standings.json`
- `data/constructor-standings.json`
- `data/driver-stats.json`

## Files Allowed To Change

Only these files may be modified during a post-race update:

- `data/race-results.json`
- `data/driver-standings.json`
- `data/constructor-standings.json`
- `data/driver-stats.json`

Do not modify any other files during a post-race update unless the user explicitly approves a separate task.

## Source Priority

Use sources in this strict priority order:

1. F1.com official race result
2. F1.com official qualifying result
3. F1.com official sprint result, only if the GP had a Sprint
4. F1.com official driver standings
5. F1.com official constructor standings
6. Wikipedia only for cross-check

Forbidden sources:

- Jolpica
- OpenF1
- Ergast
- Memory guesses
- Training-data guesses
- Unverified social media

If F1.com is not updated, stop and report exactly:

```text
F1.com not updated yet
```

## Copyright Rule

Extract numerical facts only. Do not copy F1.com commentary, wording, descriptions, article text, or other copyrighted prose.

## Required Workflow

Post-race updates must use a two-step process.

Step 1: Draft diff only, no file writes.

The draft output must include:

1. Source URLs checked
2. Verification summary
3. Per-driver stat deltas
4. Proposed file-by-file diff
5. Uncertainties

Then stop and wait for approval.

Step 2: Apply approved diff only.

The apply output must include:

1. Changed files
2. JSON validation results
3. Remaining uncertainties, if any

Update `updatedAt` only after the approved diff is applied. Use the current ISO 8601 UTC timestamp.

## Race Results Rule

Use official race classification and preserve existing race key conventions.

Do not guess race result fields. If the official classification does not clearly support a field, leave it unchanged and report the uncertainty.

## Standings Rule

Use F1.com official standings for championship positions. Do not manually recalculate championship positions from points.

## Driver Stats Baseline Rule

Treat current `data/driver-stats.json` values as the correct baseline.

Do not recalculate full career totals from scratch.

Only increment season and career fields based on this specific GP weekend.

## Season Stat Rules

- `position`: official driver standings
- `points`: official driver standings
- `wins`: +1 only for Grand Prix race winner
- `podiums`: +1 for Grand Prix race P1, P2, P3
- `poles`: +1 only for official Grand Prix pole-sitter
- `fastestLaps`: +1 only for official Grand Prix race fastest lap holder
- `top10`: +1 for official race classification P1 to P10
- `dnfs`: +1 only when official classification/status confirms DNF
- `sprintWins`: +1 only for Sprint winner if Sprint weekend
- `sprintPodiums`: +1 for Sprint P1, P2, P3 if Sprint weekend

## Career Stat Rules

Use delta-only logic.

Do not overwrite career totals from an external full career table.

Increment only fields that clearly exist in the schema:

- `career.wins`
- `career.podiums`
- `career.poles`
- `career.fastestLaps`
- `career.points`
- `career.starts` or `career.races` only if field meaning is clear

## Starts And Races Rule

- Do not count DNS as a start.
- Do not count Sprint participation as a Grand Prix start.
- If unclear, leave unchanged and report uncertainty.

## DNF Rule

- Do not guess from position.
- Do not count DNS or DSQ as DNF unless the existing schema clearly treats them that way.

## Sprint Rule

- If no Sprint, leave `sprintWins` and `sprintPodiums` unchanged.
- Do not treat Sprint podiums as Grand Prix race podiums.

# How the Data handoff is kept

Until 2026-10-06 every finished phase was appended to the root handoff files,
next to a separate legacy `SESSION_HANDOFF.md`. Since 2026-10-11 the handoff is
split by how often it is needed, the same way as `entrance-web` and
`entrance-f1-data-tools`:

| File | Holds | Read |
| --- | --- | --- |
| `AI_HANDOFF.yaml` | Current state, open and blocked work, durable decisions, interfaces, validation commands. Schema-checked by project-control. | Every session |
| `HUMAN_HANDOFF.md` | What the repository is, how data arrives, the contract map and how to verify. | When starting or lost |
| `docs/handoff/log/<year>-<month>.md` | One dated entry per finished piece of work, newest first. | When recent history matters |
| `docs/handoff/archive/` | The previous files, byte-for-byte. Never edited. | Search only |

`docs/maintenance.md` remains the reference for every contract's entry point,
scope authority and validation.

Automated publications from Tools are recorded by their commits and by Tools'
durable state, not in this log. The log is for work done in this repository.

## Keeping it short

At the end of a piece of work:

1. Add a dated entry at the top of this month's log file: what changed, why,
   the files, and the checks that passed. This is where the detail goes.
2. In `AI_HANDOFF.yaml`, change only the affected entries, keep about five
   `lastCompletedWork` entries and only the latest `validation.results`, and
   bump `handoffVersion`.
3. Update `HUMAN_HANDOFF.md` only when how data arrives, the map or the
   verification steps change.
4. Validate `AI_HANDOFF.yaml` against
   `../entrance-project-control/schemas/ai-handoff.schema.json`.
5. Check the sizes. This repository holds no scripts, so use:

   ```console
   wc -c AI_HANDOFF.yaml HUMAN_HANDOFF.md docs/handoff/log/*.md
   ```

   Limits: `AI_HANDOFF.yaml` 40 KB, `HUMAN_HANDOFF.md` 20 KB, each month's log
   100 KB. When one is over, move the older part into `archive/` unchanged and
   leave a pointer.

## The archive

- `AI_HANDOFF-v40.yaml`: handoff version 40, the last single-file version.
- `HUMAN_HANDOFF-to-2026-10-06.md`: the full human log through the 2026-10-06
  published contract review.
- `SESSION_HANDOFF.md`: the legacy session summary, last describing the Stats
  Lab production channel before the automatic publishers.

Search instead of reading, for example:

```console
grep -n "^## " docs/handoff/archive/HUMAN_HANDOFF-to-2026-10-06.md
```

Git keeps every earlier version of the root files as well.

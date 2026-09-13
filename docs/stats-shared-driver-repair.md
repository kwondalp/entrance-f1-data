# Generated Stats correction awaiting operational publication

The backfill producer 1.0.2 preserves the driver ID/name mapping for shared cars. Independent reaggregation from 1,161 archived GPs verifies all 1,864 constructor/driver start combinations, including their labels. The previous 1,946-row artifact split 82 combinations through mismatched participant names.

The correction changes only the same-driver starts payload and its catalogue, inventory and manifest. Other backfill payload bytes are preserved. Coverage remains through 2026-08-23, with the declared pinned F1DB source and approved evidence assessments. Extending that coverage requires a separately reviewed lap-position assessment; no cutoff was relabelled.

The normal native backfill audit and an independent constructor/driver arithmetic audit pass. This feature diff is ready for review, but no Data main modification or operational publication is included. Until publication, the corrected Web consumer fails closed on the old duplicate grouped-count keys.

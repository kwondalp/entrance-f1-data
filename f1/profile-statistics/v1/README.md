# Official team statistics

`manifest.json` binds one immutable `statistics.<sha256>.json` by SHA-256 and byte size. The producer is Tools `run_team_statistics.py`, scheduled hourly and after post-session publication. Web `EntranceProfiles.loadTeamStatistics` consumes this contract on team pages.

Publication requires all reviewed team identities, the current verified Results archive, the exact official constructor standings, complete official Formula 1 season and career fields, matching race counts, points and positions, and reconciled race plus Sprint points. Missing or delayed values retain the previous complete release. Career figures use the official team's organisational lineage, preserving the existing profile policy; historical chassis statistics remain separate.

`inputFingerprint` binds semantic statistics, cutoff and input bindings, independently of source HTML timestamps or retrieval time. Exact reruns are no-ops. Corrected official values create a new immutable release; a remote main comparison prevents concurrent publication. `sources` retains official URLs, raw-source checksums and retrieval times. Reviewed identity, nationality and biography fields remain in the separate profile contract.

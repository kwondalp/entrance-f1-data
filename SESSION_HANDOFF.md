# SESSION_HANDOFF.md

---

## Date

2026-04-20

---

## Session Summary

Major data pipeline migration (Jolpica → remote JSON + local data), UI interaction polish (swipe-linked segmented controls), and Explore sort order change. All Jolpica/Ergast dependencies removed from the three service files. Standings, schedule, and driver stats now served from the shared remote JSON repo or local profile data. Reanimated-based SwipeSegmented component built and wired to Standings and Explore. Typecheck clean at end of session.

---

## Current Goal

Stable MVP with working race calendar, session reminders, standings, Explore, and personalisation (My Drivers / My Teams). Next focus is device verification and polish.

---

## Completed Today

- **Tab bar safe area fix**: `insets.bottom` now applied on iOS too — tab bar no longer overlaps home indicator
- **"Constructor" → "Team" rename**: All user-visible labels unified to "Team/Teams" across Explore, Standings, Me, and team detail page
- **Swipe-linked segmented control** (new — `src/components/SwipeSegmented.tsx`):
  - Reanimated v4 animated indicator driven by real-time `scrollX` shared value
  - Indicator `translateX` + `width` interpolated from measured segment layouts
  - Label colors interpolate via `interpolateColor`
  - Two variants: `pill` (Standings — standalone pills) and `segmented` (Explore — grouped container)
  - Wired to both `app/(tabs)/standings.tsx` and `app/(tabs)/explore.tsx`
  - Pager `ScrollView` → `Animated.ScrollView` with `useAnimatedScrollHandler`
- **My Drivers / My Teams picker ordering** (`app/(modals)/my-drivers.tsx`, `app/(modals)/my-teams.tsx`):
  - "You are following" section restored (tap order)
  - "All drivers" sorted by team constructor position → driver position within team (live via `useStandings`)
  - "All teams" sorted by constructor position (live)
- **Explore sort order**: All Drivers → A–Z by last name; All Teams → A–Z by team name (replaced constructor-standings sort)
- **Data pipeline — Jolpica fully removed**:
  - `src/services/scheduleApi.ts`: now fetches from `https://kwondalp.github.io/entrance-f1-data/data/schedule.json`
  - `src/services/f1Api.ts`: now fetches from remote `driver-standings.json` and `constructor-standings.json`; `DRIVER_META` map resolves driverId → name + countryCode3 locally
  - `src/services/driverStatsApi.ts`: all network code removed; reads directly from `DRIVER_PROFILES` local data
- **Remote data JSON outputs generated** (for the shared data repo):
  - `data/drivers.json` — all 22 drivers, kebab-case IDs, normalized teamIds
  - `data/constructors.json` — all 11 teams, kebab-case IDs
  - `data/driver-standings.json` — 2026 season standings skeleton (zeroed, ready for live update)
  - `data/constructor-standings.json` — 2026 season standings skeleton
- **Jolpica cleanup**:
  - `src/hooks/useSchedule.ts` comment updated
  - `PROJECT_RULES.md` updated to reference the shared remote JSON repo
  - `app/(tabs)/me.tsx`: Added "Unofficial fan app. Not affiliated with Formula 1." disclaimer row in About section

---

## Files Created, Edited, or Reviewed

| File | Status |
|---|---|
| `src/components/SwipeSegmented.tsx` | Created |
| `src/services/scheduleApi.ts` | Replaced (remote JSON fetch) |
| `src/services/f1Api.ts` | Replaced (remote JSON fetch) |
| `src/services/driverStatsApi.ts` | Replaced (local DRIVER_PROFILES only) |
| `app/(tabs)/standings.tsx` | Edited (SwipeSegmented + Animated.ScrollView) |
| `app/(tabs)/explore.tsx` | Edited (SwipeSegmented, sort order, Animated.ScrollView) |
| `app/(modals)/my-drivers.tsx` | Edited (restored "You are following", constructor-order sort) |
| `app/(modals)/my-teams.tsx` | Edited (restored "You are following", constructor-order sort) |
| `app/(tabs)/_layout.tsx` | Edited (iOS tab bar bottom inset) |
| `app/(tabs)/me.tsx` | Edited (disclaimer row) |
| `app/team/[id].tsx` | Edited ("Constructor" → "Team" label) |
| `src/hooks/useSchedule.ts` | Edited (comment update) |
| `PROJECT_RULES.md` | Edited (data source reference) |
| `SESSION_HANDOFF.md` | Updated |

---

## Current Project State

- **Explore tab**: Drivers A–Z by last name, Teams A–Z by name. My Drivers / My Teams sections (favourites) in tap order. SwipeSegmented control with fluid swipe-linked animation.
- **Standings**: SwipeSegmented with fluid animation. Leader cards + full tables. Data from remote JSON repo (30-min cache, local fallback).
- **Schedule**: Data from remote JSON repo (24h cache, local fallback).
- **Driver detail**: Season stats from local `DRIVER_PROFILES` (zeros until remote stats feed added). Career stats from local profiles.
- **Team detail**: Hero header, swipeable Overview/Drivers/Stats tabs. Complete.
- **Me tab**: My Drivers / My Teams navigation, reminders, theme, about + disclaimer.
- **Personalisation**: My Drivers / My Teams with "You are following" + constructor-sorted "All" sections. Home carousel sections working.
- **Data pipeline**: Jolpica fully removed. All live data from `kwondalp.github.io/entrance-f1-data/`.

---

## Open Issues or Risks

- **Season race stats are zeros**: `driverStatsApi.ts` now serves local data only. Wins/podiums/poles etc. in the driver Season tab all read 0 until a remote stats feed is added to the data repo.
- **Narrow iPhone visual verification**: Not verified on physical device.
- **App Version hardcoded**: `APP_VERSION = '1.0.0'` in `me.tsx`. Should read from `expo-constants`.
- **Home screen web layout**: Deferred.
- **Terms / Privacy**: Explicitly deferred by user.

---

## Important Decisions

- **Explore sort order changed to A–Z**: User requested alphabetical (last name for drivers, name for teams) instead of constructor-standings order.
- **Jolpica fully replaced**: All three service files now use either remote JSON repo or local data. No Ergast/Jolpica calls remain in the app.
- **driverStatsApi local-only**: Season race stats (wins, podiums, poles, DNFs) are zero until a remote stats feed is added. This was a deliberate step — data accuracy over stale API data.
- **SwipeSegmented reusable component**: Shared between Standings and Explore via `progress: SharedValue<number>` prop. Same motion logic, two visual variants.
- **Remote data repo IDs**: `driverId` = kebab-case full name (e.g. `lando-norris`), `constructorId` = kebab-case team name (e.g. `red-bull`, `rb`).

---

## Next Steps in Priority Order

1. **Verify on device** — Standings swipe animation, Explore sort order, My Drivers/Teams picker on actual iPhone
2. **Add season race stats feed** — add `data/driver-season-stats.json` to remote repo and wire a new fetch in `driverStatsApi.ts`
3. **Wire App Version from `expo-constants`** — replace hardcoded `'1.0.0'` in `me.tsx`
4. **Home screen polish** — review layout, ensure web does not break

---

## Restart Instructions for the Next Session

1. Say `오늘시작` to load context.
2. The agent will read `PROJECT_RULES.md` and `SESSION_HANDOFF.md` and summarise the current state.
3. Do not modify any files until you confirm the next task.
4. At end of session, say `오늘끝` to update this file.

# PROJECT_RULES.md

## 1. Project Goal

Build **Entrance** — a clean, stable F1 companion app for mobile (iOS/Android) with web support.
MVP focus: race calendar, session reminders, standings, and a personal Me tab.

---

## 2. Current Scope

- Race calendar with session times and reminders
- Per-session notification preferences (Practice / Qualifying / Race groups)
- Driver and Constructor standings
- Me tab: personal preferences, notification settings, app info
- Web support as a secondary target (mobile first)

Out of scope for now: live timing, live race data, user accounts, social features.

---

## 3. Tech Stack

| Layer | Tool |
|---|---|
| Framework | React Native 0.81.5 |
| Meta-framework | Expo ~54 |
| Routing | Expo Router ~6 |
| Language | TypeScript ~5.9 |
| Package manager | pnpm |
| Notifications | expo-notifications |
| Storage | @react-native-async-storage/async-storage |
| Icons | @expo/vector-icons (Ionicons) |
| Navigation | expo-router (file-based) |

---

## 4. General Working Rules

- Prefer the simplest solution that fits the current project structure.
- Do not add unnecessary complexity, abstractions, or boilerplate.
- Do not add new dependencies unless clearly necessary and approved.
- Do not broadly refactor or restructure folders without approval.
- Accuracy of data is more important than whether a data source is free.
- Read the relevant files before making any changes.
- Make targeted edits — do not rewrite files unless the full file needs to change.
- Do not add docstrings, comments, or type annotations to code you did not change.
- Do not add error handling for scenarios that cannot happen.
- Do not use feature flags or backwards-compatibility shims.
- Do not create helpers or abstractions for one-time operations.
- Commit message style: short imperative, English or Korean as the user prefers.

---

## 5. Package Rules

- Package manager is **pnpm**. Do not use npm or yarn commands.
- Do not add a new package without a clear reason.
- Prefer packages already in the project over adding new ones.
- If a new package is needed, state why and wait for approval before installing.
- Do not upgrade existing packages without approval.

---

## 6. Folder Structure Rules

```
app/                  Screen files and layouts (Expo Router)
  (tabs)/             Tab screens
  (modals)/           Modal screens
src/
  components/         Reusable UI components
  data/               Static data files (sessions, drivers, teams, etc.)
  lib/                Utility functions
  reminders/          Reminder/notification logic and context
  services/           External service integrations (notifications, etc.)
assets/               Images, fonts, icons
```

- Screen files belong in `app/`.
- Reusable UI components belong in `src/components/`.
- Data files belong in `src/data/`.
- Utility functions belong in `src/lib/`.
- Do not create new top-level folders without approval.

---

## 7. UI and Design Rules

- Mobile first. Web is a secondary target.
- Use `SafeAreaView` with `edges={['top']}` for screens with a scroll view.
- Use `ScrollView` for screens that may overflow.
- Do not use hardcoded pixel sizes for safe areas — use the safe area context.
- Tab bar: `height: 64`, `paddingTop: 6`, `paddingBottom: 10` to prevent label clipping.
- Color palette: white backgrounds, `#f5f5f7` screen background, `#111` primary text, `#888` secondary text, `#fbb03b` accent (tab bar active).
- Border radius on cards: `16`.
- Do not use emojis in UI unless the user explicitly requests them.
- Do not use third-party UI libraries unless approved.
- Animations: use `LayoutAnimation` for simple expand/collapse. Skip animation on initial mount using `useRef`.

---

## 8. Data Rules

- Session data lives in `src/data/sessions.ts`.
- All session timestamps must be valid ISO 8601 UTC strings (e.g., `2026-03-20T15:00:00Z`).
- Validate: no leading zeros in hours (`T013:30` is invalid), correct country codes, correct GP names.
- For standings or live data, use the shared ENTRANCE F1 remote JSON files at https://kwondalp.github.io/entrance-f1-data/. If those are insufficient, consider OpenF1 or a similar source. Accuracy matters more than cost.
- Do not hardcode data that changes seasonally without a comment noting when to update it.

---

## 9. Development Priorities

1. Stability — the app must not crash on normal use
2. Correctness — data must be accurate
3. Responsiveness — UI must respond instantly (use optimistic updates where appropriate)
4. Readability — code must be easy to follow
5. Web support — secondary, but should not be broken

---

## 10. Prohibited Actions

- Do not modify `app.json`, `package.json`, or `pnpm-lock.yaml` without approval.
- Do not push to remote without user approval.
- Do not delete files without approval.
- Do not add Terms/Privacy screens or rows — out of scope for now.
- Do not implement Theme switching — scaffold exists, implementation is deferred.
- Do not add live race data or live timing — out of scope for MVP.
- Do not skip git hooks (`--no-verify`).
- Do not force push.

---

## 11. Output Expectations for Coding Agents

- Read before you edit. Never suggest changes to files you have not read.
- Make only the changes the task requires — no scope creep.
- If a task is ambiguous, ask one focused question before proceeding.
- Report what files were changed and why.
- If you find a bug unrelated to the current task, note it but do not fix it unless asked.
- Keep responses concise. No trailing summaries of what you just did.

---

## 12. Workflow Shortcuts

### `오늘시작`
Read `PROJECT_RULES.md` and `SESSION_HANDOFF.md` first.
Then summarise: current state, open issues, and top next tasks.
Do not modify any files unless the user explicitly asks you to.

### `오늘끝`
Update `SESSION_HANDOFF.md` only.
Do not modify any application code.
Fill in: what was completed today, relevant files touched, current project state, unresolved issues, decisions made, and exact next steps in priority order.

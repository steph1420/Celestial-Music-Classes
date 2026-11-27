# Celestial — Next Chat Handoff

**Read this first when continuing the project in a new conversation.**  
**Current repository:** https://github.com/steph1420/Celestial-Music-Classes  
**Branch:** `main`  
**Project stage:** UX screen-by-screen prototyping and approval  
**Current screen:** T05 Student Directory v1.1 navigation refinement, awaiting user review

## 1. Immediate status

Four teacher-facing experiences are approved:

1. **Class Register v1.3** — approved and locked.
2. **Lesson Notes pop-up** — current design explicitly approved; retain it, do not reinvent it.
3. **History v1.2** — approved and locked, containing both By date and By student views.
4. **Teacher Student Directory v1** — approved and locked; specification: `docs/locked-student-directory.md`; prototype: `prototype/teacher-student-directory-v1.html`.

Teacher Student Directory v1 remains approved and locked. T05 v1.1 adds Student ID + Open full student profile and matches T05/T06 records; review notes: `docs/student-directory-v1.1-review.md`. T06 profile prototype: `prototype/teacher-student-profile-v1.html`.

## 2. Files in GitHub

- `prototype/class-register.html` — Class Register v1.3 (existing approved file; do not overwrite casually).
- `prototype/history-v1.2.html` — History v1.2 (added in this handoff update).
- `docs/locked-class-register.md` — locked Class Register specification.
- `docs/locked-lesson-notes-panel.md` — locked pop-up decision.
- `docs/locked-history.md` — locked History behaviour.
- `docs/PROJECT_PLAN.md` — product and delivery plan.
- `docs/BUILD_TRACKER.md` — teacher/admin screen tracker.
- `docs/ARCHITECTURE_BASELINE.md` — 19-tab data model and technical invariants.
- `docs/UX_BASELINE.md` — 10 teacher and 17 administrator screen inventory, updated for approvals.
- `docs/DECISION_LOG.md` — approved decisions and constraints.
- `docs/OPEN_DECISIONS.md` — unresolved release gates.
- `README.md` — project entry point.

## 3. Approved Class Register details

- Prototype v1.3 is locked; preserve its exact visual/interaction result.
- Compact header; no “Teacher Workspace”; no teacher selector/name on a teacher's own register.
- Subject and Class Date selectors; count label “N students”.
- P/A buttons act immediately without popup/confirmation.
- Tapping student row opens the Lesson Notes pop-up.
- Leave and Unmarked are inside the pop-up.
- Long-press enables multi-select; bulk changes affect selected students only.
- Common notes remain separate per-student records.
- Copy/paste fills empty fields by default; replacement requires confirmation.
- Light/Dark/System themes.

## 4. Approved Lesson Notes pop-up

The user said the existing pop-up is perfect and there is no need to reinvent the wheel. Keep its current design and interaction. Do not create a second lesson editor or change it to a full-screen panel unless explicitly asked.

## 5. Approved History v1.2 behaviour

### By date (default)
- Newest dates first.
- Entries grouped under date headings.
- Each record identifies student, time, subject, attendance and a short topic preview.
- Tap a record to see full details.

### By student
- A student selector appears first.
- Select one student; only that student's lesson/attendance history is displayed.
- Group by date, with multiple lessons/subjects on one date shown within that date group.
- Present is the default filter.
- All records includes Absent, Leave, Unmarked and provisional entries with clear labels.
- Tap a lesson for full detail using the established detail/pop-up pattern.

The user tested v1.2 and said: **“Looks perfect!”** Treat it as approved and locked.

## 6. Current task — Review T05 Student Directory v1.1

- The original T05 v1 remains approved and locked; do not overwrite it.
- T05 v1.1 adds Student ID to the Student overview modal and an Open full student profile action.
- The action passes the selected Student_ID to T06 using the `studentId` query parameter.
- T05 and T06 seed data use matching IDs for the same eight students. Legacy v1 localStorage IDs are migrated; newly added demo students are given a stable ID and a blank matching profile is created on demand.
- An unknown ID must never fall back to another student's profile.
- Review prototype: `prototype/teacher-student-directory-v1.1.html`.
- Review notes: `docs/student-directory-v1.1-review.md`.
- T06 profile prototype: `prototype/teacher-student-profile-v1.html`.
- Automated validation checks all prototype JavaScript, matching T05/T06 seeded IDs and the modal-to-profile ID hand-off.
- Do not lock v1.1 until the user reviews and approves it.

## 7. Overall plan and architecture

- V1 product scope is frozen.
- Approved 19-tab model and Technical Blueprint v1.1 are the architecture baseline.
- Teacher and admin are two role-aware workspaces in one application.
- Google Sheets + Apps Script is conditionally approved for a small-school initial backend, with concurrency/recovery/audit limitations.
- Full installable/offline PWA is not proven or approved.
- Do not start production implementation until all UX screens/flows are reviewed and the user signs off.
- Build and approve screens incrementally; preserve locked screens.
- Update GitHub plan/tracker/handoff at every major approval.

Read `docs/PROJECT_PLAN.md`, `docs/BUILD_TRACKER.md`, `docs/ARCHITECTURE_BASELINE.md` and `docs/OPEN_DECISIONS.md` before making architecture or scope changes.

## 8. User collaboration preferences

- Accuracy over plausibility; verify technical claims.
- If corrected, reconsider from scratch; do not argue.
- Be direct and avoid unnecessary explanation or overcomplication.
- Use all clues and prior decisions; do not ask the same question again.
- When the user asks for a prototype, actually produce an interactive prototype.
- Do not move to the next screen until the current one is tested and approved.
- Do not redesign locked screens.
- Avoid excessive gradients, glow, ornamental decoration and AI-dashboard visuals.
- Use the existing repository and extend it rather than starting over.

## 9. Important unresolved gates

See `docs/OPEN_DECISIONS.md`. Especially authentication/deployment identity, cross-teacher note visibility, timezone, currency, future session reassignment, provisional attendance, billing/no-show/tax/refund rules, group sessions and PWA proof.

## 10. Handoff prompt

Continue Celestial from this repository and these documents. History v1.2 and Class Register v1.3 are approved and locked. The next task is the Teacher Student Directory. Discuss it, then build an interactive prototype. Do not start production coding yet.

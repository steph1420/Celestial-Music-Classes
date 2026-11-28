# Celestial — Next Chat Handoff

**Read this first when continuing the project in a new conversation.**  
**Current repository:** https://github.com/steph1420/Celestial-Music-Classes  
**Branch:** `main`  
**Project stage:** UX screen-by-screen prototyping and approval  
**Current screen:** T05 v1.2 direct navigation + T06 v2 profile redesign, awaiting user review

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

## 6. Current task — Review T05 v1.2 and T06 v2

- Preserve locked T05 v1, Class Register v1.3, Lesson Notes and History v1.2 unchanged.
- T05 v1.2: student row opens the matching T06 profile directly; no Student overview modal.
- T06 v2: one global Edit profile action and one full-page form. Save/Cancel at the end.
- Parent/Guardian: checkbox per child. When unchecked, omit the entire section in read-only profile; hide but retain existing links. When enabled, at least one guardian is required and every guardian must have a phone number. Other guardian fields are optional.
- Additional Notes: one multiline note, separate from lesson notes, shared with assigned teachers.
- Other existing T06 decisions remain: optional photo, limited student-field editing, own enrolments first, other enrolments read-only, no Learning Overview, attendance summary, Call/WhatsApp/SMS and optional Email, audit trail, no finance data.
- T05 prototype: `prototype/teacher-student-directory-v1.2.html`.
- T06 prototype: `prototype/teacher-student-profile-v2.html`.
- Specs: `docs/student-directory-v1.2-review.md` and `docs/student-profile-v2-review.md`.
- Automated deployment checks cover JavaScript syntax, direct row navigation, absence of the overview modal, matching seeded Student IDs, unified editing and conditional guardian/notes requirements.
- Do not lock either new version until the user explicitly approves.

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

Continue Celestial from this repository and these documents. History v1.2 and Class Register v1.3 are approved and locked. Review the published T05 Student Directory v1.1 refinement. Do not overwrite the locked v1 baseline. Verify the profile link opens the same Student_ID in T06. Do not start production coding yet.

# Celestial — Decision Log

This file records approved decisions and constraints. New decisions should be appended with date, scope and impact. Do not silently reverse a locked decision.

## Product and architecture

| Decision | Status | Rule |
|---|---|---|
| One application, two role-aware workspaces | ✅ Approved | Teacher and administrator workspaces share one data model |
| 19-tab relational data model | ✅ Approved with conditions | See `ARCHITECTURE_BASELINE.md` |
| Simple by default, powerful underneath | 🔒 Locked principle | Keep frequent teacher actions simple; advanced capability stays deliberate |
| Google Sheets + Apps Script | ✅ Conditional approval | Small-school initial deployment only, with locks, journal, idempotency, recovery and backups |
| Single `Code.gs` entry point | ✅ Accepted with conditions | Keep internals modular |
| Full PWA/offline behaviour | ⏸ Not approved | Prove service-worker scope, installation, offline cache and auth |
| Production implementation | ⏸ Not yet authorised | UX review/prototypes first; no production coding until UX sign-off |

## Class Register — locked

- Prototype v1.3 is the approved visual/interaction baseline.
- Compact header. No “Teacher Workspace” text.
- Teacher identity is implicit in the signed-in account; no teacher selector/name on own register.
- Subject and Class Date selectors.
- Count label is “N students”.
- P and A are immediate attendance controls; no popup or confirmation.
- Tapping a student row opens the existing Lesson Notes pop-up.
- Leave and Unmarked are inside that pop-up.
- Long-press enters multi-select; bulk operations affect selected students only.
- Common lesson notes create separate per-student lesson records.
- Paste fills empty fields by default; replacing existing content requires confirmation.
- Light, Dark and System themes.
- Preserve current design; do not rebuild it.

## Lesson Notes pop-up — locked

- User explicitly said the current pop-up is perfect and does not need reinvention.
- Reuse the same visual design and interaction.
- Do not replace it with a full-screen editor or new modal pattern.
- Existing fields: attendance status, Topic Covered, Homework and Remarks; contextual student/subject/date information.
- Any future feature must fit the existing pattern unless user requests a change.

## History — locked (prototype v1.2)

- History is a single screen with By date and By student views.
- By date opens by default.
- By date is chronological, newest first, grouped by date.
- Each item shows student, time, subject, attendance and useful short topic preview; tap to open full detail.
- By student first requires selecting a student. Only that student's records then appear.
- By student defaults to Present; All records includes Absent, Leave, Unmarked and clearly labelled provisional entries.
- Multiple lessons/subjects on one date are grouped under one date heading.
- Full details open using the established pop-up/detail pattern.
- Student history respects teacher permissions; do not expose another teacher's private notes.

## Workflow and continuity

- Student has one permanent master record; multiple subject/teacher enrolments are supported.
- Teacher reassignment is distinct from ending/re-enrolling.
- Reassignment creates a successor enrolment version within the same logical group.
- Old sessions/history stay attributed to the original teacher/enrolment.
- Future sessions affected by reassignment are flagged for review, never silently moved.
- Attendance and lesson notes are separate per-participation records.
- Historical and financial records are not silently overwritten or hard-deleted.
- Application-level audit logs have Google Sheets tampering limitations; never call them cryptographically immutable.

## UX collaboration rules

- Discuss a screen, then build the interactive prototype.
- Do not stop at static mock-ups when a prototype is expected.
- Preserve approved screens as locked assets.
- Update GitHub, tracker and handoff at each approval milestone.
- Next planned screen is Teacher Student Directory.

\n## Teacher Student Directory — locked (prototype v1, 27 November 2026)
\n- Screen title: My Students; teacher roster shown once per student, regardless of multiple subject enrolments.
- Search by student name.
- Subject filters: All subjects, Piano, Vocals and Guitar.
- Student status filters: Active (default), All students and Inactive.
- List rows show student name, subject-enrolment chips and record status.
- Selecting a row opens Student overview with name, record status and subject enrolments.
- Empty results offer Clear all filters.
- Add-student modal captures name, one or more subjects and Active/Inactive status; duplicate names in the demo roster are rejected.
- Light, Dark and System themes; established Celestial shell/modal/toast patterns retained.
- Prototype uses illustrative data and browser-local persistence only. Add-student is not a grant of production teacher permission to create master records/enrolments. Backend permissions remain authoritative; no finance data is exposed to teachers.
- Specification: `docs/locked-student-directory.md`. Prototype: `prototype/teacher-student-directory-v1.html`.
- Preserve the approved screen. Any change requires a deliberate versioned revision.
\n

## T06 Student Profile — initial planning decision (27 November 2026)
- Teachers will be allowed to edit guardian contact details from the teacher-facing Student Profile.
- Exact editable fields, add/remove permissions, shared guardian record behaviour, save/audit interaction and any restrictions remain to be decided during T06 UX planning.
- This does not grant access to fee, invoice or payment information and does not change the backend-permission requirement.

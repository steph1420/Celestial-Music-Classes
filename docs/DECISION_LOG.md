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
- T05 Student Directory v1.1 navigation refinement is under review; T06 Student Profile remains the next teacher screen.


## Teacher Student Directory — locked (prototype v1, 27 November 2026)

- Screen title: My Students; teacher roster shown once per student, regardless of multiple subject enrolments.
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



## T06 Student Profile — initial planning decision (27 November 2026)
- Teachers will be allowed to edit guardian contact details from the teacher-facing Student Profile.
- Exact editable fields, add/remove permissions, shared guardian record behaviour, save/audit interaction and any restrictions remain to be decided during T06 UX planning.
- This does not grant access to fee, invoice or payment information and does not change the backend-permission requirement.

## T06 Student Profile — approved design decisions (27 November 2026)
- Layout: one vertically scrollable profile page with clearly separated sections.
- Profile photo: optional, with initials fallback.
- Student details shown: date of birth, calculated age, address, student phone, school and class/grade. Teacher edits are limited to these permitted details; student name, record status and enrolments remain outside this edit action.
- Parent/Guardian: show name, relationship, phone, separate WhatsApp number, optional email and primary-contact designation. Teachers may add, edit and remove/unlink guardians.
- Guardian master contact fields (name, phone, WhatsApp, email) are shared. Editing them updates all students linked to that guardian. Relationship and primary-contact designation are student-specific link attributes.
- Removing a guardian from one student removes that link only. Delete the shared guardian record only when no student remains linked to it.
- Guardian edits may include relationship and primary designation for the current student. Explicit Save/Cancel; record who changed what and when in the audit trail.
- Guardian contact shortcuts: Call, WhatsApp and SMS when a usable phone number exists; Email only when an email address is present.
- Enrolments: show the signed-in teacher's enrolments first, then other subjects in a separate read-only summary.
- No Learning Overview section. Do not duplicate lesson notes on this profile.
- Cross-teacher lesson notes are visible only when explicitly marked shared (AUTH-02 resolved for this policy).
- Attendance: summary counts and recent attendance, with a link to the existing History screen. Unmarked remains distinct from Present.
- No fees, invoices or payments in the teacher profile.
- Prototype: `prototype/teacher-student-profile-v1.html`; it uses illustrative data and browser-local persistence, not production storage, authentication or multi-user sync.


## Teacher Student Directory v1.1 — requested refinement (27 November 2026)
- Preserve the locked v1 prototype unchanged.
- The v1.1 overview modal displays the selected student's stable Student_ID and offers an explicit Open full student profile action.
- T05 passes the selected Student_ID to T06; T06 must resolve exactly that record and must never silently fall back to another student's profile.
- T05/T06 prototype records use matching demo IDs in the form STU-0001, etc. Legacy T05 browser-local dN IDs are migrated to stable demo IDs; newly added demo students receive the next ID.
- If a newly added directory student has no pre-seeded profile, T06 creates a blank demo profile from the same directory record and its enrolments.
- T05 v1.1 is a refinement for user review; it is not locked until user approval. See `docs/student-directory-v1.1-review.md`.



## T05 v1.2 and T06 v2 — revised profile decisions (28 November 2026)
- T05 v1 remains approved and locked. T05 v1.2 is a separate review prototype; selecting a student row opens that student's T06 profile directly. Remove the Student overview modal and intermediate action.
- T06 v2 has one global Edit profile action. Personal details, conditional parent/guardian information and Additional Notes are edited in one full-page form. Save and Cancel appear at the end of the form; no sticky action bar.
- Parent/guardian information is enabled per child by a checkbox. When unchecked, omit the entire Parent / Guardian section from the read-only profile. Unchecking hides the information but retains the child's guardian links and shared guardian records; re-enabling restores them.
- When enabled, at least one guardian must be linked and every listed guardian must have a phone number. Phone is the only mandatory guardian field; guardian name, relationship, separate WhatsApp and email are optional.
- Additional Notes is one continuous multiline note, separate from lesson notes, shared with teachers assigned to the student.
- Preserve the previously approved profile decisions: optional photo; limited student-field editing; own enrolments first and other subjects read-only; no Learning Overview; attendance summary; Call, WhatsApp, SMS and optional Email; explicit save; audit trail; no finance information.
- At the time of this planning entry, T05 v1.2 and T06 v2 were review prototypes. Their subsequent approval and lock on 28 November 2026 is recorded in the later section below. Neither prototype approval authorises production implementation.


## T05 Student Directory v1.2 and T06 Student Profile v2 — approved and locked (28 November 2026)
- User approved both published prototypes.
- T05 v1.2 is locked at `prototype/teacher-student-directory-v1.2.html`; specification: `docs/locked-student-directory-v1.2.md`. Selecting a student row opens the matching T06 profile directly; there is no overview modal.
- T06 v2 is locked at `prototype/teacher-student-profile-v2.html`; specification: `docs/locked-student-profile-v2.md`. One Edit profile action opens one full-page form; Save/Cancel appear at the end.
- Parent/Guardian information is controlled per child by a checkbox. When unchecked, the read-only section is omitted while existing guardian links/data are retained. When enabled, at least one guardian must be linked and each listed guardian must have a phone number; other guardian fields are optional.
- Additional Notes is one continuous note shared with teachers assigned to the student.
- Next teacher screen: T09 Lesson Detail / Edit. Preserve the locked Class Register Lesson Notes pop-up and History screen.

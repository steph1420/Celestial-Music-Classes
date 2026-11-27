# Celestial — Project Plan

**Project:** Celestial Music School Management  
**Repository:** `steph1420/Celestial-Music-Classes`  
**Baseline date:** 27 November 2026  
**Current phase:** Stage 4.5 — interactive UX prototyping and approval  
**Next screen:** Teacher Student Profile — teacher view (T06)

## 1. Product vision

Build a single mobile-first application for running a music school. Teachers should be able to manage their own classes, mark attendance and record lesson notes quickly. Administrators should manage students, teachers, enrolments, sessions, fees, invoices, payments, reports and audit history.

The product principle is:

> **Simple by default. Powerful underneath.**

Daily actions must be obvious and quick. More advanced capability belongs behind deliberate actions and in the underlying data model—not in the way of ordinary teaching work.

## 2. Product scope

### Included in the V1 design baseline

- Teacher and administrator workspaces in one application.
- Student, teacher, guardian, subject and enrolment management.
- Individual sessions and structurally supported group sessions.
- Attendance and student-specific lesson records.
- Student-wise and date-wise history.
- Fee schemes and effective-dated fee assignments.
- Invoice preview and controlled issue.
- Payment recording and allocation to invoices.
- Operational reports and audit/change history.
- Role-aware student and lesson visibility.

### Anticipated, but not required in the initial release

- Parent portal and parent messaging.
- Advanced timetable automation and availability.
- Student skill/progress assessment.
- Advanced notifications and analytics.

These are not to be added casually to V1. Any scope change should be deliberate and recorded.

## 3. Experience architecture

There is one application and one underlying data model, with two role-aware workspaces.

### Teacher workspace

Optimised for frequent mobile use between lessons. Teachers see their own relevant classes, assigned students, attendance and lesson records, and permitted history. Teacher access must not expose fee amounts, invoices or payments.

### Administrator workspace

Provides school-wide management of students, guardians, teachers, subjects, enrolments, sessions, finance, reports, settings and audit. An administrator recording a lesson on behalf of a teacher must be recorded as the authenticated actor, while the selected teacher remains the responsible teacher.

### Responsive behaviour

- Phone (360–480 CSS px): reference experience; compact bottom navigation, full-width controls, no spreadsheet-like tables.
- Tablet (481–1024 CSS px): same workflows with wider layouts and useful master/detail panels.
- Desktop (>1024 CSS px): persistent navigation and wider master/detail or table layouts where appropriate.

Do not invent separate tablet or desktop workflows.

## 4. Data architecture baseline

The approved logical model contains 19 tabs/tables:

| # | Table | Responsibility |
|---:|---|---|
| 1 | `App_Users` | Application identities and roles |
| 2 | `Teachers` | Teacher master records |
| 3 | `Students` | Permanent student master records |
| 4 | `Guardians` | Guardian/contact master records |
| 5 | `Student_Guardians` | Student-to-guardian relationships |
| 6 | `Subjects` | Subject catalogue |
| 7 | `Enrolments` | Effective-dated student/teacher/subject relationships |
| 8 | `Sessions` | Individual class occurrences |
| 9 | `Session_Enrolments` | Student participation in a session |
| 10 | `Attendance` | Attendance per participation |
| 11 | `Lesson_Records` | Topic, homework and remarks per participation |
| 12 | `Fee_Schemes` | Reusable fee templates |
| 13 | `Fee_Assignments` | Effective-dated student/enrolment fee agreements |
| 14 | `Invoices` | Issued invoice records |
| 15 | `Invoice_Items` | Line items and their source charges |
| 16 | `Payments` | Receipts/payment records |
| 17 | `Payment_Allocations` | Allocation of receipts to invoices |
| 18 | `Settings` | School/application configuration |
| 19 | `Audit_Log` | Change and operation journal |

### Key data rules

- A student has one permanent Student_ID and may have multiple active or historical enrolments.
- An enrolment identifies a student, teacher and subject for an effective period.
- A teacher reassignment is an easy user-facing “Change Teacher” operation but creates a successor Enrolment_ID within the same Enrolment_Group_ID. Ending and re-enrolling is a distinct operation creating a new logical group.
- Past sessions and lesson records remain linked to their original enrolment/teacher.
- Future sessions affected by reassignment are flagged for review. They are not silently moved.
- A Session is one class occurrence. Each student participation is separate.
- Attendance and lesson notes are distinct records for each participation.
- Group-session lesson content remains student-specific.
- Fee schemes are templates; fee assignments are the effective-dated agreements.
- Student-level and enrolment-level fee assignments are additive where configured. The UI must preview combined impact and warn about likely duplicate charging.
- Invoices are previewed and recalculated before issue. Issued invoices are not silently overwritten.
- Payments are receipts. Allocations connect receipts to invoices and remain distinct from the receipt itself.

## 5. Continuity, audit and non-destructive behaviour

- No hard delete of records with dependent history. Archive/deactivate instead.
- Profile edits update current state and append a before/after audit event.
- Historically significant relationship changes create successor/effective-dated records.
- Issued invoices and completed payment transactions are not silently edited; use approved void, reversal or adjustment mechanisms.
- Related mutations use Operation_ID and Change_Set_ID so they can be reviewed together.
- Records carry versions; edits check for stale versions/conflicts.
- Undo in the interface must not erase the production audit trail. A saved undo is itself a new traceable change.
- Backups, restricted workbook access, schema checks, migration logs and recovery procedures are required.

**Google Sheets limitation:** an append-only log implemented in Apps Script is not cryptographically immutable. A spreadsheet owner/editor can potentially alter cells directly. Protect the audit tab, restrict workbook access and retain independent backups. Do not describe this as tamper-proof.

## 6. Technical implementation direction

### Conditional initial backend

Google Sheets + Google Apps Script is conditionally accepted for a small-school initial deployment. A single `Code.gs` entry point is acceptable for the initial implementation, but code inside it must be modular and maintainable.

Because Sheets is not a relational transactional database, multi-tab operations need:
- Script locks around critical writes.
- Batched reads/writes.
- Idempotency keys and duplicate prevention.
- An operation journal with BEGIN / MUTATION / COMMIT / FAILED / RECOVERY events.
- Compensating/reconciliation logic for partial failures.
- Schema/header validation and explicit schema versioning.
- Protected ranges/tabs and independent backups.

Do not promise production-grade multi-user transactions from Sheets.

### Frontend / PWA

The application should be responsive and mobile-first. An installable/offline PWA is **not yet approved or proven**. Verify service-worker scope, installability, asset caching and authentication on target Android/iOS devices. If the Apps Script origin prevents the required behaviour, host the frontend on a suitable HTTPS origin and retain Apps Script as the data API.

### Existing prototype technology

The approved register/history deliverables are standalone HTML/CSS/JS prototypes. The eventual production stack should be decided against the existing repository and dependencies before implementation. Do not rewrite approved prototypes into another framework just to change technology. Preserve the interaction contract and visual result.

## 7. UX principles and locked screens

### Global design rules

- Mobile-first and natural, understated application appearance.
- Light, Dark and System themes.
- Clean sans-serif hierarchy, restrained use of colour, clear focus/contrast.
- Interactive targets generally 44–48 CSS px where practical.
- Use rows/cards rather than tables on phones.
- Respect keyboard navigation and reduced-motion preferences.
- Confirmation for consequential actions (archive, void, issue invoice, teacher reassignment), not ordinary field edits.
- Auto-save feedback must be clear; never report server success before backend confirmation.
- Loading, empty, failed, stale/conflict, provisional and permission-denied states must be designed.
- Keep already approved screens intact. Do not redesign the Lesson Notes pop-up or Class Register.

### Teacher Screen 1 — Class Register (approved, locked)

Prototype: [`prototype/class-register.html`](../prototype/class-register.html), version v1.3.

- Compact header; no “Teacher Workspace” label.
- No teacher selector/name on the teacher's own register; login identity is implicit.
- Subject and Class Date selectors.
- Student count phrased as “N students”.
- Each row has immediate P (Present) and A (Absent) controls; no popup/confirmation.
- Tap the student row to open the Lesson Notes pop-up.
- Leave and Unmarked are selected inside that pop-up.
- Long-press enters multi-select mode.
- Bulk actions apply only to selected students.
- Copy/paste lesson details between students; paste fills empty fields by default and requires confirmation before replacing existing content.
- Individual student lesson records remain separate.
- Light, Dark and System themes.
- Auto-save and undo/redo in prototype; production audit semantics remain as described above.

### Lesson Notes pop-up (approved, locked)

The existing pop-up in the Class Register prototype is considered right. Keep its current appearance and interaction. It contains the student's lesson context, attendance status and the Topic Covered, Homework and Remarks fields. Do not invent a new full-page editor or redesign this pop-up without explicit approval.

### Teacher History (approved, locked)

Prototype: [`prototype/history-v1.2.html`](../prototype/history-v1.2.html), version v1.2.

- One History screen with two views: By date and By student.
- By date is the default: newest dates first, grouped chronologically; entries identify student, time, subject, attendance and a short topic preview.
- By student starts with a student selector. After selecting one student, show only that student's records, grouped by date.
- In By student, Present is the default filter; All records reveals Absent, Leave, Unmarked and provisional records with clear status labels.
- Multiple subjects/lessons on one date are grouped under the date heading.
- Tapping an entry opens full details using the established pop-up/detail interaction pattern.
- Teacher visibility is limited to records they are permitted to see; cross-teacher private notes are not exposed by default.

## 8. Main journeys

### Teacher records a lesson

1. Teacher opens the app and identity/role are resolved using the approved authentication mechanism.
2. Teacher sees their own relevant classes/register.
3. Teacher selects the correct subject/date/session context.
4. The correct student/enrolment is resolved; multiple eligible subjects require explicit selection.
5. Teacher records attendance and optional lesson information.
6. Backend validates role, enrolment, session and record versions.
7. UI reports a successful save only after backend confirmation.

The approved register/prototype intentionally streamlines the original multi-screen capture path. Do not reintroduce complexity from the earlier paper UX spec if the approved register already handles it.

### Administrator records on behalf of a teacher

1. Administrator selects the responsible teacher.
2. Selects student, enrolment and session/date.
3. System validates that the enrolment matches the responsible teacher and subject.
4. Administrator records the attendance and lesson details.
5. Store the administrator as actor and the selected teacher as responsible teacher.

### Administrator changes an enrolment teacher

1. Open student profile → Enrolments → selected enrolment.
2. Choose Change Teacher, successor teacher and effective date; record reason.
3. Review future sessions attached to the old version.
4. Flag affected sessions; do not move them automatically.
5. Confirm. Supersede the old version and create a successor version within the same group.
6. Preserve all historical sessions and records under the old version and expose the change in the audit timeline.

### Administrator assigns fees and issues an invoice

1. Open student profile → Fees.
2. Assign a student-level scheme and/or an enrolment-level scheme.
3. Show the additive combined expected amount and warn about possible double charging.
4. Set effective date and review agreed amount/frequency/charge basis.
5. Open invoice preview for the chosen period or eligible per-lesson charges.
6. Show each item and the fee assignment/session that sourced it.
7. Administrator confirms issue. Backend recalculates and invalidates stale previews.
8. Record invoice/items as a journaled operation. Payments and allocations are separate.

## 9. Delivery stages

| Stage | Work | Exit condition |
|---|---|---|
| 0 | Product requirements and scope | V1 product scope baseline frozen |
| 1 | Database architecture | 19-tab model reviewed |
| 2 | Continuity architecture | Versioning, reassignment and audit principles accepted |
| 3 | Technical blueprint v1.1 | Approved with conditions; release gates visible |
| 4 | Complete application UX | All teacher/admin screens and journeys reviewed |
| 4.5 | Interactive screen prototypes | Each screen approved and locked before moving on |
| 5 | Application foundation and design system | Shared shell, navigation, theme, auth boundary and reusable components agreed |
| 6 | Progressive feature implementation | Approved screens connected to validated services/data model |
| 7 | Testing, sync and deployment | Functional, security, data-integrity, mobile and recovery checks passed |

**Current position:** Stages 0–3 completed to their recorded approval status. Stage 4/4.5 is in progress. Production implementation has not begun and must not begin before UX sign-off.

## 10. Testing and release expectations

Before production use, test:
- Teacher/admin role enforcement on the backend.
- Student with multiple subjects/teachers and correct enrolment resolution.
- Present, Absent, Leave, Unmarked and provisional attendance.
- Individual and group participation records.
- Duplicate session/participation prevention.
- Teacher reassignment with old/future sessions.
- Stale-version conflicts and concurrent edits.
- Bulk edits affecting selected students only.
- Copy/paste fill-empty default and replacement confirmation.
- Invoice recalculation, duplicate Charge_Key prevention, partial payment allocation and reversals.
- Audit event completeness and failure/recovery journal.
- Backup/restore and schema migration.
- Android phone and iPad layouts; keyboard, touch, reduced-motion and themes.
- Real deployment authentication and PWA behaviour before making claims about either.

## 11. Definition of done for each UX screen

1. Discuss the screen's purpose and flow.
2. Confirm the key behaviour and any important edge cases.
3. Build an interactive prototype using the established Celestial design language.
4. Test navigation and all visible interactions; inspect JavaScript/runtime errors.
5. User tests on actual target device(s).
6. Incorporate feedback without modifying already locked screens.
7. User explicitly approves the screen.
8. Commit the approved prototype and screen specification to GitHub.
9. Update the build tracker and handoff before moving to the next screen.

A static diagram is not a substitute for the interactive prototype requested by the user.

## 12. Project continuation

The immediate next UX task is **Teacher Student Profile (T06)**. Teacher Student Directory v1 is approved and locked. Start by discussing the profile's purpose and permitted content, then produce a working interactive prototype. Do not skip directly to the next screen after a text mock-up. The existing Register, Lesson Notes pop-up and History are locked.

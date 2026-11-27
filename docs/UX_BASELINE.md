# Celestial — UX Baseline and Screen Inventory

This inventory is based on the Complete Application UX v1.0, then updated with the user's later screen-by-screen decisions. The approved interactive prototypes take precedence over earlier wireframes when they intentionally streamline a workflow.

## Teacher workspace — original inventory and current treatment

| ID | UX v1.0 screen | Current status / treatment |
|---|---|---|
| T01 | Home / Today | Pending |
| T02 | Record lesson — context | Streamlined into the approved Class Register context; review if any separate step remains useful |
| T03 | Lesson record editor | Implemented as the approved Class Register + integrated Lesson Notes pop-up |
| T04 | Save result / session detail | To reconcile; avoid duplicate confirmation screens if status can be shown in the current workflow |
| T05 | Student directory | Approved and locked as Teacher Student Directory v1; see `docs/locked-student-directory.md` |
| T06 | Student profile — teacher view | Next screen to prototype |
| T07 | History — by date | Combined into approved History screen, default mode |
| T08 | History — by student | Combined into approved History screen, select a student then inspect that student's timeline |
| T09 | Lesson detail/edit | Reuse existing detail/pop-up pattern; editing and change-history permissions require confirmation |
| T10 | Profile & preferences | Pending |

## Administrator workspace — 17 screens

| ID | Screen | Main purpose |
|---|---|---|
| A01 | School overview | Students, teachers, recent lessons, provisional items and finance exceptions |
| A02 | Student directory | Search, filter, create, archive and open student |
| A03 | Student create/edit | Student master and guardians/contact details |
| A04 | Student profile | Overview, guardians, enrolments, lessons, attendance, fees, invoices, payments and changes |
| A05 | Enrolment editor | Create, Change Teacher, end/re-enrol and fee mode |
| A06 | Teacher directory/profile | Staff records, app-user association and workload |
| A07 | Subject catalogue | Create/edit/archive subjects |
| A08 | Session manager | List/calendar, create, complete, cancel, reschedule and participants |
| A09 | Session detail | Attendance and lesson records by participation |
| A10 | Finance overview | Receivables, issued invoices, payments, previews and exceptions |
| A11 | Fee schemes | Reusable templates and charge basis |
| A12 | Student financial setup | Student-level and enrolment-level assignments and effective dates |
| A13 | Invoice preview/detail | Recalculate, compare, issue and void/reissue |
| A14 | Payments | Record receipts, partial allocations, unallocated balance and reverse allocation |
| A15 | Reports | Date, student, teacher, subject and financial filters |
| A16 | Settings | Timezone, currency, defaults, schema status and app preferences |
| A17 | Audit & change history | Search changes, compare versions, inspect operations and archive/restore |

## Shared UX rules

- One application shell and one data model; role determines navigation, actions and visibility.
- Teacher selector is fixed/implicit for a teacher account; administrator may select the responsible teacher.
- Student selector is searchable by name or ID and displays relevant enrolment context.
- Require explicit subject/enrolment choice if a student has multiple eligible enrolments.
- Reuse a matching existing session where possible; do not create duplicate occurrences without review.
- School-local dates are required; future attendance is provisional.
- Use inline labels, clear optional/required markers and field-level validation.
- Use date-only controls for dates, time-only controls for times, and the configured currency for money.
- Confirm consequential actions, not ordinary edits.
- History is read-only by default; deliberate Edit action opens the current record with values preloaded.
- If data changed elsewhere, offer reload/compare rather than silent overwrite.
- Provisional status must be explicit; never display as confirmed presence.
- Teacher history must not expose other teachers' private notes by default until visibility policy is resolved.

## Current approved prototypes

- Class Register v1.3: `prototype/class-register.html`
- History v1.2: `prototype/history-v1.2.html`
- Lesson Notes pop-up: integrated into the Class Register; do not redesign.

## Locked Teacher Student Directory

The T05 Student Directory v1 prototype is approved and locked: `prototype/teacher-student-directory-v1.html`. Its detailed behaviour and prototype limitations are recorded in `docs/locked-student-directory.md`. The next teacher screen is T06 Student Profile — teacher view.

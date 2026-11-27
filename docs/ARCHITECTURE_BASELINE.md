# Celestial — Architecture Baseline

**Reference:** Technical Blueprint v1.1  
**Approval:** Approved with conditions for design and implementation planning.  
**Not approval for:** live production student/financial data, final authentication, or a proven PWA deployment.

## 1. Logical workbook/table structure

The approved data model has 19 tabs:

1. `App_Users`
2. `Teachers`
3. `Students`
4. `Guardians`
5. `Student_Guardians`
6. `Subjects`
7. `Enrolments`
8. `Sessions`
9. `Session_Enrolments`
10. `Attendance`
11. `Lesson_Records`
12. `Fee_Schemes`
13. `Fee_Assignments`
14. `Invoices`
15. `Invoice_Items`
16. `Payments`
17. `Payment_Allocations`
18. `Settings`
19. `Audit_Log`

## 2. Relational invariants

- Student_ID is permanent; a student is not duplicated for each subject or teacher.
- One student can have many enrolments across subjects and teachers.
- Enrolments are effective-dated and versioned.
- `Enrolment_Group_ID` represents the logical ongoing relationship; a teacher change creates a successor `Enrolment_ID` within that group.
- End & Re-enrol creates a new logical group.
- A Session represents one occurrence. `Session_Enrolments` represents individual participation.
- Attendance and Lesson_Records are stored per participation; group classes do not create one shared student note.
- Fee schemes are templates; assignments are effective-dated agreements.
- A student-level fee and an enrolment-level fee can be additive; the application must show the combined impact.
- An Invoice is distinct from Invoice_Items.
- A Payment is distinct from Payment_Allocations.
- Audit events describe changes and related operation state.

## 3. Teacher reassignment

User-visible flow: open the enrolment → Change Teacher → choose successor teacher and effective date → enter reason → review future sessions → confirm.

Data behaviour:
- Close/supersede the old enrolment version.
- Create a successor Enrolment_ID within the same Enrolment_Group_ID.
- Preserve past sessions and lesson records under the old version.
- Flag future sessions attached to the old version for review.
- Do not silently move future sessions or historical records.

End & Re-enrol is separate and creates a new Enrolment_Group_ID.

## 4. Session, attendance and lesson data

- Sessions may support individual or group classes; whether group creation is enabled in V1 remains an open decision.
- Each participant is linked through Session_Enrolments.
- Attendance status is Present, Absent, Leave or Unmarked; future entries may be Provisional.
- Unmarked must not be assumed to mean Present.
- Lesson notes include Topic Covered, Homework and Remarks.
- Attendance notes are distinct from general lesson remarks.
- A future-dated attendance record must not be shown or billed as confirmed presence.

## 5. Fees and finance

- Fee scheme frequencies in the baseline include MONTHLY, PER_LESSON, WEEKLY, QUARTERLY, ANNUAL, ONE_TIME and CUSTOM.
- Fee assignments carry effective dates and agreed amounts.
- Charge basis controls eligibility. The blueprint distinguishes SESSION_CONDUCTED from STUDENT_PRESENT.
- Cancelled/rescheduled source sessions are not charged automatically.
- Unconfirmed future/provisional participation is not charged.
- PER_LESSON billing needs duplicate prevention, including a unique Charge_Key.
- Preview is not issue. Issue requires administrator confirmation and backend recalculation.
- Payment receipts and their invoice allocations are separate records.
- Rules for GST, refunds, credit notes, advances and no-shows remain open.

## 6. Audit and operation journal

Operation states in the technical baseline:
- BEGIN — append operation identity, actor, entities and STARTED state.
- MUTATION — append before/after snapshots and sequence.
- COMMIT — append terminal event only after writes and validation succeed.
- FAILED — record failure and affected operation.
- RECOVERY — record compensating/reconciliation work and final state.
- MIGRATION — record schema version, operation and outcome.

Use Operation_ID and Change_Set_ID to connect related mutations. Record actor, timestamp, entity, version, before/after values and reason where applicable.

## 7. Apps Script / Sheets reliability constraints

- Use a script lock around critical multi-tab operations.
- Batch operations where practical.
- Use idempotency keys and duplicate detection.
- Journal multi-step mutations and provide recovery/compensation.
- Validate schema version and header signatures.
- Protect sensitive tabs and ranges; restrict workbook editors.
- Maintain independent backups and rehearse restore.
- Treat Apps Script identity as deployment-dependent; prove the selected authentication mode in the real deployment.
- Application append-only rules do not stop a spreadsheet owner/editor from manually changing cells. The log is not cryptographically immutable.

## 8. Proposed service/API operations in blueprint

- `getAppBootstrap`
- `listStudents`
- `getStudentProfile`
- `saveStudent`
- `saveTeacher`
- `saveEnrolment`
- `reassignEnrolmentTeacher`
- `endAndReenrol`
- `createSession`
- `saveSessionParticipants`
- `saveAttendance`
- `saveLessonRecord`
- `previewInvoice`
- `issueInvoice`
- `recordPayment`
- `allocatePayment`
- `getDateHistory`
- `getStudentHistory`
- `getAuditHistory`
- `archiveRecord` / `restoreRecord`
- `runSchemaMigration`

Backend checks must enforce role, entity scope, version and state rules. UI visibility alone is not sufficient.

## 9. Approved implementation direction

A responsive Apps Script web application is the conditional first-release path. Before labelling it an installable/offline PWA, prove installation, service-worker scope, offline asset caching and authentication on actual target devices. If the Apps Script origin does not permit the required PWA behaviour, host the frontend separately on an appropriate HTTPS origin and retain Apps Script as the data API.

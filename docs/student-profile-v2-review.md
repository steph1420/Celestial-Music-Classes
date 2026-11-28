# Teacher Student Profile — v2 Review Specification

**Screen:** T06 — Teacher Student Profile  
**Previous prototype:** v1 (prototype/teacher-student-profile-v1.html)  
**Current prototype:** prototype/teacher-student-profile-v2.html  
**Status:** 🔒 Approved and locked by user on 28 November 2026.

Locked specification: `docs/locked-student-profile-v2.md`.

## Purpose and layout
One scrollable, teacher-facing student profile. T05 opens it directly when a student row is selected. The profile header contains optional photo/initials, student name, class, calculated age, status, Student ID and the single **Edit profile** action.

Sections, in order:
1. Personal Details
2. Parent / Guardian — rendered only when enabled for this child
3. Enrolments — teacher's own enrolments first; other subjects read-only
4. Attendance — summary, recent records and History link
5. Additional Notes — one continuous multiline note, shared with teachers assigned to the student
6. Recent changes / audit trail

No quick overview modal, no Learning Overview, no finance information.

## Unified editing
- Exactly one Edit profile button opens one full-page edit mode.
- Personal details, optional photo URL, guardian setting/details and Additional Notes are edited in the same form.
- Save and Cancel appear at the end of the form (not sticky).
- Nothing is persisted until Save. Cancel discards the draft.
- One audit entry is recorded for a profile save.

## Parent / Guardian conditional behaviour
- Edit form includes a checkbox: **Include parent / guardian information for this student**.
- When unchecked, the read-only profile omits the Parent / Guardian section entirely; no empty card, heading or placeholder appears.
- Unchecking hides the information but retains the child's guardian links and shared records. Re-enabling restores the existing information.
- When enabled, at least one guardian must be present and every listed guardian must have a phone number. Phone is the only mandatory guardian field. Name, relationship, separate WhatsApp number and email are optional.
- WhatsApp uses the phone number if no separate WhatsApp number is supplied. Email contact action appears only when an email exists.
- Multiple guardians are supported; one can be designated primary for this child.
- Guardian contact fields remain on the shared Guardian record; relationship and primary designation remain on the child–guardian link. Shared edits therefore affect siblings that use the same guardian record.
- Removing a guardian from the child during editing removes only that child's link on Save. Shared guardian records are retained while any other child remains linked.

## Additional Notes
- One multiline field, separate from lesson-specific notes.
- Shared with teachers assigned to the student.
- Rendered as a section on the profile; empty state says no additional notes yet.
- Stored on the student record in this prototype.

## Preserved decisions
- Optional profile photo.
- Student fields: DOB, calculated age, address, student phone, school and class/grade.
- Limited teacher editing; student name, status and enrolments are not editable here.
- Teacher sees own enrolments first and other subjects as read-only.
- No Learning Overview.
- Attendance summary.
- Contact actions: Call, WhatsApp, SMS and optional Email.
- Explicit Save/Cancel and audit trail.
- Backend permissions remain authoritative in production.

## Prototype limitations
- Illustrative data and browser-local persistence only.
- No production database, authentication, multi-user sync, file upload or authoritative audit service.
- Shared guardian/notes behaviour is demonstrated in the local prototype data only; production sharing and access must be enforced by the backend.

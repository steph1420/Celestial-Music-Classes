# Teacher Student Profile — Locked Specification

**Screen ID:** T06  
**Approved prototype:** prototype/teacher-student-profile-v2.html  
**Version:** v2  
**Status:** Approved and locked by user on 28 November 2026

## Purpose and navigation
Provide the teacher with the complete permitted profile for the student selected from T05. T05 opens the profile directly using the student's stable Student_ID. No quick overview modal is used.

## Layout
- One vertically scrollable profile.
- Optional profile photo, with initials fallback.
- Header shows student name, class, calculated age, record status, Student_ID and one **Edit profile** action.
- Sections, in order:
  1. Personal Details
  2. Parent / Guardian — only when enabled for this child
  3. Enrolments
  4. Attendance
  5. Additional Notes
  6. Recent changes / audit trail
- No Learning Overview section.
- No fee, invoice or payment information.

## Personal details
- Display date of birth, calculated age, home address, student phone, school and class/grade.
- Teacher editing is limited to these permitted student details and optional profile photo URL.
- Student name, record status and enrolments are not editable from this screen.
- Age is calculated from date of birth.

## Parent / Guardian
- A checkbox in Edit profile controls **Include parent / guardian information for this student**.
- When unchecked, the read-only profile omits the entire Parent / Guardian section. Do not show an empty heading, card or message.
- Unchecking hides the section but retains the child's guardian links and shared guardian records. Re-enabling restores existing information.
- When enabled, at least one guardian must be linked and every listed guardian must have a phone number. Phone is the only required guardian field.
- Guardian name, relationship, separate WhatsApp number and email are optional.
- Multiple guardians are supported; one may be designated primary for this child.
- WhatsApp uses the phone number if a separate WhatsApp number is absent. Email action appears only when an email address is supplied.
- Guardian contact details are shared Guardian-record fields; relationship and primary designation belong to the child–guardian link. Shared contact edits affect other linked students.
- Removing a guardian during editing removes the link for this child on Save. Retain a shared Guardian record while another student remains linked.

## Enrolments
- Show the signed-in teacher's enrolments first.
- Show the student's other subjects separately.

## Attendance
- Show attendance summary counts and recent records.
- Link to the existing History screen.

## Additional Notes
- One continuous multiline note, separate from lesson-specific Topic Covered, Homework and Remarks.
- Shared with teachers assigned to the student.
- Show the section even when no note has been entered, with a simple empty state.

## Editing and audit
- Exactly one Edit profile action opens one full-page edit form.
- Personal details, parent/guardian setting and data, and Additional Notes are edited in the same form.
- Save and Cancel appear at the end of the form; they are not sticky.
- No changes persist until Save. Cancel discards the draft.
- Profile saves are recorded in the prototype audit display.
- Production audit records must be created and enforced by the backend.

## Contact actions
- Call, WhatsApp and SMS when a usable phone number is present.
- WhatsApp uses the separate WhatsApp number if supplied, otherwise the phone number.
- Email appears only when an email address is supplied.

## Data and permission boundaries
- Prototype records and local persistence are illustrative only.
- Backend permissions determine actual teacher visibility and edit rights.
- Shared notes are visible only to teachers assigned to the student.
- No finance data appears in the teacher profile.
- Browser local storage is not a production database or multi-user synchronisation.

## Preservation
T06 v2 is approved and locked. Any future change requires a deliberate versioned revision. Preserve the earlier v1 review file as a historical artefact.

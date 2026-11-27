# Teacher Student Profile — Review Specification

**Screen ID:** T06  
**Prototype:** `prototype/teacher-student-profile-v1.html`  
**Version:** v1  
**Status:** 🟡 Prototype submitted for user review; not approved or locked.

## Purpose
Provide a teacher with a useful, permission-limited profile for a student selected from My Students. This is not the administrator's complete student master or finance profile.

## Layout and sections
- One vertically scrollable page with separated sections.
- Optional profile photo; use initials when no photo is supplied.
- Header shows student name, class, calculated age, status and student identifier.
- Personal details: date of birth, calculated age, home address, student phone, school and class/grade.
- Parent / Guardian cards.
- Enrolments: the signed-in teacher's own enrolments first; other subjects shown separately as a read-only summary.
- No Learning Overview section.
- Attendance summary counts and recent attendance records, with a link to the existing History screen.
- Recent changes / audit trail.
- No fees, invoices or payments.

## Teacher editing permissions
- Limited student editing: date of birth, address, student phone, school and class/grade. Age is calculated from date of birth. Student name, record status and enrolments are not editable from this screen.
- Guardian management: teachers may add, edit, remove and unlink guardians.
- Shared guardian contact data: name, phone, WhatsApp and email belong to the shared Guardian record. Updating these details updates every linked student's profile.
- Relationship and primary-contact designation belong to the student–guardian relationship, so they can differ between siblings.
- Removing a guardian from one student removes only that link. The shared Guardian record is deleted only when no student remains linked.
- Explicit Save / Cancel for edits.
- Record who changed what and when in an audit trail.
- Cross-teacher lesson notes are visible only when explicitly marked shared. Private/unshared notes remain hidden.
- Backend permissions remain authoritative in production.

## Guardian contact shortcuts
- Call and SMS use the guardian phone number when present.
- WhatsApp uses the separate WhatsApp number when present, otherwise falls back to the phone number.
- Email shortcut appears only when an email address is present.

## Prototype behaviour and limitations
- Illustrative seed records only.
- Browser-local persistence only; no production database, authentication, multi-user sync or real backend audit log.
- Contact shortcuts use the device/browser's configured handlers.
- Optional profile photo is represented by an image URL in this demo; production upload/storage behaviour remains to be designed.
- The prototype's demo audit trail is local and illustrative, not an authoritative audit record.
- The existing Register, History and locked Student Directory prototypes must not be redesigned or overwritten.

## User decisions
All listed choices above were supplied by the user on 27 November 2026. The screen remains open for prototype review; do not mark it approved until the user explicitly says so.

# Teacher Student Directory — Locked Specification

**Screen ID:** T05  
**Prototype:** `prototype/teacher-student-directory-v1.html`  
**Version:** v1  
**Status:** 🔒 Approved and locked by user on 27 November 2026

## Purpose
Give a teacher a simple, searchable view of the students in their permitted teaching roster, with a single directory entry per student even when that student has multiple subject enrolments.

## Locked interaction and presentation
- Reuse the established Celestial application shell, navigation drawer, theme treatment, modal and toast patterns.
- Screen title: **My Students**.
- Show the roster count, active-student count and number of represented subjects.
- Search students by name.
- Filter by subject: All subjects, Piano, Vocals or Guitar.
- Filter by student record status: Active (default), All students or Inactive.
- Show each matching student once, with their name, subject-enrolment chips and record status.
- Selecting a student opens the **Student overview** modal.
- The overview shows student name, record status and subject enrolments. It indicates that the full student profile is a separate screen.
- Empty search/filter results provide a clear-filter action.
- Add-student action opens a modal with student name, one or more subject selections and Active/Inactive record status. A name already present in the demo roster is rejected.
- Support Light, Dark and System appearance preferences.
- Keep the mobile layout compact and touch-friendly.

## Data and permission boundaries
- The prototype uses illustrative seed data only.
- Directory entries represent students, not enrolments: a student with several subject enrolments appears once.
- The prototype's add-student interaction and browser-local persistence are demonstration behaviour only. They do not grant teachers production permission to create student master records or enrolments.
- Production roster contents, visible fields and actions must be enforced by backend teacher permissions. The teacher must not see fee amounts, invoices or payments.
- Browser local storage is not a production database and does not provide multi-user synchronisation.
- Student profile navigation is intentionally not implemented as a production destination yet; T06 is the next screen to design.

## Preservation
This screen is approved and locked. Do not redesign or overwrite the prototype while implementing later screens. Any requested change must be treated as a deliberate versioned revision, preserving this approved baseline.

## Validation record
- JavaScript syntax check passed.
- Simulated interaction checks passed for subject/status filtering, one-record-per-student enrolments, student overview, adding a demo student, undo and redo.
- These were code/simulated interaction checks, not a live-browser visual test. User reviewed the prototype and explicitly approved it.

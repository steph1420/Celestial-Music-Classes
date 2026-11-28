# Teacher Student Directory — Locked Specification

**Screen ID:** T05  
**Approved prototype:** prototype/teacher-student-directory-v1.2.html  
**Version:** v1.2  
**Status:** Approved and locked by user on 28 November 2026

## Purpose
Give teachers a searchable view of their permitted student roster. Each student appears once, even when enrolled in multiple subjects. Selecting a student opens that student's profile directly.

## Layout and behaviour
- Reuse the established Celestial shell, drawer, theme, typography and interaction patterns.
- Screen title: My Students.
- Show roster count, active-student count and represented subjects.
- Search by student name.
- Subject filters: All subjects, Piano, Vocals and Guitar.
- Status filters: Active (default), All students and Inactive.
- Each roster entry shows student name, subject enrolment chips and record status.
- Tapping a student row opens the matching T06 Student Profile directly. No Student overview modal or intermediate profile button.
- Pass the selected stable Student_ID to T06 using the studentId query parameter.
- Empty search/filter results offer a clear-filter action.
- Add-student flow captures name, one or more subjects and record status; duplicate names in the demo roster are rejected.
- Light, Dark and System appearance preferences.
- Compact, touch-friendly mobile layout.

## Student identity and navigation
- Demo identifiers use the STU-0001 format.
- Existing browser-local legacy IDs are migrated to stable demo IDs.
- Newly added students receive the next available demo ID.
- T06 must resolve exactly the ID supplied by T05. Unknown IDs display a not-found state; never silently open another student's profile.
- The locked T05 v1 and superseded v1.1 files remain preserved as historical baselines.

## Data and permission boundaries
- Seed records are illustrative.
- A student with multiple enrolments appears once in the directory.
- Adding students and browser-local persistence are prototype behaviours, not production teacher permissions.
- Production roster contents and actions must be enforced by backend permissions.
- Teacher views must not expose fee amounts, invoices or payments.
- Browser local storage is not a production database or multi-user synchronisation.

## Preservation
T05 v1.2 is approved and locked. Do not redesign or overwrite it while implementing later screens. Any future change requires a deliberate versioned revision. Preserve the original v1 baseline.

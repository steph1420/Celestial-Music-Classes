# Teacher Student Directory — v1.2 Review Notes

**Screen:** T05 — My Students  
**Locked baseline:** v1 (prototype/teacher-student-directory-v1.html)  
**Prior refinement:** v1.1  
**Current prototype:** prototype/teacher-student-directory-v1.2.html  
**Status:** 🔒 Approved and locked by user on 28 November 2026.

Locked specification: `docs/locked-student-directory-v1.2.md`.

## Changes
- Selecting a student row opens that student's T06 profile directly.
- Removed the Student overview modal, its Student ID summary and the intermediate profile button.
- Passes the selected stable Student ID through the studentId query parameter.
- Retains search, subject/status filters, roster display, adding students, local persistence and stable ID migration.
- Newly added students receive a stable demo ID and are initialized with parent information disabled and an empty Additional Notes field.
- The locked T05 v1 baseline and the earlier v1.1 review file remain preserved.

## Integration
- T05 v1.2 publishes as the directory landing page.
- T06 v2 publishes as student-profile.html.
- T06 resolves the exact ID passed by T05; invalid IDs show a not-found state rather than opening another student.

## Limitations
- Illustrative records and browser-local persistence only.
- No production authentication, database, multi-user sync or authoritative permission enforcement.

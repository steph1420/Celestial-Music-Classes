# Teacher Student Directory — v1.1 Review Notes

**Screen:** T05 — My Students  
**Baseline:** v1, approved and locked on 27 November 2026  
**Refinement:** v1.1  
**Prototype:** `prototype/teacher-student-directory-v1.1.html`  
**Status:** Implemented for review; v1.1 is not yet locked.

## Why this refinement exists
The original overview modal did not provide a route into the newly created T06 Student Profile. The earlier demo also used separate temporary IDs in the directory and profile, so a selected directory student could not reliably resolve to the matching profile.

## v1.1 changes
- The Student overview modal now displays the selected student's stable Student ID.
- The modal includes **Open full student profile**.
- The action passes that exact ID as the `studentId` query parameter to `student-profile.html`.
- T05 demo records use stable IDs in the form `STU-0001`, `STU-0002`, and so on.
- Existing T05 browser-local records with earlier IDs such as `d1` are migrated to the corresponding stable ID when v1.1 loads, and the migrated roster is saved.
- Newly added demo students receive the next available stable Student ID.
- T06 uses the same stable IDs and matching seed names for all eight original demo students.
- When a newly added directory student has no pre-seeded profile, T06 creates a blank illustrative profile from that exact directory record and its enrolments.
- An unknown Student ID shows a not-found state; it must never silently open the first student's profile.
- Original `prototype/teacher-student-directory-v1.html` remains untouched as the locked v1 baseline.

## Integration contract
1. A directory row is selected by its permanent Student ID.
2. The overview modal displays the same ID and passes it unchanged to T06.
3. T06 reads the ID from the URL and resolves the matching profile.
4. If the profile does not yet exist in the demo profile store, it is derived from the matching directory record.
5. Missing/invalid IDs do not fall back to an unrelated student.

## Prototype limitations
- Student records remain illustrative.
- Browser local storage is local to this browser and is not a production database or multi-user sync.
- The stable IDs are demo identifiers; the eventual backend must supply permanent Student_ID values.
- T05 v1.1 and its T06 navigation are subject to user review and are not yet locked.

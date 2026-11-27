# Locked UX Specification — Teacher History

**Status:** Approved and locked  
**Prototype:** `prototype/history-v1.2.html`  
**Approval:** User tested the v1.2 prototype and said it looks perfect.

## Structure

One History screen, with two views:
- By date
- By student

**By date is the default opening view.**

## By date

- Chronological, newest first.
- Group records under date headings.
- Each entry identifies student, time, subject and attendance.
- Show a useful short topic preview when available.
- Tap an entry to open full lesson/attendance details.

## By student

- Show a student selector first.
- Do not list all students with repeated lesson cards before a selection.
- Once selected, show only that student's history.
- Group records by date; multiple subjects/lessons on one date share the date heading.
- Default filter: **Present**.
- **All records** includes Absent, Leave, Unmarked and provisional records with unmistakable status labels.
- Tap a lesson to open its full details using the established detail/pop-up interaction.

## Permissions and history rules

- Teacher view includes only records the teacher is permitted to access.
- Do not expose another teacher's private notes by default while AUTH-02 remains unresolved.
- History is read-only by default. Editing is a deliberate permitted action.
- Corrections must create traceable changes in production.
- Provisional records must never be presented as confirmed attendance.
- Unmarked is not equivalent to Present.

## Visual / implementation rule

Use the approved History v1.2 prototype as the visual baseline. Do not redesign it after approval. Future refinements should be narrowly scoped and explicitly requested.

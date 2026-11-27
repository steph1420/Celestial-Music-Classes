# Locked UX Specification — Screen 1: Class Register

**Status:** Approved and locked  
**Prototype version:** v1.3

## Purpose
A teacher can quickly mark class attendance and open an individual student's lesson details without navigating through a complicated workflow.

## Layout and visual direction
- Mobile-first.
- Natural, understated application design; avoid excessive gradients, glows, ornamental AI-dashboard motifs and oversized branding.
- Light and Dark themes, plus System preference.
- Compact header.
- Do not display “Teacher Workspace”.
- Do not display the teacher's name or a teacher selector on the teacher's own register.
- Subject and Class date are the register context selectors.
- Display the count as “N students”.

## Attendance interaction
- Each student row exposes two quick controls:
  - **P** — immediately marks Present.
  - **A** — immediately marks Absent.
- P and A are direct actions: no popup and no confirmation dialog.
- The student row itself opens that student's lesson notes panel.
- Leave and Unmarked are selected inside the lesson notes panel, not as additional quick buttons on the register.

## Multi-select and bulk actions
- Long-press a student's row to enter multi-select mode.
- Bulk actions affect only selected students.
- Common lesson details create/update individual student lesson records, not one shared record.
- Existing individual values are protected by default; common notes fill empty fields unless replacement is explicitly confirmed.

## Persistence and history
- Automatically save register changes in the prototype's local browser storage.
- Keep register undo/redo separate from general application history.
- Undo/redo must not erase the audit trail in the eventual production implementation.
- Navigation history is distinct from data-change history.

## Scope boundary
This approval locks the Class Register UX only. It does not approve the Lesson Notes panel, production backend, authentication, Google Sheets integration or application-wide implementation.

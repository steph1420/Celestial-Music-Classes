# Celestial — Music School Management

Celestial is a music-school management application. This repository preserves the approved Class Register screen as the first locked UX baseline.

## Current status

- Screen 1 — Class Register: **approved and locked**
- Screen 2 — Lesson Notes: next screen to design
- The current prototype is browser-only, uses sample data and local storage, and is not the production application.
- Production architecture, authentication, backend sync and deployment remain separate implementation stages.

## Approved Class Register behaviour

- Mobile-first, natural application UI; avoid an AI-dashboard aesthetic.
- Light, Dark and System theme preferences.
- Compact header; no “Teacher Workspace” label.
- No teacher name or teacher selector on the teacher's own register. The logged-in teacher identity is implicit.
- Subject and Class date selectors.
- Student count is labelled “N students”, not “N enrolled”.
- Each student row has immediate **P** (Present) and **A** (Absent) actions. Neither opens a popup.
- Tapping the student row opens the lesson notes panel.
- Leave and Unmarked are handled inside the lesson notes panel.
- Long-press selects multiple students; bulk attendance and common lesson-note actions are supported.
- Automatic local saving; register undo/redo is separate from general application history.
- Common lesson details fill empty fields by default and preserve existing individual notes.
- Each student's lesson record remains individual.

## Design principle

**Simple by default. Powerful underneath.**

Keep everyday teacher workflows fast and familiar. Preserve the richer data model and auditability beneath the interface without exposing unnecessary complexity.

## Prototype limitations

The prototype uses illustrative sample records and browser-local storage. It is not connected to Google Sheets, Apps Script or a production database. Local storage is not a substitute for server persistence, multi-user concurrency, authentication or a durable audit log.

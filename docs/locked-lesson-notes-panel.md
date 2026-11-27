# Locked UX Specification — Lesson Notes Pop-up

**Status:** Approved and locked  
**Host screen:** Class Register v1.3  
**Approval:** User explicitly said the current pop-up is perfect and does not need redesign.

## Rule

Preserve the current Lesson Notes pop-up appearance and interaction. Do not reinvent it, replace it with a full-screen page, introduce a new editor pattern, or make unnecessary changes.

## Context and fields

- Opened by tapping a student row in the Class Register.
- Shows the selected student's lesson context (student, subject/date and related context already available in the current prototype).
- Attendance options include Present, Absent, Leave and Unmarked in the pop-up workflow; P/A remain quick actions on the register.
- Lesson fields: Topic Covered, Homework and Remarks.
- Copy/paste lesson detail behaviour remains consistent with the approved register specification.
- Auto-save and feedback follow the existing prototype's interaction model; production must report server-confirmed persistence accurately.

## Scope

This lock preserves the pop-up's current UI. It does not resolve production authentication, server persistence, cross-teacher visibility, edit permissions or audit policy. Those remain governed by the architecture and open-decision documents.

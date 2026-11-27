# Celestial — Music School Management

**Guiding principle: Simple by default. Powerful underneath.**

Celestial is a mobile-first music-school management application for teachers and administrators. It is being designed screen by screen, with interactive prototypes reviewed and approved before production implementation.

## Project status

- Product scope: baseline frozen.
- Data architecture: 19-tab relational model approved with operational conditions.
- Technical blueprint v1.1: approved with conditions.
- UX: in screen-by-screen review and prototype validation.
- **Teacher Screen 1 — Class Register: approved and locked (prototype v1.3).**
- **Lesson Notes pop-up: existing design approved and locked.**
- **Teacher History — By date and By student: approved and locked (prototype v1.2).**
- **Teacher Student Directory: approved and locked (prototype v1).**
- **Next UX screen: Teacher Student Profile (T06).**
- Production implementation, backend sync, authentication and deployment: not yet authorised/completed.

## Start here

1. [Project plan](docs/PROJECT_PLAN.md) — product scope, architecture, workflows, implementation stages and release strategy.
2. [Build tracker](docs/BUILD_TRACKER.md) — current status of every planned teacher and administrator screen.
3. [Next-chat handoff](docs/HANDOFF_NEXT_CHAT.md) — exact continuation point and instructions for resuming work.
4. [Decision log](docs/DECISION_LOG.md) — locked decisions and constraints.
5. [Open decisions](docs/OPEN_DECISIONS.md) — policies that must be resolved before affected production features.
6. [Architecture baseline](docs/ARCHITECTURE_BASELINE.md) — 19-tab data model and technical invariants.
7. [UX baseline](docs/UX_BASELINE.md) — teacher/admin screen inventory and workflow rules.

## Approved interactive prototypes

- [Class Register v1.3](prototype/class-register.html)
- [History v1.2](prototype/history-v1.2.html)
- [Teacher Student Directory v1](prototype/teacher-student-directory-v1.html)
- [Teacher Student Directory locked specification](docs/locked-student-directory.md)
- [Teacher Student Directory v1](prototype/teacher-student-directory-v1.html)
- [Teacher Student Directory locked specification](docs/locked-student-directory.md)

The Lesson Notes pop-up is part of the approved Class Register experience. Keep its existing appearance and interaction; do not redesign it.

## Non-negotiable product principles

- One shared application and data model with role-aware teacher and administrator workspaces.
- One permanent Student record; a student can have multiple subject/teacher enrolments.
- One class occurrence is a Session; each student's participation, attendance and lesson record remain individual.
- Current records should be easy to use; important changes remain traceable.
- No silent destructive edits to historical financial or teaching records. Archive/deactivate rather than hard-delete referenced records.
- Backend permission checks are authoritative; hiding a UI control is not security.
- Existing approved screens are locked. Extend the application without rebuilding or replacing them.
- Keep the phone experience as the reference; tablet and desktop adapt the same workflows.
- Avoid an AI-dashboard aesthetic, excess decoration and unnecessary complexity.

## Prototype limitations

The approved HTML prototypes are interactive UI demonstrations using illustrative data and browser-local persistence. They are not connected to the production database, do not establish multi-user sync or authentication, and must not be treated as production code.

See the [handoff document](docs/HANDOFF_NEXT_CHAT.md) before continuing work.

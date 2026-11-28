# Celestial — Build Tracker

**Last updated:** 27 November 2026  
**Current phase:** UX design + interactive prototype approval  
**Next item:** Review T05 v1.2 direct navigation and T06 v2 profile

Legend: ✅ complete/approved · 🔒 approved and locked · 🟡 in progress · ⬜ not started · ⏸ blocked by policy/decision

## 1. Stage tracker

| Stage | Workstream | Status | Notes |
|---:|---|---|---|
| 0 | Product requirements and scope | ✅ | V1 scope baseline frozen |
| 1 | Database architecture | ✅ | Approved 19-tab model |
| 2 | Continuity architecture | ✅ | Effective dating, successor enrolments, traceability |
| 3 | Technical blueprint v1.1 | ✅ | Approved with conditions; open gates remain |
| 4 | Complete application UX | 🟡 | Screen-by-screen refinement; earlier UX v1.0 is a baseline, not final screen approval |
| 4.5 | Interactive prototypes and user approval | 🟡 | Register, Notes, History and Student Directory approved |
| 5 | Application foundation/design system | ⬜ | Wait for UX sign-off |
| 6 | Feature implementation | ⬜ | Production code not yet authorised |
| 7 | Testing, sync and deployment | ⬜ | Backend/auth/PWA decisions and implementation pending |

## 2. Teacher workspace tracker

| ID | Screen / flow | Status | Current decision / next action |
|---|---|---|---|
| T01 | Home / Today | ⬜ | Design after core daily workflows; keep operational, not an analytics dashboard |
| T02 | Record lesson — context | 🔄 | Original multi-screen concept streamlined into Class Register. Reconcile remaining context selection during UX review; do not reintroduce unnecessary steps |
| T03 | Lesson capture / Class Register | 🔒 | Class Register v1.3 approved and locked |
| T03a | Lesson Notes pop-up | 🔒 | Existing pop-up design approved; preserve it exactly unless user asks to change it |
| T04 | Save result / session detail | 🔄 | Determine which confirmation/status details are integrated into register/history versus needing a separate view |
| T05 | Student Directory | 🔒 / 🟡 | v1 remains approved and locked; v1.2 removes overview and opens T06 directly. See `docs/student-directory-v1.2-review.md` |
| T06 | Student Profile — teacher view | 🟡 IN PROGRESS | Revised conditional guardian fields, unified editing and shared Additional Notes; prototype `prototype/teacher-student-profile-v2.html` awaiting review |
| T07 | History — by date | 🔒 | Combined History screen v1.2; default view |
| T08 | History — by student | 🔒 | Combined History screen v1.2; select a student, then show that student's dates; Present default, All records switch |
| T09 | Lesson detail / edit | 🔄 | Detail pop-up pattern established; editing permissions/history behaviour to be confirmed in context |
| T10 | Profile & preferences | ⬜ | Basic identity/preferences/sign-out; avoid duplicating admin teacher management |

Notes:
- T07 and T08 are now two modes of one History screen, not separate navigation destinations.
- T03/T03a reflect the approved streamlined register experience, not a commitment to preserve every older UX v1.0 wireframe as a separate screen.
- 🔄 means intentionally merged, streamlined or awaiting confirmation against the approved prototype—not a production feature.

## 3. Administrator workspace tracker

| ID | Screen | Status | Notes |
|---|---|---|---|
| A01 | School overview | ⬜ | Operational overview and exceptions; not unbounded analytics |
| A02 | Student directory | ⬜ | Search/filter/create/archive/open profile |
| A03 | Student create/edit | ⬜ | Student master and guardian details |
| A04 | Student profile | ⬜ | Overview, guardians, enrolments, lessons, attendance, fees, invoices, payments, changes |
| A05 | Enrolment editor | ⬜ | Create, Change Teacher, end/re-enrol and fee mode |
| A06 | Teacher directory/profile | ⬜ | Teacher records and app-user association |
| A07 | Subject catalogue | ⬜ | Create/edit/archive |
| A08 | Session manager | ⬜ | Occurrence list/calendar, create, complete, cancel, reschedule |
| A09 | Session detail | ⬜ | Participation-level attendance and lesson records |
| A10 | Finance overview | ⬜ | Receivables, payments, invoice previews and exceptions |
| A11 | Fee schemes | ⬜ | Reusable templates and charge basis |
| A12 | Student financial setup | ⬜ | Student/enrolment-level fee assignments |
| A13 | Invoice preview/detail | ⬜ | Recalculate, compare, issue, void/reissue |
| A14 | Payments | ⬜ | Record receipts, allocate, reverse allocations |
| A15 | Reports | ⬜ | Operational and finance filters |
| A16 | Settings | ⬜ | Timezone, currency, defaults, schema/app settings |
| A17 | Audit & change history | ⬜ | Search/compare versions, operations, archive/restore |

## 4. Repository artefacts

| Artefact | Repository path | Status |
|---|---|---|
| Project overview | `README.md` | ✅ Committed |
| Class Register prototype | `prototype/class-register.html` | 🔒 v1.3 approved |
| Class Register specification | `docs/locked-class-register.md` | 🔒 |
| History prototype | `prototype/history-v1.2.html` | 🔒 v1.2 approved and committed |
| Teacher Student Directory prototype | `prototype/teacher-student-directory-v1.html` | 🔒 v1 approved and committed |
| Teacher Student Directory v1.1 | `prototype/teacher-student-directory-v1.1.html` | ⏸ Superseded by v1.2 |
| Teacher Student Directory v1.2 | `prototype/teacher-student-directory-v1.2.html` | 🟡 Direct row-to-profile navigation review |
| T05 v1.2 review notes | `docs/student-directory-v1.2-review.md` | 🟡 Under review |
| Teacher Student Profile v1 | `prototype/teacher-student-profile-v1.html` | ⏸ Superseded by v2 |
| Teacher Student Profile v2 | `prototype/teacher-student-profile-v2.html` | 🟡 Revised profile for review |
| Teacher Student Profile v2 specification | `docs/student-profile-v2-review.md` | 🟡 Revised decisions documented; pending approval |
| Lesson Notes pop-up specification | `docs/locked-lesson-notes-panel.md` | 🔒 Approved and committed |
| History specification | `docs/locked-history.md` | 🔒 Approved and committed |
| Whole project plan | `docs/PROJECT_PLAN.md` | ✅ Committed |
| Architecture baseline | `docs/ARCHITECTURE_BASELINE.md` | ✅ Committed |
| UX screen inventory | `docs/UX_BASELINE.md` | ✅ Committed |
| Decision log | `docs/DECISION_LOG.md` | ✅ Committed |
| Open policy decisions | `docs/OPEN_DECISIONS.md` | ✅ Committed |
| Student Directory specification | `docs/locked-student-directory.md` | 🔒 Approved and committed |
| This tracker | `docs/BUILD_TRACKER.md` | ✅ Committed |
| Next-chat handoff | `docs/HANDOFF_NEXT_CHAT.md` | ✅ Committed |

## 5. Release gates (do not mark complete until actually resolved)

- ⏸ Authentication/deployment identity method.
- Teacher visibility of other teachers' lesson notes: resolved — only explicitly shared notes are visible.
- ⏸ Future-session reassignment policy and workflow.
- ⏸ Provisional attendance expiry/confirmation policy.
- ⏸ Student-level per-lesson fee scope.
- ⏸ Cancellation/no-show billing policy.
- ⏸ Invoice cadence.
- ⏸ Discount permissions and limits.
- ⏸ GST/tax rules.
- ⏸ Refunds/credit notes/payment reversals scope.
- ⏸ Advance/unallocated payment handling.
- ⏸ School timezone.
- ⏸ Currency confirmation.
- ⏸ Installable/offline PWA deployment proof.
- ⏸ Group session activation in V1.
- ⏸ Guardian requirements for minors.

## 6. Next actions

1. Review and approve T05 Student Directory v1.1, preserving locked v1.
2. Verify the Student ID hand-off into the matching T06 profile.
3. Continue T06 review and obtain explicit approval before locking it.
4. Proceed to the remaining teacher screens, then the administrator workspace.
5. Complete UX sign-off before beginning production implementation.

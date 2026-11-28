# Celestial — Open Decisions and Release Gates

These items were explicitly unresolved in Technical Blueprint v1.1 / Application UX v1.0. Do not guess or quietly hard-code a policy. They may be visually prepared in a prototype, but the production behaviour must remain gated until decided.

| ID | Topic | Question requiring a decision | Impact |
|---|---|---|---|
| AUTH-01 | Authentication/deployment | How are teacher identities verified, and which Apps Script deployment mode is used? | Blocker for multi-user production |
| ENR-01 | Future sessions on teacher reassignment | Are old future sessions left on the old enrolment for admin review, or is an explicit bulk reassignment permitted? | Before reassignment release |
| ATT-01 | Provisional expiry | How long can future/overdue provisional attendance remain before reminder/escalation? | Before automation |
| BILL-01 | Student-level per-lesson scope | Charge once per student per calendar day or per eligible Session_Enrolment across all subjects? | Blocker for student-level per-lesson billing |
| BILL-02 | No-show/cancellation rules | How are teacher cancellation, late cancellation, student no-show and teacher absence treated? | Blocker for billing automation |
| BILL-03 | Invoice cadence | Manual preview on demand or scheduled monthly preview generation? Admin confirmation remains required before issue. | Before recurring billing |
| BILL-04 | Discounts | Who can apply/approve discounts and what limits apply? | Before discount feature |
| BILL-05 | Tax/GST | Do taxes apply; what rates, registration details and invoice disclosures are required? | Blocker before tax-enabled invoicing |
| BILL-06 | Refunds/credit notes | Which refund, credit note and payment-reversal workflows are required in V1? | Before refund handling |
| BILL-07 | Advance/unapplied payments | How do unallocated payments carry forward, expire or get refunded? | Before advance-payment automation |
| DATE-01 | School timezone | Confirm timezone for dates, sessions and due dates. | Blocker before production scheduling |
| FIN-01 | Currency | Confirm configured currency; INR was proposed but not formally confirmed. | Blocker before finance activation |
| PWA-01 | Installable/offline app | Is Apps Script-only acceptable, or is a separately hosted same-origin PWA needed? Prove install/cache/auth. | Blocker for PWA claim |
| GROUP-01 | Group classes in V1 | Are group session creation and management enabled in initial release or only structurally supported? | Before session UX freeze |
| DATA-01 | Guardian requirement | Must minors have a guardian contact at admission? | Before student form validation |

## Resolved decision\n\n- **AUTH-02 — Teacher note visibility:** Teachers may see another teacher's lesson notes/remarks only when the record is explicitly marked as shared. Private/unshared notes remain hidden. This policy is recorded in `docs/DECISION_LOG.md`.\n\n## Safe defaults already in the architecture baseline

These are not open to silent reinterpretation:
- Unmarked attendance is not Present.
- Future attendance is provisional until confirmed under the final policy.
- Provisional future attendance is not billable.
- Cancelled/rescheduled sessions are not automatically billable.
- Student-level and enrolment-level charges are additive where configured; preview combined impact.
- Invoice issue requires admin confirmation and backend recalculation.
- Historical records remain linked to their original teacher/enrolment.
- Future sessions affected by reassignment are flagged, not silently moved.
- Backend permissions are authoritative.

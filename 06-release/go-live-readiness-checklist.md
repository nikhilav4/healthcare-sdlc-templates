# Go-live readiness checklist

## When to use it

Use it for the go/no-go decision on any production release, from a major go-live to a small patch, trimming the rows a small release doesn't need. Work through it in readiness reviews in the weeks before go-live (T-14 and T-7 are common), so the go/no-go meeting confirms a position everyone already knows instead of discovering one. Hold the formal decision a day or two before cutover, and a final checkpoint just before cutover starts. Each row has an owner who brings evidence, not an opinion. The decision rules at the bottom are agreed with the sponsor before the meeting, and hard blockers override everything else.

## Template

| Field | Value |
| --- | --- |
| Release | [Name, version] |
| Go-live | [YYYY-MM-DD], cutover window [HH:MM] to [HH:MM] |
| Decision meeting | [YYYY-MM-DD HH:MM] |
| Decision owner | [Sponsor's name] |
| Facilitator | [Project manager] |
| Checklist version | [ ] |

Status for each row: Met, Partly met, Not met or N/A. A row marked as a blocker that is neither Met nor N/A makes the decision NO-GO, and N/A on a blocker row needs a reason in the evidence column.

*Every status needs evidence: a link, a document, a ticket, a test report. "The team says it's fine" is not evidence.*

### 1. Scope and change control

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 1.1 | Scope frozen on [YYYY-MM-DD]; nothing added since without an approved change request | | | | |
| 1.2 | Every change in the release traces to an approved story or change request, and the release notes list them | | | | |
| 1.3 | Production change approved by the change advisory board for the cutover window | Yes | [Change ticket ID] | | |
| 1.4 | Deployment and cutover plan reviewed by engineering, IT operations and the vendor | | | | |
| 1.5 | Go-live date checked against the clinical calendar: census peaks, holidays, other changes booked for the same window | | | | |

### 2. Testing and UAT sign-off

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 2.1 | System and integration testing complete, with results recorded | | | | |
| 2.2 | Regression tests passed on the release build | | | | |
| 2.3 | UAT complete: [N] of [N] scenarios run, [N] percent passed against a target of [N] percent | | | | |
| 2.4 | Every acceptance criterion traces to a passed test in the [traceability matrix](../03-requirements-and-design/requirements-traceability-matrix.md) | | | | |
| 2.5 | Interfaces tested end to end at production-like message volumes | | | | |
| 2.6 | Performance tested at expected peak load | | | | |
| 2.7 | UAT signed off by the business owner | Yes | | | |
| 2.8 | Clinical workflows signed off by a clinical reviewer for each affected discipline | Yes | | | |

### 3. Defects

Counts use the [defect severity guide](../05-testing/defect-severity-guide.md).

| Rating | Open now | Allowed at go-live | Met |
| --- | --- | --- | --- |
| S1 Critical | [n] | None | |
| S2 High | [n] | Only with a trained workaround, a fix date and the business owner's written acceptance | |
| S3 Medium | [n] | Up to [N], each with a fix date | |
| S4 Low | [n] | Any number, listed as known issues | |
| Clinical-safety flag, any severity | [n] | None | |

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 3.1 | No open S1 defects | Yes | | | |
| 3.2 | No open defects with the clinical-safety flag | Yes | | | |
| 3.3 | Each open S2 has a workaround that support and super-users have been trained on, and a fix date | | | | |
| 3.4 | Known issues written up for the service desk and the release notes | | | | |

*Look at the flag history, not just today's count. If a flag was cleared this week, confirm that a clinical reviewer cleared it and recorded why.*

### 4. Operational readiness

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 4.1 | [Cutover runbook](cutover-and-rollback-runbook.md) complete, with owners and timings, and rehearsed end to end in a production-like environment | | [Runbook version, rehearsal date] | | |
| 4.2 | Rollback tested end to end, including re-pointing interfaces; time to roll back measured at [duration] | Yes | | | |
| 4.3 | Rollback triggers, decision owner, deputy and point of no return written into the runbook | | | | |
| 4.4 | Monitoring and alerts live for the application, the interfaces (queue depth, error queue) and the infrastructure, routed to on-call | | | | |
| 4.5 | On-call rota covers cutover and hypercare, nights and weekends included, with names and numbers | | | | |
| 4.6 | Data migration verified: record counts reconcile, and clinicians have spot-checked migrated charts (allergies, active medications, problem lists) | Yes, when data is migrated | | | |
| 4.7 | Backup taken before cutover, and a restore tested | | | | |
| 4.8 | Downtime procedures ready in every clinical area that loses access: forms, downtime reports, the critical-result call process, and a back-entry plan with owners | Yes | | | |
| 4.9 | Service desk has the support model, known issues, scripts and the escalation route | | | | |

### 5. Security and compliance

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 5.1 | [Privacy and security review](../03-requirements-and-design/privacy-and-security-review.md) signed off; no critical or high findings open unless formally accepted by security | | | | |
| 5.2 | No PHI in application logs, error messages, analytics or monitoring tools, checked on the release build | | | | |
| 5.3 | Production access matches the approved role design; test and project accounts removed or disabled; admin access time-limited | | | | |
| 5.4 | Audit logging on and verified for access to patient records | | | | |
| 5.5 | Business associate agreements in place with every vendor that can reach PHI in production | | | | |
| 5.6 | Emergency access (break-the-glass) configured and tested, where the system has restricted records | | | | |
| 5.7 | Critical and high findings from vulnerability scans or penetration tests fixed, or accepted by security | | | | |

### 6. Training and support

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 6.1 | Training completion at or above [N] percent for each role, reported by unit and shift, with night and weekend staff included | | | | |
| 6.2 | Super-users named for every unit and shift, trained, and scheduled for go-live | | | | |
| 6.3 | Tip sheets and quick guides published where staff can find them mid-shift | | | | |
| 6.4 | Service desk briefed on known issues, workarounds, scripts and the route to the project team | | | | |
| 6.5 | Vendor support confirmed for cutover and hypercare, with contacts and response times | | | | |

### 7. Communications

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 7.1 | Go-live date, downtime window and what to expect sent to affected staff at [T-14] and [T-2] | | | | |
| 7.2 | Clinical leadership and department heads (emergency department, pharmacy, laboratory, nursing) briefed on the cutover and downtime plan | | | | |
| 7.3 | [Release notes](release-notes.md) published | | | | |
| 7.4 | Command center contacts and bridge line sent to every unit | | | | |
| 7.5 | Patients told, if they will notice the change (portal outage, new reminders, check-in changes) | | | | |
| 7.6 | Messages for every outcome drafted in advance, postponement included | | | | |

### 8. Hypercare

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 8.1 | [Hypercare plan](../07-hypercare/hypercare-plan.md) approved: duration, exit criteria, support model | | | | |
| 8.2 | Command center staffed for [hours], with a roster | | | | |
| 8.3 | Daily huddle scheduled, with clinical and technical leads | | | | |
| 8.4 | At-the-elbow support scheduled on every unit and shift for the first [N] days | | | | |
| 8.5 | Metrics and thresholds agreed (ticket volume, interface errors, back-entry backlog) | | | | |
| 8.6 | Clinical escalation path sent to every unit | | | | |

### 9. Conditions

Fill this in only for a CONDITIONAL GO. Every gap that is not a blocker gets a workaround, an owner and a due date.

| # | Condition | Row | Owner | Due | How it will be checked |
| --- | --- | --- | --- | --- | --- |
| C1 | | | | | |

*Make conditions due in the first days of hypercare, not "after go-live". A condition without a date is a gap the team has agreed to forget.*

### 10. Decision

Hard blockers override everything else. If any blocker row is neither Met nor N/A, the decision is NO-GO, however good the rest of the checklist looks. No average, vote, deadline or sponsor preference outweighs a blocker.

The hard blockers in this checklist:

- 1.3: no approved production change for the cutover window
- 2.7 and 2.8: UAT not signed off by the business owner, or clinical workflows not signed off by a clinical reviewer
- 3.1: an open S1 defect
- 3.2: an open defect with the clinical-safety flag
- 4.2: rollback not tested end to end
- 4.6: migrated data not reconciled and spot-checked by clinicians
- 4.8: downtime procedures not ready in a clinical area that loses access

*Agree the blocker list with the sponsor before the meeting, not during it. Add to it if your release needs more. Taking one off needs the sponsor's agreement in writing.*

| Decision | When it applies |
| --- | --- |
| GO | Every blocker row is Met or N/A, and every other row is Met or N/A. |
| CONDITIONAL GO | Every blocker row is Met or N/A. Each remaining gap has a workaround, an owner and a due date in the conditions table, and the decision owner accepts them. |
| NO-GO | Any blocker row is neither Met nor N/A, or a gap has no credible workaround. Set the date of the next decision and name what has to change before it. |

Decision record:

| Field | Value |
| --- | --- |
| Decision | [GO / CONDITIONAL GO / NO-GO] |
| Hard blockers open | [None / row numbers] |
| Conditions | [None / C1 to Cn] |
| Decision owner | [Name, role] |
| Decided at | [YYYY-MM-DD HH:MM] |
| Next checkpoint | [Final check before cutover starts, YYYY-MM-DD HH:MM] |

### 11. Sign-off

Each lead confirms readiness for their own area. The decision owner decides; nobody votes.

| Role | Name | Go or no-go | Comment | Date |
| --- | --- | --- | --- | --- |
| Sponsor (decision owner) | | | | |
| Project manager | | | | |
| Business owner | | | | |
| Clinical lead | | | | |
| Engineering lead | | | | |
| QA lead | | | | |
| IT operations | | | | |
| Security and privacy | | | | |
| Support lead | | | | |
| Vendor lead | | | | |

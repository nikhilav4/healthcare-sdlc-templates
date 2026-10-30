# Go-live readiness checklist: EHR Integration Phase 2

*Fictional example. The project, the organization, the people and every figure here are made up. It is the same project as the example register in [raid-log](https://github.com/nikhilav4/raid-log/blob/main/examples/ehr-integration.yaml) and the [example status report](weekly-status-report-ehr-integration.md). The register is a snapshot from 2026-10-27; this checklist is from the go/no-go meeting five weeks later, so the table below shows where each of those items ended up. It is filled in from the [go-live readiness checklist template](../06-release/go-live-readiness-checklist.md).*

| Field | Value |
| --- | --- |
| Release | EHR Integration Phase 2 |
| Go-live | 2026-12-05, cutover window 01:00 to 05:00 |
| Decision meeting | 2026-12-03 14:00 |
| Decision owner | Chief Medical Information Officer (sponsor); deputy for overnight decisions: Chief Nursing Officer |
| Facilitator | Elena Ruiz, project manager |
| Checklist version | 4, after readiness reviews on 11-19 and 11-24 |

## Where the RAID items stand

| ID | Item | On 2026-10-27 | On 2026-12-03 |
| --- | --- | --- | --- |
| R-001 | Interface vendor may slip the HL7 ADT feed | Mitigating, exposure 20 | Closed 11-20. The test feed arrived on 11-04, inside the trigger date steering set, and passed integration testing on 11-20. The flat-file census load stays built as a fallback for go-live night. |
| R-002 | Duplicate MPI records could overlay charts | Mitigating, 15 | Mitigating. HIM worked all 1,840 flagged pairs; 46 unresolved pairs are held out of the merge, as the contingency planned (condition C4). |
| R-003 | Night-shift nurses may not finish training | Open, 12 | Mitigating. Night-shift RNs at 88 percent (condition C1). |
| R-004 | Point-of-care glucose units mapped inconsistently | Monitoring, 8 | Closed 11-13. The parallel run found the problem (DEF-163, below); it was fixed and the rerun matched. |
| R-006 | Interface analyst leaves in November | Open, 9 | Closed 11-20. Runbook written and paired sessions done before the analyst left. |
| R-007 | Go-live may coincide with a census surge | Open, 9, review overdue | Mitigating. Threshold agreed on 11-10; final check at 18:00 on 12-04. |
| R-008 | Pharmacy formulary mapping incomplete at cutover | Mitigating, 12 | Mitigating. 9 of the 140 NDCs still unmapped (condition C2). |
| R-010 | ED downtime procedures not rehearsed | Open, 10 | Closed 11-13, after the tabletop with ED charge nurses on 11-12. |
| I-001 | No pediatric test patients in UAT | Open, medium | Closed 11-12. Pack loaded; weight-based dosing scenarios passed in UAT cycle 2. |
| I-003 | Duplicate allergy entries after test load 2 | Mitigating, high | Resolved 11-03 in load 3, and confirmed absent in load 4. |
| I-004 | Interface error queue not monitored after hours | Open, high | Resolved 11-19, before integration testing ended. Error-queue alerts now page the on-call interface analyst. |

Status for each row: Met, Partly met, Not met or N/A. A blocker row that is neither Met nor N/A makes the decision NO-GO.

## 1. Scope and change control

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 1.1 | Scope frozen on 2026-11-13; nothing added since without an approved change request | | Change log: no additions since the freeze | Elena Ruiz | Met |
| 1.2 | Every change in the release traces to an approved story or change request, and the release notes list them | | Release notes v3; traceability matrix, 11-30 | Sam Patel | Met |
| 1.3 | Production change approved by the change advisory board for the cutover window | Yes | CHG-20931 approved 12-01; go-live weekend network change approved 11-18 (D-002) | Tom Okafor | Met |
| 1.4 | Deployment and cutover plan reviewed by engineering, IT operations and the vendor | | Runbook v6 walkthrough, 11-30 | Tom Okafor | Met |
| 1.5 | Go-live date checked against the clinical calendar | | Census threshold agreed with nursing leadership on 11-10 (R-007): postpone one week if adult medical-surgical occupancy is 95 percent or more at 18:00 on 12-04 | Elena Ruiz | Met |

## 2. Testing and UAT sign-off

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 2.1 | System and integration testing complete, with results recorded | | Integration test report, 11-20 | Priya Shah | Met |
| 2.2 | Regression tests passed on the release build | | Regression run 12-01: 418 of 418 passed | Sam Patel | Met |
| 2.3 | UAT complete: 212 of 212 scenarios run, 98.6 percent passed against a target of 95 percent | | UAT summary v4, 11-24. The three failures are S3 and S4 defects with fix dates. | Sam Patel | Met |
| 2.4 | Every acceptance criterion traces to a passed test | | Traceability matrix coverage check, 11-30: no gaps | Sam Patel | Met |
| 2.5 | Interfaces tested end to end at production-like message volumes | | ADT, lab results and FHIR scheduling run at a full day's volume, 11-19 | Priya Shah | Met |
| 2.6 | Performance tested at expected peak load | | Load test 11-18 at 1.5 times the busiest hour | Tom Okafor | Met |
| 2.7 | UAT signed off by the business owner | Yes | Signed 11-24 | Director of Clinical Applications | Met |
| 2.8 | Clinical workflows signed off by a clinical reviewer for each affected discipline | Yes | Nursing (Jordan Reyes), pharmacy informatics and laboratory informatics on 11-24; ED physician lead on 11-25 | Jordan Reyes | Met |

## 3. Defects

| Rating | Open now | Allowed at go-live | Met |
| --- | --- | --- | --- |
| S1 Critical | 0 | None | Yes |
| S2 High | 1 | Only with a trained workaround, a fix date and the business owner's written acceptance | Yes (DEF-187, condition C3) |
| S3 Medium | 6 | Up to 10, each with a fix date | Yes |
| S4 Low | 14 | Any number, listed as known issues | Yes |
| Clinical-safety flag, any severity | 0 | None | Yes |

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 3.1 | No open S1 defects | Yes | Defect report, 12-03 08:00 | Sam Patel | Met |
| 3.2 | No open defects with the clinical-safety flag | Yes | Four flagged defects were raised in testing; each was fixed, retested and cleared by a clinical reviewer. The last, DEF-163, closed on 11-13. | Sam Patel | Met |
| 3.3 | Each open S2 has a trained workaround and a fix date | | DEF-187: point-of-care glucose charges don't reach billing. Revenue integrity runs a daily reconciliation report; the fix ships in the 12-10 patch. | Priya Shah | Met, tracked as C3 |
| 3.4 | Known issues written up for the service desk and the release notes | | Known issues list v2; release notes section 4 | Sam Patel | Met |

*DEF-163 shows why the flag is separate from severity. The parallel run of 200 point-of-care glucose results (R-004) found three from one meter model filed with the wrong unit label. The values themselves were right, but a clinician reading them against the label would have seen a dangerous low. It was S2 with the clinical-safety flag. Lab informatics fixed the mapping table on 11-12, the rerun on 11-13 matched 200 of 200, and lab informatics signed off the mapping that day (D-005).*

## 4. Operational readiness

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 4.1 | Cutover runbook complete, with owners and timings, and rehearsed end to end | | Runbook v6. Cutover rehearsal on 11-21 took 3 h 35 min against the 4-hour window. | Elena Ruiz | Met |
| 4.2 | Rollback tested end to end, including re-pointing interfaces | Yes | The first rollback rehearsal on 11-21 failed at step RB4: interface routes did not switch back to the legacy system. The runbook was corrected, and the second rehearsal on 12-01 passed in 1 h 50 min. | Tom Okafor | Met |
| 4.3 | Rollback triggers, decision owner, deputy and point of no return in the runbook | | Runbook section 5. Point of no return 03:10, so a rollback still finishes by 05:00. If ADT isn't flowing at 03:10, the census switches to the flat-file load rather than rolling back. | Elena Ruiz | Met |
| 4.4 | Monitoring and alerts live, routed to on-call | | Error-queue alerts page the on-call interface analyst; test page on 11-19 answered in 4 minutes (I-004) | Priya Shah | Met |
| 4.5 | On-call rota covers cutover and hypercare, nights and weekends included | | Rota v3, 12-02 | Elena Ruiz | Met |
| 4.6 | Data migration verified: counts reconcile, clinicians spot-checked migrated charts | Yes | Load 4 on 11-17 reconciled to source with no duplicate allergies (I-003). Two pharmacists and two nurses spot-checked 150 migrated charts on 11-18 and found no errors. 46 MPI pairs held out of the merge (C4). | Marcus Bell | Met |
| 4.7 | Backup taken before cutover, and a restore tested | | Restore tested 11-30; pre-cutover backup scheduled for 21:00 on 12-04 (runbook P5) | Tom Okafor | Met |
| 4.8 | Downtime procedures ready in every clinical area that loses access | Yes | ED tabletop on 11-12 (R-010). Downtime packets on all 14 inpatient units, the ED, pharmacy and the lab by 12-02. Critical-result call process confirmed with the lab on 11-30. Clinic leaders accepted the four-hour read-only window on 11-05 (A-003). | Dana Whitfield | Met |
| 4.9 | Service desk has the support model, known issues, scripts and escalation route | | Service desk briefing, 12-01 | Service desk manager | Met |

## 5. Security and compliance

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 5.1 | Privacy and security review signed off; no critical or high findings open | | Security review complete and production access approved 10-16 (R-009) | Grace Liu | Met |
| 5.2 | No PHI in application logs, error messages, analytics or monitoring | | Log scan of the release build, 11-30 | Grace Liu | Met |
| 5.3 | Production access matches the role design; test and project accounts removed; admin access time-limited | | Access review 12-02: 31 test accounts disabled; project admin access expires 12-19 | Grace Liu | Met |
| 5.4 | Audit logging on and verified for access to patient records | | Audit logging test, 11-23 | Grace Liu | Met |
| 5.5 | Agreements in place with every vendor that can reach PHI | | Business associate agreements on file for the EHR and interface vendors; data-sharing agreement amendment signed by the privacy office on 11-03 (D-004) | Grace Liu | Met |
| 5.6 | Emergency access configured and tested for restricted records | | Break-the-glass tested with restricted test patients, 11-23 | Grace Liu | Met |
| 5.7 | Critical and high scan or penetration test findings fixed or accepted | | Vulnerability scan 11-25: none critical or high | Tom Okafor | Met |

## 6. Training and support

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 6.1 | Training completion at or above 95 percent for each role, by unit and shift | | 97 percent overall, but night-shift RNs are at 88 percent (R-003) | Jordan Reyes | Partly met; condition C1 |
| 6.2 | Super-users named for every unit and shift, trained and scheduled | | 58 super-users across 14 units, nights included | Jordan Reyes | Met |
| 6.3 | Tip sheets and quick guides published where staff can find them mid-shift | | Intranet page and a binder on every unit, 11-30 | Jordan Reyes | Met |
| 6.4 | Service desk briefed on known issues, workarounds and the route to the project team | | Briefing and scripts v2, 12-01 | Service desk manager | Met |
| 6.5 | Vendor support confirmed for cutover and hypercare | | EHR and interface vendors on the bridge for cutover; 30-minute response during hypercare | Priya Shah | Met |

## 7. Communications

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 7.1 | Go-live date, downtime window and what to expect sent at T-14 and T-2 | | T-14 notice sent 11-20; the T-2 notice goes out after this decision | Elena Ruiz | Met |
| 7.2 | Clinical leadership and department heads briefed on the cutover and downtime plan | | Briefings 11-23 to 11-25 | Dana Whitfield | Met |
| 7.3 | Release notes published | | Release notes v3, 12-02 | Elena Ruiz | Met |
| 7.4 | Command center contacts and bridge line on every unit | | Contact cards delivered 12-02 | Dana Whitfield | Met |
| 7.5 | Patients told about anything they will notice | | Portal banner since 12-01: online booking unavailable from 01:00 to 05:00 on 12-05 | Elena Ruiz | Met |
| 7.6 | Messages for every outcome drafted, postponement included | | Approved by the Chief Nursing Officer's office, 12-02 | Elena Ruiz | Met |

## 8. Hypercare

| # | Criterion | Blocker | Evidence | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| 8.1 | Hypercare plan approved | | Approved 11-24; runs 12-05 to 12-18 | Elena Ruiz | Met |
| 8.2 | Command center staffed, with a roster | | 24 hours a day for the first 72 hours, then 07:00 to 23:00 with on-call overnight | Elena Ruiz | Met |
| 8.3 | Daily huddle scheduled with clinical and technical leads | | 08:30 and 16:30 in week one | Elena Ruiz | Met |
| 8.4 | At-the-elbow support on every unit and shift | | All shifts for the first 7 days; super-user rounding on nights for 14 days (R-003) | Jordan Reyes | Met |
| 8.5 | Metrics and thresholds agreed | | Hypercare plan section 6 | Elena Ruiz | Met |
| 8.6 | Clinical escalation path sent to every unit | | Printed on the command center contact cards | Dana Whitfield | Met |

## 9. Conditions

| # | Condition | Row | Owner | Due | How it will be checked |
| --- | --- | --- | --- | --- | --- |
| C1 | The 26 night-shift RNs who haven't finished training complete the recorded session before their first shift on the new system; super-users round on nights from 12-05 to 12-18 | 6.1, R-003 | Jordan Reyes | Before each nurse's first shift | Unit managers check the roster at every huddle |
| C2 | Pharmacy informatics maps the last 9 NDCs; until then, orders for them go in as free text with pharmacist verification | R-008 | Marcus Bell | 2026-12-09 | Mapping report; verification queue reviewed at every huddle |
| C3 | Revenue integrity runs the daily charge reconciliation until the DEF-187 fix ships | 3.3 | Priya Shah | 2026-12-10 | Fix verified in production, then three days of clean reconciliation |
| C4 | HIM resolves the 46 potential-duplicate pairs held out of the merge; registration reviews those patients' records when they arrive | 4.6, R-002 | Marcus Bell | 2026-12-18 | HIM queue at zero |

## 10. Decision

Hard blockers override everything else. If any blocker row is neither Met nor N/A, the decision is NO-GO, however good the rest of the checklist looks.

| Field | Value |
| --- | --- |
| Decision | CONDITIONAL GO |
| Hard blockers open | None. Rows 1.3, 2.7, 2.8, 3.1, 3.2, 4.2, 4.6 and 4.8 are all Met. |
| Conditions | C1 to C4 |
| Decision owner | Chief Medical Information Officer (sponsor) |
| Decided at | 2026-12-03 15:10 |
| Next checkpoints | 2026-12-04 18:00, census check against the R-007 threshold (Dana Whitfield). 2026-12-05 00:30, checkpoint A, go to start cutover (Elena Ruiz). |

*Why conditional rather than a plain GO: night-shift training is short of target, and three items carry residual work into hypercare. None of them is a blocker, each has a workaround, an owner and a date, and the sponsor accepted them in the meeting. At the 11-24 readiness review, row 4.2 alone would have made this a NO-GO: the first rollback rehearsal had failed, and it took a second, successful one on 12-01 to clear it.*

## 11. Sign-off

| Role | Name | Go or no-go | Comment | Date |
| --- | --- | --- | --- | --- |
| Sponsor (decision owner) | Chief Medical Information Officer | Conditional go | Accepts C1 to C4 | 2026-12-03 |
| Project manager | Elena Ruiz | Go | | 2026-12-03 |
| Business owner | Director of Clinical Applications | Go | | 2026-12-03 |
| Clinical readiness and nursing review | Jordan Reyes | Conditional go | C1 | 2026-12-03 |
| Cutover and clinical operations | Dana Whitfield | Go | Downtime packets and contact cards on every unit | 2026-12-03 |
| Integrations | Priya Shah | Go | C3 | 2026-12-03 |
| Data migration | Marcus Bell | Conditional go | C2 and C4 | 2026-12-03 |
| Infrastructure and IT operations | Tom Okafor | Go | Rollback rehearsal passed 12-01 | 2026-12-03 |
| QA lead | Sam Patel | Go | | 2026-12-03 |
| Security and privacy | Grace Liu | Go | | 2026-12-03 |
| Pharmacy informatics | Pharmacy informatics lead | Conditional go | C2 | 2026-12-03 |
| Laboratory informatics | Laboratory informatics lead | Go | Unit mapping signed off 11-13 | 2026-12-03 |
| Service desk | Service desk manager | Go | | 2026-12-03 |
| EHR vendor | Vendor project lead | Go | | 2026-12-03 |

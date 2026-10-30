# Weekly status report: EHR Integration Phase 2

*Fictional example. The project, the organization, the people and every figure here are made up. It is the same project as the example register in [raid-log](https://github.com/nikhilav4/raid-log/blob/main/examples/ehr-integration.yaml), and the RAID items below match that register as of 2026-10-27. It is filled in from the [weekly status report template](../00-every-phase/weekly-status-report.md).*

| Field | Value |
| --- | --- |
| Project | EHR Integration Phase 2 |
| Period | 2026-10-20 to 2026-10-26 |
| Report date | 2026-10-27 |
| Project manager | Elena Ruiz |
| Sponsor | Chief Medical Information Officer |
| Go-live date | 2026-12-05, unchanged |

## Overall status

| Overall | Last week | Trend |
| --- | --- | --- |
| Amber | Amber | Worsening |

| Area | Status | Why |
| --- | --- | --- |
| Schedule | Amber | The vendor's HL7 ADT test feed slipped again, to 11-04 (R-001). Go-live holds, but integration testing now ends 11-20 instead of 11-13 and the slack before UAT exit is gone. |
| Scope | Green | No change requests this week. Using the ADT fallback would need one (decision 1). |
| Budget | Green | Forecast $64,000 under the approved budget, which is the unused contingency. Option B in decision 1 would use most of it. |
| Resources | Amber | The interface analyst who knows the mappings best leaves in November (R-006). Paired mapping sessions and a written runbook are due before 11-20. |
| Quality and testing | Amber | Duplicate allergy entries from migration test load 2 (I-003, patient safety) are understood but not yet fixed. UAT still has no pediatric test patients, so weight-based dosing can't be tested (I-001). |
| Clinical readiness | Amber | Night-shift training is behind (R-003, exposure up from 8 to 12). ED downtime procedures haven't been rehearsed (R-010). Pharmacy still has 140 NDCs to map (R-008). |
| Privacy and security | Green | Security review complete and production access approved on 10-16 (R-009 closed). The privacy office is due to sign the data-sharing agreement amendment by 11-04 (D-004). |

## Summary

Go-live on 2026-12-05 still holds, with less room than a week ago. The vendor moved the HL7 ADT test feed to 11-04, which pushes the end of integration testing from 11-13 to 11-20 and takes R-001 to exposure 20, the highest on the register. The flat-file census fallback is scoped and can still be ready in time, so we are asking steering on 11-03 to set the date on which we stop waiting for the vendor (decision 1). The duplicate allergies from migration test load 2 have a known cause, and the fix goes into load 3 on 11-03.

## Highlights this period

- Agency nurses' SSO login loop fixed on 10-21 and verified with five agency accounts (I-002 resolved).
- Root cause of the duplicate allergy entries found on 10-20: allergies were loaded from two source tables (I-003). The fix is in the build for migration test load 3.
- Two new risks logged, both tagged patient-safety: pharmacy formulary mapping (R-008) and ED downtime procedures not yet rehearsed (R-010).

## Milestones

| Milestone | Baseline | Forecast or actual | Status | Notes |
| --- | --- | --- | --- | --- |
| Migration test load 2 | 2026-10-12 | 2026-10-13 | Complete | Surfaced I-003 |
| Security review and production access | 2026-10-16 | 2026-10-16 | Complete | R-009 closed |
| Vendor HL7 ADT test feed | 2026-10-10 | 2026-11-04 | Late | R-001; the vendor's second slip |
| Migration test load 3 | 2026-11-03 | 2026-11-03 | On track | Carries the I-003 fix |
| UAT cycle 1 complete | 2026-11-06 | 2026-11-06 | At risk | Pediatric dosing scenarios blocked until test patients arrive (I-001) |
| FHIR scheduling endpoint in test | 2026-10-30 | 2026-11-06 | At risk | D-001; need-by moved from 10-30 |
| ED downtime tabletop rehearsal | 2026-11-12 | 2026-11-12 | On track | R-010 |
| Integration testing complete | 2026-11-13 | 2026-11-20 | At risk | Waits on the ADT feed |
| UAT exit | 2026-11-20 | 2026-11-24 | At risk | ADT scenarios move into cycle 2 |
| Cutover rehearsal | 2026-11-21 | 2026-11-21 | On track | |
| Go/no-go meeting | 2026-12-03 | 2026-12-03 | On track | |
| Go-live | 2026-12-05 | 2026-12-05 | At risk | Census threshold for postponement not yet agreed (R-007) |

## Top risks and issues

| ID | Item | Exposure or severity | Owner | Change since last report | Next step and date |
| --- | --- | --- | --- | --- | --- |
| R-001 | Interface vendor may slip the HL7 ADT feed | 20 (4 x 5) | Priya Shah | Up from 15: test feed moved to 11-04 | Weekly vendor checkpoint; flat-file fallback scoped; trigger date is decision 1 on 11-03 |
| R-002 | Duplicate patient records in the legacy MPI could overlay charts during the merge | 15 (3 x 5), patient safety | Marcus Bell | Same | HIM working the 1,840 pairs flagged on 10-07 before cutover; review 11-05 |
| R-003 | Night-shift nurses may not finish training before go-live | 12 (3 x 4) | Jordan Reyes | Up from 8 | Recorded sessions, plus super-user rounding on nights for the first two weeks; review 11-02 |
| R-008 | Pharmacy formulary mapping may be incomplete at cutover | 12 (3 x 4), patient safety | Marcus Bell | New | Pharmacy informatics maps the remaining 140 NDCs; anything unmapped falls back to free text with pharmacist verification; review 11-03 |
| R-010 | ED downtime procedures have not been rehearsed for the cutover window | 10 (2 x 5), patient safety | Dana Whitfield | New | Tabletop with ED charge nurses on 11-12; downtime packets printed; review 11-04 |
| I-003 | Allergy lists show duplicate entries after the second migration test load | High, patient safety | Marcus Bell | Root cause found 10-20 | Fix in migration test load 3 on 11-03; review 10-30 |
| I-004 | Interface engine error queue is not monitored after hours | High | Priya Shah | Same | Route error-queue alerts to the on-call interface analyst before integration testing ends; review 11-02 |

One review is overdue: R-007, the census-surge risk, was due on 10-26 and `raid validate` now flags it. It needs decision 2.

## Decisions needed

| # | Decision | Options | Recommendation | From whom | Needed by |
| --- | --- | --- | --- | --- | --- |
| 1 | When to stop waiting for the vendor's real-time ADT feed (R-001) | A: keep waiting, and accept that go-live moves if the feed slips again. B: set a trigger date; if the feed isn't passing messages in test by then, go live on the nightly flat-file census load and move real-time ADT to a fast follow. | B, with a trigger of 11-06. The flat-file load needs four working days to finish and test. Under B, bed managers update the bed board by hand during the day until real-time ADT arrives; Dana Whitfield is walking nursing leadership through that workaround before 11-03. | Steering committee | 2026-11-03 |
| 2 | The inpatient census level at which the go-live weekend is postponed (R-007) | Nursing leadership sets the threshold, the measure and who checks it | Check adult medical-surgical occupancy at 18:00 on 12-04 and postpone by one week if it is at or above the agreed level | Chief Nursing Officer, through the sponsor | 2026-11-10 |

## Budget

| Approved | Spent to date | Committed | Forecast at completion | Variance | Contingency left |
| --- | --- | --- | --- | --- | --- |
| $1,850,000 (includes $120,000 contingency) | $1,212,400 | $356,000 | $1,786,000 | $64,000 under | $64,000 of $120,000 |

$18,000 of contingency was released this week to fund super-user rounding on nights for the first two weeks after go-live (R-003). Not yet in the forecast: if steering chooses option B in decision 1, the vendor's change order for the ADT fast follow, estimated at $40,000 to $60,000, would come out of the remaining contingency.

## Next period

- 10-30: Check a sample of provider directory NPIs against the credentialing roster (A-002, Marcus Bell). This check has already moved once, from 10-16.
- 10-30: Confirm the allergy fix is in the load 3 build (I-003, Marcus Bell).
- 11-02: Chase the vendor's pediatric test-patient pack, requested on 10-05 (I-001, Sam Patel).
- 11-02: Confirm the recorded training sessions are published and draft the night super-user rota (R-003, Jordan Reyes).
- 11-03: Steering committee, decision 1 (Elena Ruiz). Migration test load 3 (Marcus Bell).
- 11-04: Vendor's ADT test feed due (R-001, Priya Shah). Data-sharing agreement amendment due from the privacy office (D-004, Grace Liu).
- 11-06: FHIR scheduling endpoint due in test (D-001, Priya Shah). Clinic leaders confirm the four-hour read-only window for cutover (A-003, Dana Whitfield).
- By 11-20: Paired mapping sessions with the departing interface analyst, and the written runbook (R-006, Elena Ruiz).

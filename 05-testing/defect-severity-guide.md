# Defect severity guide

## When to use it

Agree it before system testing starts and use the same scale through UAT, release and hypercare, so that an S2 means the same thing to the tester, the vendor and the sponsor at the go/no-go meeting. It keeps apart two questions that teams tend to blur: how badly a defect breaks the system (severity) and whether it could hurt a patient (the clinical-safety flag). The two often disagree. A cosmetic defect can be dangerous, and a complete failure of a back-office report can be clinically harmless.

## Severity

| Severity | Definition | Examples |
| --- | --- | --- |
| S1 Critical | The system or a core function is unusable, data is lost or corrupted, or one patient's data is shown or filed as another's. No workaround. | Users can't sign in; results filed to the wrong patient; orders lost on save |
| S2 High | A major function fails or gives wrong results. A workaround exists but is slow, error-prone or needs extra staff. | An interface rejects one message type, so staff re-enter those by hand; a report used in daily operations is wrong |
| S3 Medium | A function works but has a problem. A reasonable workaround exists. | Search ignores one filter; a printout cuts off a line that is still visible on screen |
| S4 Low | Cosmetic, or a minor inconvenience. | Misaligned label; inconsistent capitalization; a typo in help text |

Severity describes impact. Priority, which the product owner sets, describes the order of fixing. A defect can be high severity and low priority, for example a broken year-end report in March.

## Clinical-safety flag

The flag records clinical risk. It answers one question: could this defect contribute to harm to a patient, directly or through a decision a clinician makes based on what the system shows? It can be set at any severity.

Raise it when a defect could cause or hide:

- the wrong patient: misidentification, records merged or split wrongly, results or notes filed to someone else
- the wrong medication, dose, route, frequency or timing, or a missing allergy or interaction warning
- a result that is wrong, missing, late or easy to misread, especially a critical result
- an order, referral or task that is lost, duplicated or delayed without anyone being told
- clinical information that is truncated, out of date or displayed in a misleading way
- documentation a clinician believes was saved but wasn't

Who sets and clears it:

- Anyone can propose the flag. A clinical reviewer confirms it and records the reasoning in the defect.
- Only a clinical reviewer can clear it, and the reason goes in the defect: fixed and retested, or judged on review not to carry the risk after all.
- The project manager, the vendor and engineering can't remove the flag, however close go-live is.

*Severity and the flag disagree more often than people expect. A medication name cut short in a narrow list column looks like an S4 layout bug until the column shows "hydr" for both hydralazine and hydroxyzine. That defect is S4 with the clinical-safety flag, and it blocks release.*

| Defect | Severity | Clinical-safety flag | Why |
| --- | --- | --- | --- |
| Medication list column truncates drug names | S4 | Yes | Look-alike drug names become identical |
| Monthly billing extract fails | S2 | No | Serious for revenue, but no route to a patient |
| Lab result shows the right value with the wrong reference range | S2 | Yes | A clinician may misjudge whether the value is abnormal |
| An allergy entered in the new system is missing from the downtime report | S3 | Yes | During downtime, staff rely on that report |

## Triage

| Phase | Cadence | Who attends |
| --- | --- | --- |
| System testing | Twice a week | QA lead, engineering lead, product owner |
| UAT | Daily | Add the UAT lead and a clinical reviewer |
| Release week and hypercare | Daily, and at once for any S1 or flagged defect | Add the support lead and the vendor |

| Severity | Triaged within | Expected fix |
| --- | --- | --- |
| S1, or any defect with the clinical-safety flag | [1 hour in testing; 15 minutes in hypercare] | [Before release; a hotfix if found in production] |
| S2 | [1 working day] | [Before release, or an approved workaround and a fix date] |
| S3 | [2 working days] | [Planned into a release] |
| S4 | [Next triage] | [Backlog] |

## What blocks a release

| Open at go-live | Allowed? |
| --- | --- |
| Any S1 | No. Hard blocker. |
| Any defect with the clinical-safety flag | No. Hard blocker. |
| S2 | Only with a workaround that support and super-users have been trained on, a fix date, and the business owner's written acceptance. Each becomes a condition on a CONDITIONAL GO. |
| S3 | Up to [agreed number], each with a fix date. |
| S4 | No limit. Listed as known issues in the release notes. |

## Writing a defect

| Field | What to put |
| --- | --- |
| Title | What is wrong, and where: "Allergy banner missing on transfer summary", not "Bug in summary" |
| Steps to reproduce | Numbered, from a known starting point |
| Expected and actual | What should have happened, and what did |
| Environment and build | [ ] |
| Test patient and account | Test IDs only |
| Evidence | A screenshot or log extract with no real patient data |
| Severity | S1 to S4, with one line of reasoning |
| Clinical-safety flag | Yes or no, who confirmed it, and why |

*Never paste real patient identifiers into a defect, a screenshot or a chat about one. Defect trackers are rarely approved for PHI, and vendors usually have access to them.*

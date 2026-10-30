# UAT plan

## When to use it

Write it before user acceptance testing starts and get it agreed by the business owner, the clinical reviewers and the QA lead, since they are the people who will sign off against it. UAT is where the people who will use the system confirm that it supports their real work, end to end, with realistic data. In healthcare that means clinicians testing clinical workflows, and the plan has to secure their time, which is usually the scarcest resource on the project. Settle the entry and exit criteria up front: arguing about them in the last week of testing is how releases go out with problems nobody accepted.

## Template

| Field | Value |
| --- | --- |
| Project or release | [Name] |
| UAT environment | [Name, URL, build or version] |
| UAT window | [YYYY-MM-DD] to [YYYY-MM-DD] |
| UAT lead | [Name] |
| Business owner | [Name] |
| Plan version | [ ] |

### 1. Scope

In scope:

- [Workflows by role, for example admit from the emergency department, transfer between units, discharge]
- [Interfaces and integrations exercised end to end]
- [Reports and outputs that users rely on]
- [Access by role: each role sees and does only what it should]
- [Downtime and recovery: what users do while the system is unavailable, and back-entry afterwards]

Out of scope:

- [Performance, security and data migration testing, where other test phases cover them]
- [Features deferred to a later release]

### 2. Approach

[Number of cycles and what each covers, for example cycle 1 for core workflows, cycle 2 end to end with live interfaces, cycle 3 for regression of fixes. Where testing happens, for example a UAT room with clinicians booked in shifts.]

*Write scenarios as complete pieces of work a role does during a shift, not field-by-field checks. Field checks belong in system testing.*

### 3. Test environment and data

- Environment: [name], refreshed on [YYYY-MM-DD] and frozen until UAT exit.
- Test data: synthetic or de-identified patients only. Production PHI in UAT needs written approval from the privacy office and the same controls as production.
- Test accounts: one per tester for each role they test, so access is tested the way it will work in production.

Build test patients for the cases that cause clinical errors:

| Test patient | Purpose |
| --- | --- |
| [TP-01] | Child, for weight-based dosing |
| [TP-02] | Several allergies, including one to a drug class |
| [TP-03] and [TP-04] | Similar names and the same date of birth |
| [TP-05] | Newborn with a temporary name |
| [TP-06] | Merged record (two MRNs combined) |
| [TP-07] | Restricted record, such as an employee or a public figure |
| [TP-08] | Deceased patient |
| [TP-09] | Needs an interpreter; preferred name differs from legal name |

### 4. Entry criteria

- [ ] Build deployed to UAT and smoke-tested.
- [ ] System and integration testing complete, with no open S1 or S2 defects.
- [ ] Scenarios reviewed and approved by the business owner and the clinical reviewers.
- [ ] Test patients and test accounts ready for every role.
- [ ] Testers trained on the scenarios and the defect process.
- [ ] Clinical testers scheduled, with shift backfill agreed with their managers.

### 5. Exit criteria

- [ ] Every planned scenario executed; [N] percent passed against a target of [N] percent.
- [ ] No open S1 or S2 defects.
- [ ] No open defects with the clinical-safety flag.
- [ ] Every open S3 has a fix date or an accepted workaround.
- [ ] Every acceptance criterion traced to a passed scenario in the [traceability matrix](../03-requirements-and-design/requirements-traceability-matrix.md).
- [ ] Signed off by the business owner and by each clinical reviewer.

*A pass rate means little on its own. Ten failed scenarios out of 200 is fine if they are cosmetic and a serious problem if one of them is medication administration.*

### 6. Roles

| Role | Name | Responsibilities | Time needed |
| --- | --- | --- | --- |
| UAT lead | | Plans and runs UAT, tracks progress, reports daily | [Full time during UAT] |
| Business owner | | Accepts or rejects the release for the business | |
| Clinical reviewers, one per discipline (nursing, physicians, pharmacy, laboratory) | | Test clinical workflows, judge the clinical risk of defects, sign off clinical workflows | [Hours per week] |
| Testers (end users, by role) | | Run scenarios, record results and evidence | |
| QA lead | | Environment, test data, defect triage | |
| Product owner | | Prioritizes fixes | |
| Engineering | | Fixes defects and deploys builds to UAT | |

*Clinical reviewers are not testers with a different job title. Their job is to judge whether a result is clinically right and whether a defect could harm a patient. Book them for that, and don't let schedule pressure turn them into extra hands for data entry.*

### 7. Schedule

| Activity | Start | End | Owner |
| --- | --- | --- | --- |
| Scenario review | | | |
| Tester training | | | |
| Cycle 1 | | | |
| Cycle 2 | | | |
| Regression of fixes | | | |
| Sign-off | | | |

### 8. Test scenarios

| ID | Scenario | Role | Test patient | Expected result | Clinical reviewer | Result | Defect |
| --- | --- | --- | --- | --- | --- | --- | --- |
| UAT-001 | [A workflow from start to finish] | | [TP-01] | [What the tester should see] | [Yes / No] | [Pass / Fail / Blocked / Not run] | [ID] |
| UAT-002 | | | | | | | |

*Include scenarios that should fail: a user without access trying to open a restricted record, an order that should trigger an allergy warning, a duplicate registration that should be caught.*

### 9. Defects

Log defects in [tool] and rate them with the [defect severity guide](defect-severity-guide.md). In short:

| Rating | Meaning |
| --- | --- |
| S1 Critical | Unusable, data lost or corrupted, or one patient's data shown or filed as another's; no workaround |
| S2 High | A major function fails; the workaround is slow, error-prone or needs extra staff |
| S3 Medium | Works with a problem; a reasonable workaround exists |
| S4 Low | Cosmetic or minor |
| Clinical-safety flag | Set by a clinical reviewer, at any severity, when the defect could contribute to patient harm |

Triage: [daily at HH:MM during UAT], with the UAT lead, QA lead, product owner, engineering and, for flagged defects, a clinical reviewer.

*Never put real patient identifiers in a defect ticket, screenshots included. Use test patient IDs.*

### 10. Sign-off

| Role | Name | Decision | Conditions | Date |
| --- | --- | --- | --- | --- |
| Business owner | | [Accept / Accept with conditions / Reject] | | |
| Clinical reviewer, [discipline] | | | | |
| Clinical reviewer, [discipline] | | | | |
| QA lead | | | | |

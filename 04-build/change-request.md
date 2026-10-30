# Change request

## When to use it

Use it once scope, schedule and budget are baselined, for any change that would move one of them beyond the project manager's agreed tolerance, and for any change, however small, that alters a clinical workflow or the way patient data is handled. It gives the people who approve changes the same picture every time: what is being asked, why, what it costs in time, money and risk, what the alternatives are, and what the project recommends. Approved or rejected, the request stays on file, so nobody has to reconstruct later why the scope looks the way it does.

*This is the project change request, and it changes the plan. The production change ticket that the change advisory board approves before anything is deployed is a separate record; an approved scope change here will usually need one of those later.*

## Template

| Field | Value |
| --- | --- |
| CR ID | [CR-000] |
| Title | [Short and specific] |
| Requested by | [Name, role] |
| Date raised | [YYYY-MM-DD] |
| Prepared by | [Project manager] |
| Decision needed by | [YYYY-MM-DD, and why that date] |
| Status | [Draft / Under review / Approved / Rejected / Deferred] |

### 1. Description

[What would change, in plain words. What is included and what is not.]

### 2. Reason

[Why the change is needed now. Name the driver (regulation, clinical safety, a defect, a vendor change, a new stakeholder need, something learned in testing) and cite the source: a policy, a rule, an incident number, a meeting.]

### 3. Impact

| Area | Impact | Detail |
| --- | --- | --- |
| Scope | [None / Low / Medium / High] | [What is added, removed or changed] |
| Schedule | | [Milestones that move and by how much; the effect on go-live] |
| Cost | | [One-time and recurring; from contingency or new money] |
| Resources | | [Who is needed, and what they stop doing] |
| Quality and testing | | [Tests to add or rerun; UAT scenarios affected] |
| Risk | | [New or changed items in the RAID log] |
| Clinical workflow and safety | | [Who works differently; the clinical reviewer's view] |
| Privacy and security | | [New PHI flows, access changes, vendor agreements; whether the privacy and security review needs updating] |
| Training and communications | | [Who needs retraining or notice] |
| Other projects and systems | | [Interfaces, shared environments, other teams' plans] |

*Get the clinical and privacy rows from the clinical reviewer and the privacy office, not from the delivery team's best guess. A change that looks small to engineering can add a step for every nurse on every shift.*

### 4. Options

| Option | Description | Cost | Schedule effect | Risk | Notes |
| --- | --- | --- | --- | --- | --- |
| A. Don't make the change | [What happens if we carry on as planned] | | | | |
| B. [Make the change as requested] | | | | | |
| C. [A partial change, or defer it to a later release] | | | | | |

*Always include "don't make the change". It is a real option, and the approvers need to see what it costs.*

### 5. Recommendation

[The option the project recommends and why, in two or three sentences.]

### 6. Approval

Who can approve: [for example, the project manager approves changes within tolerance that have no clinical or PHI impact; the sponsor approves up to [N] days or $[amount]; the steering committee approves anything larger. A change to a clinical workflow also needs the clinical lead, and a change to how PHI is handled also needs security and the privacy office.]

| Role | Name | Decision | Date | Comments |
| --- | --- | --- | --- | --- |
| Sponsor | | [Approve / Reject / Defer] | | |
| Clinical lead | | | | |
| Security and privacy | | | | |
| [Other approver] | | | | |

### 7. After the decision

- [ ] Change log updated with the decision.
- [ ] Baseline, plan and budget updated (approved changes only).
- [ ] [RAID log](../02-planning/raid-log.md) updated.
- [ ] [Traceability matrix](../03-requirements-and-design/requirements-traceability-matrix.md) updated.
- [ ] [Privacy and security review](../03-requirements-and-design/privacy-and-security-review.md) updated, if data flows, roles or vendors changed.
- [ ] Requester and affected teams told.
- [ ] Production change ticket raised when the work is ready to deploy: [ticket ID].

# RACI matrix

## When to use it

Build it during planning, once the team and the main stakeholders are known, and look at it again before UAT and before go-live, which is when responsibilities blur fastest. Its real value is in the handful of activities where two groups each assume the other is handling something, or both believe they get the final say. The matrix below is filled in for a typical healthcare software release. Change the roles and rows to fit your project, and keep the rules.

## How to read it

- R (Responsible): does the work. A row can have more than one R.
- A (Accountable): owns the outcome and makes the final call. Exactly one per row.
- C (Consulted): asked before the work is done or the decision is made. A two-way conversation.
- I (Informed): told afterwards. One-way.

Where one role both does the work and owns the outcome, the cell reads A/R. A dash means no part in it.

*One A per row, always. If two people both believe they are the A, you have found the argument that would otherwise happen at 02:00 during cutover. Settle it now, with the sponsor if you need to.*

*The A must have the authority to make the call. If the accountable person needs someone else's permission, that someone is the real A.*

*Count the Cs. Each one is a person who can hold the work up, so ask whether each really needs to be asked first or only told afterwards. The go/no-go row is the exception: everyone speaks for their own area before the decision.*

## Template

| Activity | Sponsor | Project manager | Product owner | Engineering lead | QA lead | Clinical reviewer | Security and compliance | Support lead |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Approve release scope | A | C | R | C | I | C | I | I |
| Maintain the release plan and schedule | I | A/R | C | C | C | I | I | I |
| Keep the RAID log current | I | A/R | R | R | R | C | C | I |
| Write user stories and acceptance criteria | - | I | A/R | C | C | C | C | - |
| Review designs for clinical workflow and safety | - | I | C | C | I | A/R | - | - |
| Privacy and security review (PHI flows, access, audit logging) | I | I | C | R | - | - | A/R | - |
| Build and unit test | - | I | C | A/R | C | - | - | - |
| System and regression testing | - | I | C | C | A/R | - | - | - |
| Prepare UAT (scenarios, test patients, environment) | - | C | C | C | A/R | R | - | - |
| Accept UAT results for the business | I | I | A/R | - | C | C | - | I |
| Sign off clinical workflows in UAT | I | I | C | - | C | A/R | - | - |
| Set or clear the clinical-safety flag on a defect | - | I | C | I | C | A/R | - | - |
| Triage and prioritize defects | - | I | A | R | R | C | C | C |
| Raise the production change and present it to the change advisory board | I | R | I | A | C | - | C | C |
| Write and rehearse the cutover and rollback runbook | I | A | C | R | C | C | - | C |
| Prepare clinical downtime procedures and the back-entry plan | I | C | - | C | - | A/R | - | C |
| Brief the service desk and super-users | - | I | C | C | - | C | - | A/R |
| Release notes and go-live communications | I | A | R | C | - | C | - | C |
| Go/no-go decision | A | R | C | C | C | C | C | C |
| Call a rollback during cutover | A | R | C | C | I | C | I | C |
| Run hypercare triage and the daily huddle | I | A/R | C | R | C | C | - | R |
| Accept the handover to normal support | I | R | C | C | I | I | I | A |
| Run the lessons-learned review | I | A/R | C | C | C | C | C | C |

## Notes on this matrix

- The clinical reviewer is accountable for clinical sign-off and for the clinical-safety flag. Whether a defect could harm a patient is a clinical judgment, and the project cannot overrule it to protect a date.
- Security and compliance owns the privacy and security review; the engineering lead is responsible because they know the design and do most of the writing.
- The sponsor owns the go/no-go decision and the call to roll back. Cutovers often run overnight, so name a deputy for the rollback call in the runbook.
- The support lead is accountable for accepting the handover, not the project manager. Support has to live with whatever is handed over, so they decide when it's ready.
- On a project without clinical users, the clinical reviewer column becomes whoever can judge harm to the people the system serves; keep the column rather than dropping it.

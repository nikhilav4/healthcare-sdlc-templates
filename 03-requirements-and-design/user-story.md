# User story

## When to use it

Use it for every backlog item a delivery team will build, from the first refinement session until the product owner accepts the work. A good story names a real role, says what that role needs and why, and carries acceptance criteria that a tester and a clinician could each check without asking the author what was meant. A story that touches patient data or changes a clinical workflow needs two more things before it is ready: privacy, access and audit requirements written as acceptance criteria, and a named clinical reviewer.

## Template

| Field | Value |
| --- | --- |
| ID | [STORY-000] |
| Title | [Short and specific; starts with a verb] |
| Epic or feature | |
| Priority | |
| Estimate | [Points or size] |
| Touches patient data | [Yes / No] |
| Changes a clinical workflow | [Yes / No] |
| Clinical reviewer | [Name and discipline, or "not needed"] |

### Story

As a [specific role, for example charge nurse, outpatient scheduler, pharmacist],
I want [capability],
so that [benefit to the role, the patient or the organization].

*"As a user" tells the team nothing. Name the role: a nurse on a medical-surgical unit at 03:00 and a scheduler at a front desk need different things from the same screen.*

### Context

[Why this matters now, what happens today, and links to designs, policies or source documents.]

### Acceptance criteria

*Write each criterion as Given, When, Then, so it can be tested exactly as written. Include at least one case where the system should refuse, block or warn.*

1. Given [starting state], when [action], then [observable result].
2. Given [ ], when [ ], then [ ].
3. Given [ ], when [ ], then [ ].

### Non-functional requirements

- Performance: [for example, the screen opens in under two seconds at peak load]
- Access: [which roles can see and change this data]
- Audit: [which actions on patient data are logged]
- Accessibility: [ ]
- Downtime: [what users do if this function is unavailable]

### Out of scope

- [What this story deliberately does not do]

### Dependencies

- [Other stories, interfaces, vendor deliverables]

## Definition of Ready

A story can come into a sprint when:

- [ ] It names a real role and states the benefit.
- [ ] Acceptance criteria are written as Given, When, Then and QA has reviewed them.
- [ ] It fits in one sprint, or has been split until it does.
- [ ] Designs are attached wherever the screen changes.
- [ ] Dependencies are known and none blocks the start.
- [ ] If it touches patient data: the data elements are listed and access and audit criteria are written.
- [ ] If it changes a clinical workflow: a clinical reviewer is named and has read the criteria.
- [ ] Test data is available, using synthetic patients only.

## Definition of Done

A story is done when:

- [ ] The code is reviewed and merged.
- [ ] Automated tests cover the acceptance criteria and pass.
- [ ] QA has tested it in [environment].
- [ ] The product owner has accepted it against the acceptance criteria.
- [ ] The clinical reviewer has accepted it, if one is named.
- [ ] No PHI appears in application logs, error messages or analytics from the new code.
- [ ] Audit events are written and checked wherever the story requires them.
- [ ] Release notes and user guidance are updated.
- [ ] The traceability matrix links the story to its requirement and its tests.

*The last four are the ones teams skip under deadline pressure, and the ones an auditor or a privacy investigation asks about first.*

## Example: audit logging on patient data

*Illustrative only. Confirm audit and retention requirements with your privacy and security officers.*

| Field | Value |
| --- | --- |
| ID | STORY-214 |
| Title | Record every view of a patient's medication history |
| Epic or feature | Medication history |
| Priority | Must have for release |
| Estimate | 5 points |
| Touches patient data | Yes |
| Changes a clinical workflow | No |
| Clinical reviewer | Not needed; the privacy officer reviews |

### Story

As a privacy officer,
I want every view of a patient's medication history recorded with who opened it, when and from where,
so that I can investigate suspected inappropriate access to a patient's record.

### Context

The HIPAA Security Rule's audit controls standard (45 CFR 164.312(b)) requires mechanisms that record and examine activity in systems holding electronic PHI. The medication history screen and its API are new in this release, so nothing records access to them yet.

### Acceptance criteria

1. Given a signed-in clinician with access to the patient, when they open the patient's medication history, then an audit event is written with the user ID, the patient's MRN, the action "view", a UTC timestamp, the workstation or IP address, and the screen name.
2. Given a client reads the medication history through the API, when the request succeeds, then the same audit event is written, with the API client ID in place of the screen name.
3. Given an audit event exists, when any user, including a system administrator, tries to change or delete it through the application, then the change is refused and the attempt is itself logged.
4. Given an audit event is written, then it holds identifiers and metadata only, with no clinical content such as medication names or doses.
5. Given the audit service is unavailable, when a clinician opens the medication history, then the screen still opens, the event is queued and written once the service recovers, and no events are lost.
6. Given a privacy officer searches the audit log by MRN and a date range of up to 90 days, when the search runs, then every view of that patient's medication history in the range is returned, newest first, within 10 seconds.

### Non-functional requirements

- Performance: writing the audit event adds no more than 50 ms to opening the screen.
- Access: only the privacy office role can search the audit log.
- Retention: [the period set by the organization's records retention policy].

*Criterion 5 is a clinical decision as much as a technical one: the team chose not to block care when the audit service is down. Get choices like that agreed with the privacy officer and the clinical lead and write them into the story, instead of leaving them to whoever writes the error handling.*

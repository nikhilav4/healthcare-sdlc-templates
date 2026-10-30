# Project charter

## When to use it

Write the charter once the sponsor has agreed the project should start and before anyone commits money or people to it. It is the document the steering committee approves, and the one you go back to when someone asks whether a request is in scope, who can approve a slip, or what success was supposed to look like. Keep it to a few pages and link out to anything longer. On a healthcare project the charter is also the first time the privacy office, security and clinical leadership see what the project will touch, so fill in the compliance section even when some answers are still "to be confirmed".

## Template

| Field | Value |
| --- | --- |
| Project | [Project name] |
| Version | [0.1] |
| Date | [YYYY-MM-DD] |
| Sponsor | [Name, role] |
| Project manager | [Name] |
| Status | [Draft / Approved] |

### 1. Purpose

[One or two sentences: what the project will change, and for whom.]

*Write this for someone outside IT. "Replace the interface engine" is a task. "Get admissions, transfers and discharges onto the bed board in real time so bed managers stop phoning units" is a purpose.*

### 2. Background

[Why now. What happens today, what it costs or risks, and what triggered the project: a vendor end-of-support date, a regulatory deadline, a patient-safety event, a contract renewal, a strategic plan.]

### 3. Objectives

*Make each objective specific, measurable, achievable, relevant and time-bound. If the sponsor could not check it at closure without asking you what it meant, rewrite it.*

| # | Objective | Measure | Baseline | Target | By when |
| --- | --- | --- | --- | --- | --- |
| O1 | [Outcome in plain words] | [What you will count or time] | [Today's value] | [Value that means success] | [YYYY-MM-DD] |
| O2 | | | | | |
| O3 | | | | | |

### 4. Scope

In scope:

- [Sites, departments and care settings, for example inpatient units, emergency department, outpatient clinics]
- [Systems, interfaces and integrations]
- [Data to migrate, including how many years of history]
- [User roles affected]
- [Training, documentation and handover to support]

Out of scope:

- [Anything a reasonable stakeholder might expect and won't get: other sites, a later phase, history beyond the cutoff, reports nobody has asked for yet]

*The out-of-scope list settles more arguments than the in-scope list. If you can picture someone being surprised that it isn't included, write it down.*

### 5. Deliverables

| Deliverable | Description | Accepted by | Target date |
| --- | --- | --- | --- |
| [Deliverable] | [What it is, in one line] | [Name, role] | [YYYY-MM-DD] |
| | | | |

### 6. Success measures

*Take the baseline before go-live. Once the old system is switched off, the numbers you needed are usually gone with it.*

| Measure | Data source | Baseline | Target | Measured when | Owner after closure |
| --- | --- | --- | --- | --- | --- |
| [For example, median minutes from ED admit decision to bed assignment] | [System or report] | [Value, date taken] | [Value] | [30 and 90 days after go-live] | [Name, role] |
| | | | | | |

### 7. Stakeholders

| Stakeholder | Role in the project | What they need from it | Influence | How we engage them |
| --- | --- | --- | --- | --- |
| [Sponsor] | [Approves scope, budget and go-live] | | [High] | [Weekly status report, steering] |
| [Clinical leadership, for example CMIO, CNO] | [Clinical decisions and sign-off] | | | |
| [Frontline staff, by role and shift] | [End users] | | | [Unit huddles, super-users] |
| [Privacy office and information security] | [Review how patient data is handled] | | | [Design reviews] |
| [Vendors] | | | | |

*List night, weekend and agency staff as their own group if go-live touches them. They miss daytime training and town halls, and they are the ones on shift during cutover.*

### 8. Governance

| Role | Name | Decides |
| --- | --- | --- |
| Sponsor | [Name] | [Scope, budget, go-live date, go/no-go] |
| Steering committee | [Members] | [Changes beyond the project manager's tolerance; escalations] |
| Clinical lead | [Name] | [Clinical workflow and patient-safety questions] |
| Project manager | [Name] | [Day-to-day delivery within agreed tolerances] |

Steering committee cadence: [for example, every two weeks, weekly in the last month before go-live]

Project manager tolerance: [for example, may move a milestone by up to five working days, or release up to $[amount] of contingency, without going to steering, provided go-live does not move]

Escalation path:

| Level | Who | Escalate when | Expected response |
| --- | --- | --- | --- |
| 1 | Workstream lead | [The problem can't be solved inside the workstream] | [1 working day] |
| 2 | Project manager | [It threatens a milestone or crosses workstreams] | [2 working days] |
| 3 | Sponsor | [It threatens go-live, budget or scope, or needs a decision beyond the PM's tolerance] | [ ] |
| 4 | Steering committee | [The sponsor can't resolve it alone] | [Next meeting, or called ad hoc] |
| Clinical safety | Clinical lead | [Anything that could harm a patient] | [Same day, by phone] |

*A possible patient-safety problem does not climb the ladder one rung at a time. It goes straight to the clinical lead, the same day.*

Phase gates:

| Gate | What has to be true | Approved by | Target date |
| --- | --- | --- | --- |
| Charter approved | [This document signed] | [Sponsor] | |
| Plan baselined | [Schedule, RACI, RAID log and communication plan agreed] | [Sponsor] | |
| Privacy and security review | [PHI data flows, access design and audit logging approved before build starts] | [Security, privacy office] | |
| UAT sign-off | [Business owner and clinical reviewers accept the release] | [Business owner, clinical lead] | |
| Production change approved | [Change advisory board approves the cutover window] | [Change advisory board] | |
| Go/no-go | [Go-live readiness checklist complete; decision recorded] | [Sponsor] | |
| Hypercare exit | [Exit criteria met; support accepts the handover] | [Sponsor, support lead] | |
| Closure | [Closure report signed] | [Sponsor] | |

### 9. Milestones

| Milestone | Target date | Owner | Notes |
| --- | --- | --- | --- |
| [Kickoff] | [YYYY-MM-DD] | | |
| [Design complete] | | | |
| [Build complete] | | | |
| [UAT complete] | | | |
| [Go-live] | | | |
| [Hypercare exit] | | | |

*Check the go-live date against the organization's calendar before you publish it: holidays and holiday staffing, respiratory-season census, July resident changeover in teaching hospitals, month-end close for revenue cycle systems, accreditation survey windows, and other changes already booked for the same weekend.*

### 10. Budget

| Category | One-time | Recurring (annual) | Notes |
| --- | --- | --- | --- |
| Internal labor | | | |
| Vendor and professional services | | | |
| Licenses and subscriptions | | | |
| Infrastructure and hosting | | | |
| Training, including backfill for clinical staff | | | |
| Go-live support (command center, at-the-elbow support) | | | |
| Contingency | | | [Who can release it] |
| Total | | | |

*Budget for backfill. When nurses or pharmacists train on paid time, someone covers their shift, and that cost lands on a department's budget unless the project planned for it.*

### 11. Assumptions and constraints

Assumptions (copy each into the RAID log with a date to confirm it by):

- [For example: the vendor's test environment is available from [YYYY-MM-DD]]

Constraints:

- [Fixed dates, budget caps, change freezes, staffing limits, contract terms]

### 12. Compliance considerations

PHI data flows:

| Flow | PHI involved | From | To | How it moves | Agreement in place |
| --- | --- | --- | --- | --- | --- |
| [For example, admissions feed] | [Demographics, encounter details] | [System] | [System] | [HL7 v2 over VPN, FHIR API, SFTP] | [Business associate or data-sharing agreement, date] |
| | | | | | |

Questions to answer before build starts:

- Will any non-production environment (test, training, reporting) hold real patient data? If so, who approved it and what controls apply?
- Which vendors will be able to see PHI, and is a business associate agreement signed with each?
- Does any of the data fall under rules stricter than HIPAA, such as substance use disorder records under 42 CFR Part 2, or state laws on mental health or HIV status?
- How will access to patient records be logged, and who reviews the logs?

Security review:

| Review | Owner | Needed by | Status |
| --- | --- | --- | --- |
| Privacy and security review of the design | [Security, privacy office] | [Before build starts] | |
| Vendor security assessment | | | |
| Penetration test or vulnerability scan | | [Before go-live] | |

*Book the security review when you write the charter. Review queues in large organizations run for weeks, and a late review is one of the most common reasons a go-live date moves.*

Clinical safety:

[Does the project change how clinicians order, document, give medication or receive results? If yes, name a clinical reviewer for each affected discipline and say when they will review designs and sign off UAT.]

### 13. Initial risks

*Write each risk as a cause and an effect: "If the vendor misses the test window, integration testing runs into UAT." These seed the RAID log. Manage them there from now on, not here.*

| ID | Risk | Probability (1-5) | Impact (1-5) | Owner | Response |
| --- | --- | --- | --- | --- | --- |
| R-001 | | | | | |
| R-002 | | | | | |

### 14. Approvals

| Role | Name | Approved | Date | Comments |
| --- | --- | --- | --- | --- |
| Sponsor | | [Yes / No] | | |
| Clinical lead | | | | |
| IT leadership | | | | |
| Privacy and security | | | | |
| Finance | | | | |

*An approval by email counts if the email is filed with the charter. A nod in a meeting counts only if the minutes record it.*

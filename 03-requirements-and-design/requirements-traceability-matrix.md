# Requirements traceability matrix

## When to use it

Start it as soon as requirements are agreed and keep it current through build, testing and release. It links each requirement to where it came from, how it was designed, which story built it, which tests prove it and whether users accepted it. Most weeks it sits in the background. It earns its keep at three moments: when someone asks whether a clinical requirement was really tested before go-live, when an auditor asks you to show it, and when a requirement changes and you need to know which tests to run again.

## Why it matters in healthcare

- Clinical safety. A requirement such as "warn when a drug is ordered for a patient with a documented allergy to its class" is only safe if someone tested it with the right test patients and a clinician accepted the result. The matrix shows that chain for every requirement with clinical risk, instead of leaving it to memory.
- Audits and investigations. Internal audit, an accreditation surveyor or a privacy investigation may ask how you know a control works. A traceability record answers in minutes rather than days.
- Change impact. When a requirement, a policy or a regulation changes, the matrix shows which designs, stories and tests it touches.
- Regulated software. If the product is regulated as a medical device, your quality system will require traceability in a form it defines. Use that; this template doesn't replace it.

## Template

| Field | Value |
| --- | --- |
| Project or release | [Name] |
| Owner | [Business analyst or QA lead] |
| Updated | [YYYY-MM-DD] |

| Req ID | Requirement | Source | Clinical risk | Design reference | Story | Test cases | Test result | UAT result | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| REQ-001 | [One testable statement] | [Policy, regulation, stakeholder, incident] | [Yes / No] | [Design document and section] | [STORY-000] | [TC-000, TC-001] | [Pass / Fail / Not run] | [Accepted / Rejected / Not run] | [Status] |
| REQ-002 | | | | | | | | | |

Status values: Draft, Approved, In build, Built, Tested, Accepted, Deferred (with the change request ID), Withdrawn.

*One requirement per row. "The system shall do A and B" becomes two rows, because A can pass while B fails.*

*Mark clinical risk as Yes when getting the requirement wrong could affect diagnosis, treatment, medication, results or patient identification. Those rows need a UAT result from a clinical reviewer, not only from the business owner.*

### Example rows

| Req ID | Requirement | Source | Clinical risk | Design reference | Story | Test cases | Test result | UAT result | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| REQ-014 | An allergy warning appears when a medication is ordered for a patient with a documented allergy to its drug class | Pharmacy and therapeutics committee policy | Yes | Ordering design 3.2 | STORY-118 | TC-301, TC-302, TC-303 | Pass | Accepted by pharmacist reviewer | Accepted |
| REQ-022 | Every view of a patient's medication history is written to the audit log | HIPAA Security Rule audit controls; privacy office | No | Audit design 2.1 | STORY-214 | TC-410 to TC-415 | Pass | Accepted by privacy officer | Accepted |
| REQ-031 | Shared clinical workstations lock after [N] minutes idle | Information security policy | No | Security design 4.4 | STORY-162 | TC-520 | Fail | Not run | In build |
| REQ-040 | Discharge summaries can be faxed from the application | Request from a clinic manager | No | | | | | | Deferred (CR-006) |

### Coverage checks

Run these before every phase gate.

| Check | Result |
| --- | --- |
| Approved requirements with no test case | [Count and IDs] |
| Test cases that trace to no requirement | [Count and IDs] |
| Clinical-risk requirements without a clinical reviewer's UAT result | [Count and IDs] |
| Requirements deferred without a change request | [Count and IDs] |
| Requirements planned for this release with a failed or unrun test | [Count and IDs] |

*A test with no requirement behind it is a warning sign, not a bonus. Either a requirement is missing from the matrix, or the team is testing something nobody asked for.*

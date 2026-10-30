# Hypercare plan

## When to use it

Write it before the go/no-go meeting, because the decision depends on it, and run it from the moment cutover closes until the exit criteria are met. Hypercare is the period of extra support straight after go-live, when users are still learning, small configuration problems surface and the project team still owns the outcome. The plan sets how long it lasts, who supports whom, how issues are triaged, how a clinical safety concern is escalated, which numbers are watched, and what has to be true before normal support takes over.

## Template

| Field | Value |
| --- | --- |
| Release | [Name, version] |
| Hypercare starts | [YYYY-MM-DD HH:MM] |
| Planned end | [YYYY-MM-DD] |
| Hypercare lead | [Name] |
| Command center | [Location, bridge line, hours] |

### 1. Duration and exit criteria

Planned length: [for example, two weeks for most releases and longer for a large clinical go-live]. Hypercare ends when the exit criteria are met, not when the date arrives.

| Exit criterion | Target | Status |
| --- | --- | --- |
| Open S1 defects or incidents | None for [5] consecutive days | |
| Open S2 | None, or each with a workaround and fix date that support accepts | |
| Open items with the clinical-safety flag | None | |
| Daily ticket volume | Below [N] for [3] consecutive days | |
| Back-entry of downtime records | Complete and checked | |
| Interface error queue | Cleared daily; no message older than [N] hours | |
| Knowledge articles | Published for every recurring issue | |
| Support handover | Accepted by the support lead | |

*Agree the exit criteria before go-live. Once hypercare starts, everyone is tired and the pull to declare victory is strong.*

### 2. Support model

| Tier | Who | Handles | Hours |
| --- | --- | --- | --- |
| At the elbow | Super-users and project staff on the units | How-to questions, quick fixes, spotting problems early | [Days 1 to N, all shifts] |
| Tier 1 | Service desk | Logging, passwords and access, known issues | [24/7] |
| Tier 2 | Project team in the command center | Configuration, data fixes, triage | [Hours; on call outside them] |
| Tier 3 | Engineering and vendor | Code fixes, infrastructure | [On call] |

Roster:

| Date | Shift | Command center | At the elbow | On call |
| --- | --- | --- | --- | --- |
| [YYYY-MM-DD] | [Day / Evening / Night] | [Names] | [Names and units] | [Names] |

*Staff the night shift as well as the day. Night staff get the least training and have the fewest experts nearby, so problems often show up there first.*

### 3. Daily huddle

When: [for example 08:30 and 16:30 in the first week, then once a day], [location or bridge], [15 to 30 minutes].

Who: hypercare lead, clinical lead or delegate, engineering, interface team, support lead, super-user lead, vendor.

Agenda:

1. Safety first: any clinical safety concern raised since the last huddle.
2. Open S1 and S2 issues: owner, status, next step.
3. Metrics against their thresholds.
4. Themes from tickets and from the units.
5. Decisions needed, and messages to send to staff.

### 4. Issue triage

Every issue is logged as a ticket tagged [hypercare tag], including the ones raised in person on a unit.

| Rating | First response | Updates | Fix target |
| --- | --- | --- | --- |
| S1, or clinical-safety flag | [15 minutes] | [Hourly] | [Hours; hotfix] |
| S2 | [1 hour] | [At each huddle] | [Days] |
| S3 | [Next huddle] | [Daily] | [A planned release] |
| S4 | [Weekly review] | | [Backlog] |

Severity and the clinical-safety flag follow the [defect severity guide](../05-testing/defect-severity-guide.md).

### 5. Clinical escalation path

If anyone believes a patient is at risk because of the system:

1. Make the patient safe first, using downtime procedures if needed.
2. Call the command center on [number], at any hour.
3. The command center calls the clinical lead on call ([name, number]) straight away.
4. The clinical lead decides on containment: a workaround, a warning to the units, or taking a function out of use.
5. The event is reported through the organization's patient-safety reporting process, and the report number goes in the ticket.

Who can send a unit, or the whole organization, back to downtime procedures: [role, and deputy], and how that is announced: [channel].

*Make sure every unit knows the command center number before go-live. Staff who worry about bothering someone won't call, so tell them plainly that a call which turns out to be nothing was still the right call.*

### 6. Metrics to watch

| Metric | Source | Threshold for concern | Owner |
| --- | --- | --- | --- |
| Tickets opened per day, by category | [Service desk] | | |
| Open S1 and S2 | [Defect tracker] | [Any S1] | |
| Interface error queue depth and oldest message | [Interface engine] | | |
| Failed sign-ins and access requests | [Identity system] | | |
| Back-entry backlog | [Unit reports] | | |
| Time for results to reach the chart | [Interface or lab system] | | |
| Outages and slow response | [Monitoring] | | |
| [An adoption measure, for example the share of orders entered electronically] | | | |

### 7. Handover to normal support

- [ ] Open issues transferred, each with an owner and a due date.
- [ ] Knowledge articles and runbooks handed to support.
- [ ] Monitoring and alerts routed to the operations team.
- [ ] Vendor support contacts and contract terms shared.
- [ ] Project team access cut back to what normal support needs.
- [ ] Exit agreed by the sponsor and the support lead on [YYYY-MM-DD].

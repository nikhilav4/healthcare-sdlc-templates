# Cutover and rollback runbook

## When to use it

Write it once the release scope is stable, rehearse it at least once in a production-like environment with a stopwatch running, and run the cutover from it line by line. It is the one plan everyone follows during the cutover window: what happens in what order, who does it, how each step is checked, where the go/no-go checkpoints fall, what clinical areas do while the system is unavailable, and exactly when and how to roll back. If a step isn't in the runbook, nobody does it during cutover.

## Template

| Field | Value |
| --- | --- |
| Release | [Name, version] |
| Production change ticket | [Approved change ID] |
| Cutover window | [YYYY-MM-DD HH:MM] to [YYYY-MM-DD HH:MM] |
| Clinical downtime window | [HH:MM] to [HH:MM] |
| Cutover lead | [Name] |
| Decision owner | [Name]; deputy for overnight decisions: [name] |
| Command center | [Room, bridge line, chat channel] |
| Rehearsals | [Date, duration, result for each] |

*Times are relative to T, the moment users lose the ability to save in the old system. Record actual durations at every rehearsal; a step that took 40 minutes in rehearsal will not take 20 on the night.*

### 1. Contacts

| Role | Name | Phone | Backup |
| --- | --- | --- | --- |
| Cutover lead | | | |
| Decision owner | | | |
| Engineering lead | | | |
| Interface analyst | | | |
| Database administrator | | | |
| Clinical lead on call | | | |
| Nursing supervisor | | | |
| Service desk lead | | | |
| Vendor on call | | | |

### 2. Before cutover

| # | When | Task | Owner | Done |
| --- | --- | --- | --- | --- |
| P1 | T-7 days | Change freeze in force on affected systems | | |
| P2 | T-2 days | Go/no-go meeting held and the decision recorded | | |
| P3 | T-1 day | Downtime reports printed, or loaded on standalone downtime computers, for every affected unit | | |
| P4 | T-1 day | Downtime forms and back-entry instructions on every unit | | |
| P5 | T-4 hours | Full backup taken and verified | | |
| P6 | T-1 hour | Final reminder sent to units; command center open | | |

### 3. Cutover timeline

| # | Start | Duration | Step | Owner | How it is checked | Actual |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | T-00:30 | 15 min | Checkpoint A, go to start: every lead confirms ready | [Decision owner] | Each lead says go on the bridge | |
| 2 | T | 5 min | Old system set to read-only; units start downtime procedures | | A test user can't save | |
| 3 | T+00:05 | | Interfaces stopped and queues drained | | Queue depth zero | |
| 4 | | | Final data extract and load | | Record counts reconcile | |
| 5 | | | Checkpoint B, data verified: clinicians spot-check sample charts | [Decision owner] | Reconciliation report; clinical spot-check signed | |
| 6 | | | Application deployed and configured | | Smoke tests pass | |
| 7 | | | Interfaces started; test messages sent end to end | | Messages received and filed correctly | |
| 8 | | | Checkpoint C, point of no return: go forward or roll back | [Decision owner] | Rollback triggers reviewed | |
| 9 | | | Users given access; units end downtime | | Super-users confirm on each unit | |
| 10 | | | Back-entry of downtime records starts | | Back-entry log | |
| 11 | | | Cutover closed; hypercare begins | [Cutover lead] | Handover to the command center | |

*Put the point of no return where a rollback still fits inside the downtime window, using the rollback time measured in rehearsal. After that point, problems get fixed forward.*

### 4. Downtime procedures for clinical areas

| Area | During downtime | Information available | After go-live | Owner |
| --- | --- | --- | --- | --- |
| Inpatient units | [Paper medication administration record, paper orders, downtime documentation forms] | [Downtime reports: medications, active orders, allergies] | [Back-enter medication administration and vital signs by HH:MM] | [Unit manager] |
| Emergency department | [Downtime registration with pre-assigned numbers; paper tracking board] | | [Register patients properly; merge the temporary numbers] | |
| Pharmacy | [Verify paper orders; dispense under the downtime process] | | [Reconcile orders placed during downtime] | |
| Laboratory | [Phone critical results to units; paper requisitions] | | [File results in the new system and check them] | |
| Outpatient clinics | [Read-only schedule; paper visit notes] | | | |
| Registration and bed management | | | | |

*Every record created on paper needs a named person to enter it afterwards and a deadline to do it by. Back-entry with no owner is still waiting a week later, and the chart is incomplete until it's done.*

*Critical lab results are phoned to the unit during downtime, never left on paper in the lab. Confirm the read-back process with the laboratory before the night.*

### 5. Rollback

Triggers (any one is enough to consider rolling back at a checkpoint):

- [Data reconciliation fails beyond the agreed tolerance, or the clinical spot-check finds wrong-patient data or missing allergies]
- [A core clinical function (ordering, results, medication administration) fails smoke testing]
- [Interfaces can't pass test messages end to end by T+HH:MM]
- [Cutover is running more than [N] minutes behind the point of no return]

Decision owner: [name]. Deputy, if the decision owner can't be reached within 10 minutes: [name].

| # | Step | Owner | Duration in rehearsal | How it is checked |
| --- | --- | --- | --- | --- |
| RB1 | Announce the rollback on the bridge and to the units | | | |
| RB2 | Stop interfaces to the new system | | | |
| RB3 | Return the old system to read-write | | | |
| RB4 | Re-point interfaces to the old system and replay queued messages | | | |
| RB5 | Smoke-test the old system, including a test order and a test result | | | |
| RB6 | Units end downtime on the old system; back-entry plan for the old system | | | |
| RB7 | Record what happened and set the date of the next attempt | | | |

*A rollback plan that hasn't been rehearsed is a hope. Rehearse it separately from the cutover, re-pointing of interfaces included, because that is the step most often forgotten.*

### 6. Communication points

| When | Audience | Message | Channel | Sender |
| --- | --- | --- | --- | --- |
| T-1 day | All affected staff | Downtime starts at [time]; what to do; the command center number | | |
| T-00:15 | Units, emergency department, pharmacy, laboratory | Downtime starts in 15 minutes | [Overhead page, secure message] | [Command center] |
| Each checkpoint | Leads and sponsor | Checkpoint result and decision | [Bridge, chat] | [Cutover lead] |
| End of downtime | All affected staff | The system is live; back-entry instructions; where to get help | | |
| If rolling back | All affected staff | Staying on the old system, and what to do now | | |
| T+[N] hours | Sponsor and leadership | Cutover summary | | [Cutover lead] |

### 7. Sign-off

| Role | Name | Runbook reviewed | Date |
| --- | --- | --- | --- |
| Cutover lead | | | |
| Engineering lead | | | |
| Clinical lead | | | |
| Support lead | | | |
| Decision owner | | | |

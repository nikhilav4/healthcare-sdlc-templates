# RAID log

## When to use it

Start it the day the charter is approved, seed it from the charter's initial risks and assumptions, and review it every week with the workstream leads; the top of it goes to every steering meeting. A RAID log is only as good as its review dates. An item nobody has looked at in a month is a guess, not a record. The fields here match the YAML register read by [raid-log](https://github.com/nikhilav4/raid-log), so the same register can live in a spreadsheet, a wiki page or a YAML file next to the code without losing anything when it moves.

## The four types

| Type | What it is | The question to answer |
| --- | --- | --- |
| Risk | Something that hasn't happened and might | How likely, how bad, and what are we doing about it now? |
| Assumption | Something the plan treats as true that nobody has confirmed | Who will confirm it, and by when? |
| Issue | Something that has happened and needs handling | How serious is it, and who is fixing it? |
| Dependency | Something the project needs from a person or team outside it | Who delivers, and on what date does our plan break without it? |

*When a risk happens, raise a new issue, link the two, and close the risk with a resolution that names the issue. Don't change the risk's type: the record of what you saw coming is worth keeping.*

*An assumption that is still unconfirmed on its validate-by date has become a risk. Raise one.*

## Scoring risks

Probability:

| Score | Label | Rough likelihood |
| --- | --- | --- |
| 1 | Rare | Under 10 percent |
| 2 | Unlikely | 10 to 30 percent |
| 3 | Possible | 30 to 50 percent |
| 4 | Likely | 50 to 80 percent |
| 5 | Almost certain | Over 80 percent |

Impact (score the worst column that applies):

| Score | Schedule | Cost | Scope and quality | Patient safety and compliance |
| --- | --- | --- | --- | --- |
| 1 | Absorbed by the team's slack | Within the workstream budget | Users won't notice | None |
| 2 | A task slips; no milestone moves | Small draw on contingency | Minor workaround for a few users | Minor procedural gap; no PHI exposed |
| 3 | A milestone moves; go-live holds | Most of the contingency | Workaround for a whole role or department | Extra steps for clinicians; a privacy or security finding to fix |
| 4 | Go-live moves | Needs the sponsor to approve more money | A committed feature misses go-live | Clinical workflow degraded; a compliance finding that needs formal remediation |
| 5 | Can't deliver without re-planning | Needs a new funding decision | Release not fit for use | Could contribute to patient harm, or a reportable privacy breach |

Exposure is probability times impact, from 1 to 25:

| Exposure | Band | What it means |
| --- | --- | --- |
| 20 to 25 | Critical | On the steering agenda every meeting until it drops |
| 12 to 16 | High | Must have a mitigation; reviewed weekly |
| 5 to 10 | Moderate | Owner reviews it by its review date |
| 1 to 4 | Low | Watch |

*Exposure ranks risks; it doesn't triage them. A risk scored 1 x 5 on patient safety still belongs in front of the clinical lead, however far down the list it sits.*

## Issue severity

| Severity | Meaning |
| --- | --- |
| critical | Could harm a patient, exposes PHI, or stops go-live with no workaround |
| high | Blocks a milestone or a clinical workflow; the workaround is costly or fragile |
| medium | Slows the work; a reasonable workaround exists |
| low | A nuisance; fix when convenient |

## Status

| Status | Use it when |
| --- | --- |
| open | Logged; no response under way yet |
| monitoring | Being watched; nothing to do unless something changes |
| mitigating | Actions are under way |
| resolved | Fixed, or the response worked; waiting to confirm it stays that way |
| closed | Nothing left to do, including risks that passed without happening |

## Rules

These are the checks `raid validate` runs, so a register that follows them passes.

- Every item has one named owner. A team is not an owner.
- Every open, monitoring or mitigating item has a review-by date.
- A risk with exposure 12 or more has a mitigation.
- Resolved and closed items record a resolution.
- A dependency names the counterparty and a need-by date.
- An assumption has a validate-by date.
- IDs are R-, A-, I- or D- followed by at least three digits, and are never reused.

*Keep PHI out of the RAID log. Describe the problem, not the patient, and refer to incidents by ticket number. The register is shared widely and kept for years.*

*The RAID log is not the patient-safety event reporting system. If something reached a patient, or nearly did, report it through the organization's process and put the report number in the item.*

## Template

| Field | Value |
| --- | --- |
| Project | [Project name] |
| Updated | [YYYY-MM-DD] |
| Register owner | [Project manager] |

### Risks

| ID | Risk | Owner | Status | Raised | Review by | P | I | Exposure | Mitigation | Contingency | Links |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| R-001 | [What might happen and what it would hit] | [Name] | [open] | [YYYY-MM-DD] | [YYYY-MM-DD] | [1-5] | [1-5] | [P x I] | [What we are doing now] | [What we'll do if it happens] | [D-001] |
| R-002 | | | | | | | | | | | |

### Assumptions

| ID | Assumption | Owner | Status | Raised | Validate by | Review by | How it will be confirmed |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A-001 | [What the plan takes as true] | [Name] | [open] | [YYYY-MM-DD] | [YYYY-MM-DD] | [YYYY-MM-DD] | |

### Issues

| ID | Issue | Owner | Status | Severity | Raised | Review by | Action and next step | Links |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| I-001 | [What has gone wrong] | [Name] | [open] | [low / medium / high / critical] | [YYYY-MM-DD] | [YYYY-MM-DD] | | |

### Dependencies

| ID | Dependency | Owner | Counterparty | Need by | Status | Review by | Links |
| --- | --- | --- | --- | --- | --- | --- | --- |
| D-001 | [What we need] | [Name on our side] | [Team or vendor] | [YYYY-MM-DD] | [open] | [YYYY-MM-DD] | [R-001] |

### Resolved and closed

| ID | Title | Status | Closed on | Resolution |
| --- | --- | --- | --- | --- |
| | | [resolved / closed] | [YYYY-MM-DD] | [What happened; name the issue if a risk turned into one] |

*Move items here when they close rather than deleting them. Next year's project will want to know what this one worried about.*

## Keeping it as YAML

[raid-log.yaml](raid-log.yaml) is the same register as a YAML starter, with one item of each type and one closed item. [raid-log](https://github.com/nikhilav4/raid-log) validates it, writes the steering report, draws a probability and impact heatmap, and shows what changed since the last meeting:

```bash
raid validate raid-log.yaml
raid report raid-log.yaml --since 2026-11-02
```

The YAML has no column for "How it will be confirmed"; put that in the assumption's description. It has fields the tables here leave out to stay readable: description, workstream, tags, source and a dated log. Use them if you keep the register as YAML.

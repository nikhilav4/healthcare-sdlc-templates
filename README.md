# Healthcare IT project templates

Templates for running a healthcare IT software project through the SDLC, from charter to hypercare.

Generic project templates treat a release as done when it ships. In a hospital or clinic it is done when clinicians can work safely with it, and that takes a privacy and security review before build, clinical sign-off in UAT, a defect scale that rates clinical risk apart from technical severity, and downtime procedures for the hours the system is unavailable. These templates put each of those checks in the phase where it belongs. I run Agile delivery for a healthcare software platform, where release readiness and UAT with clinical reviewers decide whether a release goes out, and the templates are written for that kind of work.

## The SDLC map

| Phase | What it is for | Templates | Gate that ends it |
| --- | --- | --- | --- |
| 00 Every phase | Keep the sponsor and the team current, and record what was decided | [Weekly status report](00-every-phase/weekly-status-report.md), [meeting minutes](00-every-phase/meeting-minutes.md) | None; these run from kickoff to closure |
| 01 Initiation | Agree why the project exists, what it covers and who decides | [Project charter](01-initiation/project-charter.md) | Charter signed by the sponsor |
| 02 Planning | Set roles, track risks, and plan how each group hears about the work | [RACI matrix](02-planning/raci-matrix.md), [RAID log](02-planning/raid-log.md) with a [YAML starter](02-planning/raid-log.yaml), [communication plan](02-planning/communication-plan.md) | Plan baselined and the RAID log reviewed at steering |
| 03 Requirements and design | Decide what to build, and how patient data will be protected | [User story](03-requirements-and-design/user-story.md), [requirements traceability matrix](03-requirements-and-design/requirements-traceability-matrix.md), [privacy and security review](03-requirements-and-design/privacy-and-security-review.md) | Healthcare: privacy and security review signed off before build starts |
| 04 Build | Build in sprints and keep changes to the baseline under control | [Change request](04-build/change-request.md), [sprint retrospective](04-build/sprint-retrospective.md) | Scope frozen, with every change since the baseline approved |
| 05 Testing | Prove the release works for the people who will use it | [UAT plan](05-testing/uat-plan.md), [defect severity guide](05-testing/defect-severity-guide.md) | Healthcare: UAT signed off by the business owner and the clinical reviewers |
| 06 Release | Decide to go live, and get there safely | [Go-live readiness checklist](06-release/go-live-readiness-checklist.md), [cutover and rollback runbook](06-release/cutover-and-rollback-runbook.md), [release notes](06-release/release-notes.md) | Change advisory board approval and a GO decision. Healthcare: downtime procedures ready in every clinical area that loses access |
| 07 Hypercare | Support users through the first weeks after go-live | [Hypercare plan](07-hypercare/hypercare-plan.md) | Exit criteria met and the handover accepted by support |
| 08 Closure | Close formally and keep what was learned | [Lessons learned](08-closure/lessons-learned.md), [project closure report](08-closure/project-closure-report.md) | Closure report signed by the sponsor |

Gates marked Healthcare are the ones specific to clinical software. They sit on the main path rather than in an appendix, and everything else in each template works for any software project.

## Templates

| Template | Use it when |
| --- | --- |
| Weekly status report | Every week, to tell the sponsor where things stand and what you need from them |
| Meeting minutes | Any meeting that makes a decision or hands out actions |
| Project charter | The sponsor has agreed to start, and nothing is committed yet |
| RACI matrix | In planning, and again before UAT and go-live, when ownership blurs |
| RAID log | From charter approval to closure, reviewed weekly |
| Communication plan | In planning, then at every phase gate |
| User story | For every backlog item, from refinement to acceptance |
| Requirements traceability matrix | From agreed requirements to release, to show each one was built, tested and accepted |
| Privacy and security review | During design, before build starts, and again whenever data flows change |
| Change request | For a change beyond tolerance once the plan is baselined, or any change to a clinical workflow or to how PHI is handled |
| Sprint retrospective | At the end of every sprint |
| UAT plan | Before UAT starts, agreed with the people who will sign it off |
| Defect severity guide | Before system testing, then unchanged through hypercare |
| Go-live readiness checklist | In readiness reviews before go-live, and at the go/no-go meeting |
| Cutover and rollback runbook | Once scope is stable; rehearse it, then follow it line by line |
| Release notes | For every production release, before users meet the change |
| Hypercare plan | Before the go/no-go meeting, then from cutover until the exit criteria are met |
| Lessons learned | Two to four weeks after hypercare ends |
| Project closure report | After hypercare exit, to close the project formally |

## How to use them

Each file opens with a short "When to use it", followed by the template. Placeholders are in square brackets, and the short italic notes mark the places where people new to the work tend to go wrong; delete them once they've done their job.

To use a template in Confluence, Google Docs or SharePoint, open the file on GitHub, copy the rendered page and paste it in. Headings, lists and tables come across. Or keep the Markdown in a repo next to the code and change it through pull requests, so edits to a runbook or a RAID log get reviewed like any other change.

Cut the rows that don't fit your project. Two things are worth keeping as they are: the hard blockers on the go-live checklist, which come off only with the sponsor's written agreement, and the defect severity guide, whose S1 to S4 scale and clinical-safety flag are shared by the UAT plan, the go-live checklist and the hypercare plan.

## Examples

[examples/](examples/) holds two documents filled in for a fictional project, EHR Integration Phase 2: a [weekly status report](examples/weekly-status-report-ehr-integration.md) from 2026-10-27, and the [go-live readiness checklist](examples/go-live-checklist-ehr-integration.md) from its go/no-go meeting on 2026-12-03, which ends in a CONDITIONAL GO. They share the project, people and RAID items of the example register in raid-log, so the status report can be checked against that register line by line. The project, people and figures are made up.

## RAID log as code

The [RAID log template](02-planning/raid-log.md) has a YAML twin, [raid-log.yaml](02-planning/raid-log.yaml), in the format read by [raid-log](https://github.com/nikhilav4/raid-log), a command-line tool that validates a register, writes the steering report and shows what changed since the last meeting. With raid-log installed (see its README), check the starter with:

```bash
raid validate 02-planning/raid-log.yaml
```

## What these are not

They are starting points, not policy. Your privacy office, information security team, change advisory board and clinical leadership decide what a review or a sign-off has to contain, and nothing here is legal advice about HIPAA.

## License

MIT. See [LICENSE](LICENSE).

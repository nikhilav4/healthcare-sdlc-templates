# Release notes

## When to use it

Publish release notes for every production release, from a major go-live to a small patch, before users meet the change. They have two audiences with different needs: the people whose work changes, who want to know what is different for them and where to get help, and the support and IT staff, who need the technical detail and the known issues. Write the user sections in the language of the job rather than in ticket titles, and have the clinical lead check any wording that describes a clinical workflow before it goes out.

## Template

| Field | Value |
| --- | --- |
| Release | [Name, version] |
| Release date | [YYYY-MM-DD] |
| Downtime | [None / YYYY-MM-DD HH:MM to HH:MM] |
| Production change ticket | [ID] |
| Help | [Service desk number or channel] |

### Summary

[Two or three sentences: what the release does and who it affects.]

### What changes for you

| Who | What's different | What to do |
| --- | --- | --- |
| [Role, for example inpatient nurses] | [The change, described plainly] | [Any action, and where to learn more] |
| | | |

*Lead with what people will notice on their first shift. "Allergies now show in the banner on every screen" helps a nurse; "STORY-118: implement allergy banner component" doesn't.*

### Clinical workflow changes

[Any change to how clinicians order, document, give medication or receive results, described step by step.]

Reviewed by: [clinical lead], [YYYY-MM-DD]

### Known issues and workarounds

| Defect | What you'll see | Workaround | Fix expected |
| --- | --- | --- | --- |
| [ID] | | | [Release or date] |

### Fixed in this release

| Defect | What was wrong |
| --- | --- |
| [ID] | |

### Training and help

- [Tip sheets and videos, and where to find them]
- [Super-users on each unit until [YYYY-MM-DD]]
- [The service desk, and how to reach the command center during hypercare]

### Technical notes for IT and support

| Item | Detail |
| --- | --- |
| Components and versions | |
| Database changes | [Migrations, and whether they can be reversed] |
| Configuration changes | |
| Interfaces affected | [Feeds, message types, endpoints] |
| Access and roles | [New roles, changed permissions] |
| Monitoring | [Alerts added or changed] |
| Rollback | [Section] of the [cutover and rollback runbook](cutover-and-rollback-runbook.md) |

### Security and privacy

[New or changed PHI flows, access, audit logging or vendor access, with a reference to the privacy and security review. Write "None" when nothing changed, so readers know it was checked.]

*Use synthetic test patients in every screenshot. Release notes get forwarded, printed and pinned to walls.*

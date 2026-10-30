# Privacy and security review

## When to use it

Complete it during design and get it signed by information security and the privacy office before build starts; it is the gate between the two phases. Update it whenever a change request adds a data flow, a vendor, a role or a new place where patient data is stored. The review records what patient data the system touches, where that data goes, who can see it, how access is recorded, how it is protected and which vendors handle it. A problem found here costs a design change; the same problem found in a penetration test two weeks before go-live costs the date.

*This template organizes the review. It does not replace your organization's security risk assessment, its policies or legal advice, and the privacy office and security team decide what is acceptable.*

## Template

| Field | Value |
| --- | --- |
| System or release | [Name] |
| System owner | [Name] |
| Prepared by | [Name] |
| Security reviewer | [Name] |
| Privacy reviewer | [Name] |
| Review date | [YYYY-MM-DD] |
| Version | [ ] |

### 1. System overview

[What the system does, who uses it, where it is hosted and what it connects to. Link an architecture diagram that shows every data store and every connection.]

### 2. PHI inventory

| Data element | PHI | Source | Stored where | Retention | Why it is needed |
| --- | --- | --- | --- | --- | --- |
| [Patient name, MRN, date of birth] | [Yes] | [System] | [Database, cache, files, backups] | [Period and policy reference] | [The task that needs it] |
| | | | | | |

*Include the places nobody thinks of: logs, caches, message queues, backups, report exports, analytics and error-tracking services, and the test and training environments.*

Data that may carry stricter rules than HIPAA alone: [substance use disorder treatment records covered by 42 CFR Part 2, psychotherapy notes, HIV status, genetic information, reproductive health, minors' records, and anything else your state's law protects more closely]

### 3. Data flows

| Flow | From | To | Data elements | Method | Encryption in transit | Frequency | Owner |
| --- | --- | --- | --- | --- | --- | --- | --- |
| F1 | [System] | [System] | | [HL7 v2, FHIR API, SFTP, database link] | [TLS version, VPN] | [Real time / nightly] | |
| F2 | | | | | | | |

### 4. Minimum necessary

| Flow or role | Data received | Needed for | Could it be less? | Decision |
| --- | --- | --- | --- | --- |
| [F1] | | | [For example, age instead of date of birth, or the last four digits instead of the full number] | |

*The usual answer is "the interface sends everything because that is the vendor's default message". Ask whether the receiving system needs it. The HIPAA minimum necessary standard has exceptions, including disclosures to a provider for treatment, but trim anyway where you can: data a system never receives can't leak from it.*

### 5. Access control and role design

| Role | Who holds it | Can see | Can change | Who approves access | Access review |
| --- | --- | --- | --- | --- | --- |
| [Inpatient nurse] | | [Patients on assigned units] | | [Unit manager] | [Quarterly] |
| [Vendor support] | | | | | |
| [Service accounts for interfaces and jobs] | | | | | |

- Unique user IDs for everyone. No shared accounts, including on shared clinical workstations.
- Emergency access (break-the-glass): [how it works, what reason is recorded, who reviews its use and how often]
- Restricted records, such as employees, public figures and patient-requested restrictions: [how they are protected]
- Automatic logoff or screen lock: [timeout for each type of workstation]
- Joiners, movers and leavers: [how access is granted, changed and removed, and how quickly]
- Vendor and remote access: [named accounts, time-limited, multi-factor authentication, logged]

*Design roles around the job, not around whoever asked first. A role made broad because it was quicker to set up is the one that turns up in a privacy investigation.*

### 6. Audit logging

| Question | Answer |
| --- | --- |
| Which actions on patient data are logged (view, create, change, delete, print, export)? | |
| What each event records (user, patient, action, time, source) | |
| Where the audit log is stored, and who can change or delete it | |
| How long it is kept | [Period from the records retention policy] |
| Who reviews it, how often, and what raises an alert | [For example, a user opening their own record or a relative's] |
| Is the application log free of PHI? | [Yes, checked on YYYY-MM-DD, and how] |

*The audit log and the application log are different things. The audit log should record access to patient data. The application log, which engineers and vendors read every day, should hold no patient data at all.*

### 7. Encryption

| Where | Method | Keys managed by | Notes |
| --- | --- | --- | --- |
| In transit, external connections | [TLS version] | | |
| In transit, internal connections | | | |
| At rest, databases | | | |
| At rest, backups | | | |
| At rest, file storage and exports | | | |
| Endpoints and mobile devices | | | |

*Encryption changes the outcome when something goes missing. PHI encrypted in line with HHS guidance is not "unsecured", so a lost laptop or backup tape holding it is generally not a reportable breach. Confirm with the privacy office what your organization requires.*

### 8. Vendors and agreements

| Vendor | Service | Access to PHI | Business associate agreement | Subcontractors with PHI access | Security assessment |
| --- | --- | --- | --- | --- | --- |
| | [Hosting, support, interface, analytics] | [None / Limited / Full] | [Signed YYYY-MM-DD / Pending] | | [Date and result] |

*A vendor that can see PHI, even only when a support engineer logs in to troubleshoot, usually needs a business associate agreement before that access is granted, not after.*

### 9. Non-production environments and test data

- [ ] Test, training and development environments use synthetic or de-identified data.
- [ ] Any use of production PHI outside production is approved in writing by the privacy office, has the same controls as production, and has an end date.
- [ ] Training environments use fictional patients that can't be mistaken for real ones.
- [ ] De-identification method, where used: [Safe Harbor / expert determination]

### 10. Findings

| # | Finding | Rating | Owner | Due | Status |
| --- | --- | --- | --- | --- | --- |
| F-01 | | [Critical / High / Medium / Low] | | | [Open / Fixed / Risk accepted by name and role] |

Critical and high findings are fixed, or have a fix planned and accepted by security, before build starts. Any still open at go-live are listed on the go-live readiness checklist.

### 11. Sign-off

| Role | Name | Decision | Conditions | Date |
| --- | --- | --- | --- | --- |
| Information security | | [Approved / Approved with conditions / Not approved] | | |
| Privacy office | | | | |
| System owner | | | | |

# IAM-LifeCycle-OffBoarding-Lifecycle
: High volunteer and staff turnover in nonprofits results in "orphan accounts"—former staff or volunteers retaining active access to cloud drives, email lists, and identity providers.

# IAM-OffBoarding-Playbook

**Identity & Access Management (IAM) Lifecycle and Offboarding Playbook for Nonprofits**

**Cyber Ready Clinic Capstone Project | Status: Planning / Initial Development**

## Overview

Small nonprofit organizations often depend on staff, volunteers, contractors, and managed service providers (MSPs) to run daily operations. When people leave or change roles, their access to email, cloud files, mailing lists, and other systems may not be promptly updated or removed.

This project aims to provide an affordable, repeatable **identity and access management (IAM) lifecycle standard operating procedure (SOP)** and supporting automation to help nonprofits reduce the risk of orphaned accounts and inappropriate access.

The initial technical focus is **Microsoft 365 / Microsoft Entra ID**, using **PowerShell** and the **Microsoft Graph API**. Google Workspace support may be considered in a later phase.

> **Project status:** This repository describes a proposed capstone solution. Automation, testing, and deliverables will be added incrementally. Features described as planned should not be assumed to be implemented.

## The Problem

Nonprofits may experience frequent changes in staffing and volunteer participation without having a dedicated IT or security team. Common risks include:

- Former staff or volunteers retaining access to organizational accounts.
- Unused accounts remaining enabled for months or years.
- Excessive permissions after an employee or volunteer changes roles.
- Cloud files, shared mailboxes, and group memberships lacking clear ownership.
- Inconsistent documentation of who approved, completed, and verified offboarding.
- Compromised accounts being used to send fraudulent messages or access sensitive information.

An inactive account is **not automatically an orphaned account**. Account ownership, business purpose, activity signals, and authorization must be reviewed before taking action.

## Project Objectives

1. Design an end-to-end IAM lifecycle SOP covering **onboarding, role changes, periodic access reviews, and offboarding**.
2. Create an account inventory and identify accounts requiring review.
3. Develop PowerShell-based, Microsoft Graph-assisted reporting and approved offboarding workflows.
4. Document ownership and retention decisions for email, files, groups, and third-party services.
5. Maintain an auditable checklist and risk register.
6. Deliver a board-level tabletop exercise involving a compromised former staff member's email account.
7. Keep the solution understandable and practical for low-budget nonprofit organizations and their MSPs.

## IAM Lifecycle Workflow

```text
Personnel request / change notification
                |
                v
     Authorization and approval
                |
                v
  Onboard / Change Role / Offboard
                |
                v
   Provision or adjust permissions
                |
                v
 Verify access and document evidence
                |
                v
    Periodic access certification
```

For offboarding, the planned workflow is:

```text
Departure confirmed
       |
       v
Approval and effective time recorded
       |
       v
Inventory accounts, roles, and access
       |
       v
Disable sign-in and revoke sessions
       |
       v
Review groups, apps, devices, and delegated access
       |
       v
Transfer business ownership of email/files as authorized
       |
       v
Verify completion and document exceptions
       |
       v
Apply approved retention/deletion schedule
```

**Important:** Disabling sign-in or revoking sessions alone does not complete offboarding. Existing access tokens, application sessions, third-party accounts, and shared resources may require separate handling. Session revocation may not take effect immediately in every service.

## Planned Technical Capabilities

| Capability | Planned approach | Status |
| --- | --- | --- |
| Account inventory | Microsoft Graph PowerShell | Planned |
| Inactivity review | Sign-in data where licensed and authorized | Planned |
| Potential orphan-account report | CSV output for manual review | Planned |
| Approved account disablement | Microsoft Graph with confirmation | Planned |
| Session revocation | Microsoft Graph, with verification guidance | Planned |
| Group and role access review | Graph inventory and documented actions | Planned |
| Mailbox and file ownership transition | Microsoft 365 admin procedures and checklists | Planned |
| Audit evidence | Timestamped reports and approval records | Planned |
| Risk register | Standardized risk-tracking template | Planned |
| Google Workspace integration | Admin SDK (optional future scope) | Future consideration |

### Safety-first design

The initial automation should be **read-only by default**. Any account-changing operation must require an authorized operator, an explicit approval, and a deliberate confirmation. Production changes should not be tested against real nonprofit accounts without permission and a documented rollback or recovery plan.

Use the minimum required Microsoft Graph permissions and avoid granting broad administrative access when narrower permissions are sufficient.

## Proposed Repository Structure

The following is a **target layout**, not a claim that these files already exist:

```text
IAM-OffBoarding-Playbook/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── iam-lifecycle-sop.md
│   ├── offboarding-checklist.md
│   ├── risk-register-template.csv
│   └── tabletop-exercise.md
├── scripts/
│   ├── Get-IAMAccountInventory.ps1
│   ├── Find-AccountsForReview.ps1
│   └── Invoke-ApprovedOffboarding.ps1
├── examples/
│   └── sample-accounts-synthetic.csv
└── tests/
```

## Planned Development Phases

### Phase 1 — Discovery and Reporting

- Establish a safe Microsoft 365 test environment or use synthetic data.
- Define required Microsoft Graph permissions.
- Enumerate accounts and relevant access attributes.
- Flag accounts for review based on documented criteria.
- Export a report without changing accounts.

### Phase 2 — Controlled Offboarding

- Require documented authorization.
- Disable sign-in for an approved account.
- Revoke sign-in sessions where supported.
- Review delegated access, group membership, applications, and devices.
- Coordinate mailbox and file ownership transitions.
- Verify the result and record exceptions.

### Phase 3 — SOP, Audit Evidence, and Tabletop Exercise

- Finalize onboarding, role-change, and offboarding procedures.
- Publish a reusable checklist and risk-register template.
- Test with synthetic identities and approved test accounts.
- Conduct a tabletop exercise for nonprofit leadership.
- Prepare a 5–7 minute Cyber Ready Clinic capstone demonstration.

## Sample Offboarding Checklist

- [ ] Confirm departure and effective date/time with the authorized manager.
- [ ] Identify the account and all associated access.
- [ ] Record approval and assign an offboarding owner.
- [ ] Disable organizational sign-in at the approved time.
- [ ] Revoke supported sessions and review remaining access paths.
- [ ] Review privileged roles, groups, applications, devices, and MFA methods.
- [ ] Transfer business-critical mail, files, and resource ownership as authorized.
- [ ] Review external services not managed by Microsoft 365.
- [ ] Preserve records according to organizational retention and legal-hold requirements.
- [ ] Verify completion and document evidence or exceptions.
- [ ] Schedule account deletion only after retention and recovery requirements are met.

## Board Tabletop Exercise

**Scenario:** A volunteer coordinator departed six weeks ago, but their Microsoft 365 account remained enabled. Suspicious messages requesting changes to donation payment instructions are discovered in the account's sent mail.

Participants should discuss:

1. Who declares and coordinates the incident?
2. Who contacts the MSP or IT administrator?
3. How will the account and related sessions be contained?
4. How will the organization investigate messages, access, and potential data exposure?
5. Who determines whether donors, regulators, insurers, or law enforcement should be notified?
6. What corrective actions and policy changes are needed?

**Expected outputs:** an incident timeline, responsibility assignments, an evidence checklist, and prioritized improvements to the IAM SOP.

## Intended Audience

- Nonprofit executive directors and board members.
- Volunteer coordinators and operations managers.
- Small nonprofit IT administrators.
- MSPs and cybersecurity advisors.
- Cyber Ready Clinic participants and mentors.

## Prerequisites for Future Automation

- PowerShell 7 or an appropriate supported Windows PowerShell environment.
- Microsoft Graph PowerShell SDK.
- A Microsoft 365 / Microsoft Entra test tenant or authorized environment.
- Appropriate administrator consent and least-privilege permissions.
- Organizational approval before making changes.

Installation commands and operating instructions will be added alongside tested scripts. **No production execution instructions are provided at this planning stage.**

## Data Protection and Responsible Use

Do not commit real employee or volunteer information, authentication tokens, API secrets, client exports, or sensitive incident evidence to this repository. Use synthetic sample data and redact screenshots and reports before sharing. Logs should avoid unnecessary personal data and be retained according to organizational policy.

This project is a decision-support and administrative workflow aid, **not** a substitute for organizational authorization, professional incident response, legal advice, or vendor-specific guidance.

## Success Criteria

The capstone will be considered successful when it can demonstrate a documented onboarding/offboarding process, a safe account review report, an authorized and verified test-account offboarding workflow, and a practical tabletop exercise that nonprofit leadership can follow.

## License

A license has not yet been selected. Add a `LICENSE` file before representing the project as open-source or granting reuse rights.

## Acknowledgment

Developed as a **Cyber Ready Clinic capstone project**, with an emphasis on practical, affordable cybersecurity improvements for nonprofit organizations.


# New User Account Creation Detection

## Overview

Unauthorized account creation is a common technique used by attackers to establish persistence, maintain privileged access, or create backdoor accounts within an Active Directory environment. Monitoring newly created user accounts enables Security Operations Center (SOC) analysts to identify unauthorized administrative activity and investigate potential security incidents.

This detection monitors Windows Security Event ID **4720** to identify the creation of new user accounts.

---

## Detection Objective

- Detect newly created Windows user accounts.
- Identify unauthorized account creation activities.
- Monitor administrative actions within Active Directory.
- Support investigations into persistence and privilege abuse.

---

## Detection Severity

**Medium**

New user account creation is generally a legitimate administrative activity but should always be validated to ensure it was authorized and performed according to organizational policies.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Create Account | **T1136** |

---

## Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4720** | A user account was created |

---

## Log Source

- Windows Security Event Log

---

## Detection Logic

Generate an alert whenever a new Windows user account is created. Every account creation event should be reviewed to verify that it was performed by an authorized administrator and aligns with approved business processes.

---

## SPL Detection Query

```spl
index=main EventCode=4720
| table _time SubjectUserName TargetUserName ComputerName
| sort -_time
```

---

## Query Explanation

- **index=main** – Searches events from the primary Splunk index.
- **EventCode=4720** – Filters Windows user account creation events.
- **_time** – Time the account was created.
- **SubjectUserName** – Administrator or user who created the account.
- **TargetUserName** – Newly created user account.
- **ComputerName** – Domain Controller or system where the event was recorded.
- **sort -_time** – Displays the most recent account creation events first.

---

## Example Output

| Time | Created By | New User | Computer |
|------|------------|----------|----------|
| 2026-07-31 14:05 | Administrator | alice | DC01 |
| 2026-07-31 16:22 | Administrator | testuser | DC01 |

---

## Investigation Workflow

When a new user account is detected:

1. Identify the administrator who created the account.
2. Verify the business justification for the account creation.
3. Confirm the account creation request through approved change management or onboarding records.
4. Review the user's assigned security groups and permissions.
5. Check whether the account was immediately added to privileged groups.
6. Review subsequent authentication activity associated with the new account.
7. Determine whether the account follows organizational naming conventions.
8. Document findings and escalate any unauthorized activity.

---

## Possible False Positives

The following legitimate activities may generate this detection:

- New employee onboarding.
- Service account creation.
- Application account provisioning.
- Temporary administrative accounts.
- User migration or account synchronization.
- Automated identity management processes.

---

## Recommended Response

If the account creation is unauthorized or suspicious:

- Disable or remove the newly created account.
- Review the administrator account responsible for the creation.
- Investigate recent administrative activities on the affected system.
- Audit group memberships and assigned privileges.
- Review authentication logs associated with the new account.
- Preserve relevant security logs for forensic analysis.
- Escalate the incident according to the organization's incident response procedures.

---

## Expected Outcome

This detection enables SOC analysts to quickly identify newly created Windows user accounts, verify whether they were legitimately provisioned, and investigate unauthorized account creation that may indicate persistence or privilege abuse within the environment.
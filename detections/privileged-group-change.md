# Privileged Group Membership Change Detection

## Overview

Privileged security groups, such as **Domain Admins**, **Enterprise Admins**, and **Administrators**, provide elevated permissions that can significantly impact an organization's security. Unauthorized additions to these groups are a strong indicator of privilege escalation, account compromise, or malicious administrative activity.

This detection monitors Windows Security Events that record users being added to privileged security groups, enabling Security Operations Center (SOC) analysts to quickly identify and investigate unauthorized privilege assignments.

---

## Detection Objective

- Detect users added to privileged security groups.
- Monitor privilege escalation activities.
- Identify unauthorized administrative changes.
- Support investigations into account compromise and persistence techniques.

---

## Detection Severity

**High**

Membership changes involving privileged security groups should be considered high priority because they may grant attackers elevated permissions across the environment.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Account Manipulation | **T1098** |
| Privilege Escalation | Account Manipulation | **T1098** |

---

## Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4728** | A member was added to a security-enabled global group |
| **4732** | A member was added to a security-enabled local group |

---

## Log Source

- Windows Security Event Log

---

## Detection Logic

Generate an alert whenever a user account is added to a privileged security group. Administrative changes involving high-privilege groups should always be validated to ensure they were authorized and performed according to organizational policies.

---

## SPL Detection Query

```spl
index=main (EventCode=4728 OR EventCode=4732)
| table _time SubjectUserName MemberName GroupName ComputerName
| sort -_time
```

---

## Query Explanation

- **index=main** – Searches events within the primary Splunk index.
- **EventCode=4728 OR EventCode=4732** – Filters group membership modification events.
- **_time** – Time when the group membership change occurred.
- **SubjectUserName** – Administrator or account that performed the action.
- **MemberName** – User account added to the privileged group.
- **GroupName** – Security group receiving the new member.
- **ComputerName** – Domain Controller that recorded the event.
- **sort -_time** – Displays the most recent events first.

---

## Example Output

| Time | Performed By | Added User | Security Group | Computer |
|------|--------------|------------|----------------|----------|
| 2026-07-31 11:42 | Administrator | alice | Domain Admins | DC01 |
| 2026-07-31 15:18 | HelpDesk01 | bob | Backup Operators | DC01 |

---

## Investigation Workflow

When a privileged group membership change is detected:

1. Identify the administrator who performed the group membership change.
2. Verify that the modification was authorized through change management procedures.
3. Confirm the business justification for granting elevated privileges.
4. Review the user's existing permissions and assigned roles.
5. Investigate recent authentication activity for both the administrator and the newly privileged account.
6. Review additional administrative changes performed during the same timeframe.
7. Determine whether the affected group is considered highly privileged.
8. Document findings and escalate any unauthorized activity.

---

## Possible False Positives

The following legitimate activities may generate this detection:

- New administrator onboarding.
- Role or department changes.
- Planned privilege assignments.
- Temporary administrative access.
- IT maintenance activities.
- Automated identity and access management (IAM) provisioning.

---

## Recommended Response

If the group membership change is determined to be unauthorized or suspicious:

- Immediately remove the user from the privileged security group.
- Verify the legitimacy of the administrator account that performed the action.
- Review authentication logs for both accounts.
- Audit additional administrative actions performed during the same period.
- Reset credentials if account compromise is suspected.
- Preserve security logs for forensic investigation.
- Escalate the incident according to the organization's incident response procedures.

---

## Expected Outcome

This detection enables SOC analysts to rapidly identify privilege escalation attempts, validate administrative changes, and investigate unauthorized modifications to privileged security groups before they can be leveraged for lateral movement or further compromise.
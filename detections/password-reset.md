# Password Reset Detection

## Overview

Password reset events are important security indicators because they may represent legitimate administrative activity or unauthorized attempts to gain access to user accounts. Monitoring password reset operations enables Security Operations Center (SOC) analysts to detect potential account compromise, privilege abuse, or suspicious administrative actions.

This detection monitors Windows Security Event ID **4724** to identify password reset attempts performed within the Active Directory environment.

---

## Detection Objective

- Detect password reset operations.
- Monitor administrative account management activities.
- Identify unauthorized or suspicious password resets.
- Support investigations into potential account compromise and privilege abuse.

---

## Detection Severity

**Medium**

Password reset events are typically legitimate administrative actions; however, unexpected or unauthorized password resets should be investigated immediately, especially when performed on privileged accounts.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Credential Access | Password Policy Discovery / Account Manipulation | **T1098** |

> **Note:** Password resets are administrative actions rather than a direct attack technique. This detection is commonly associated with **T1098 – Account Manipulation**, as attackers may reset credentials after obtaining administrative privileges.

---

## Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4724** | An attempt was made to reset an account's password |

---

## Log Source

- Windows Security Event Log

---

## Detection Logic

Generate an alert whenever a password reset event is recorded. Each event should be reviewed to verify that the password reset was performed by an authorized administrator or as part of an approved operational process.

---

## SPL Detection Query

```spl
index=main EventCode=4724
| table _time SubjectUserName TargetUserName ComputerName
| sort -_time
```

---

## Query Explanation

- **index=main** – Searches events within the primary Splunk index.
- **EventCode=4724** – Filters Windows password reset events.
- **_time** – Time when the password reset occurred.
- **SubjectUserName** – Administrator or account performing the password reset.
- **TargetUserName** – User account whose password was reset.
- **ComputerName** – Domain Controller that recorded the event.
- **sort -_time** – Displays the most recent password reset events first.

---

## Example Output

| Time | Performed By | Target User | Computer |
|------|--------------|-------------|----------|
| 2026-07-31 15:42 | Administrator | alice | DC01 |
| 2026-07-31 16:18 | HelpDesk01 | bob | DC01 |

---

## Investigation Workflow

When a password reset event is detected:

1. Identify the administrator or account that initiated the password reset.
2. Verify that the reset was approved through organizational change management or help desk procedures.
3. Determine whether the affected account is privileged or sensitive.
4. Review recent authentication activity before and after the password reset.
5. Check whether the affected account was involved in suspicious authentication events.
6. Review additional administrative actions performed by the initiating account.
7. Document findings and escalate any unauthorized activity.

---

## Possible False Positives

The following legitimate activities may generate password reset events:

- Help desk password reset requests.
- User self-service password recovery.
- Administrator password maintenance.
- Employee onboarding or offboarding.
- Scheduled credential rotation.
- Automated identity management processes.

---

## Recommended Response

If the password reset is determined to be unauthorized or suspicious:

- Verify the identity of the administrator performing the reset.
- Contact the affected user to confirm the password reset request.
- Reset the account credentials if compromise is suspected.
- Review authentication logs before and after the event.
- Audit recent administrative activities associated with the initiating account.
- Investigate additional changes made to the affected account.
- Preserve relevant security logs and escalate according to the organization's incident response procedures.

---

## Expected Outcome

This detection enables SOC analysts to identify password reset activities, distinguish legitimate administrative operations from suspicious behavior, and rapidly investigate potential account compromise or unauthorized credential modifications.
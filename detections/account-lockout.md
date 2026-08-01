# Account Lockout Detection

## Overview

Account lockouts are often generated after multiple failed authentication attempts or when account lockout policies are triggered. Monitoring these events helps Security Operations Center (SOC) analysts identify potential brute-force attacks, password spraying, credential misuse, or user account issues requiring investigation.

This detection identifies Windows account lockout events by monitoring **Windows Security Event ID 4740**.

---

## Detection Objective

- Detect user account lockout events
- Identify accounts affected by repeated authentication failures
- Support early detection of brute-force and password spraying attacks
- Provide visibility into account security incidents

---

## Windows Event ID

| Event ID | Description |
|----------|-------------|
| **4740** | A user account was locked out |

---

## Log Source

- Windows Security Event Log

---

## SPL Detection Query

```spl
index=main EventCode=4740
| table _time ComputerName TargetUserName CallerComputerName SubjectUserName
| sort -_time
```

---

## Query Explanation

- **_time** – Time when the account lockout occurred.
- **ComputerName** – Domain Controller that recorded the event.
- **TargetUserName** – User account that was locked.
- **CallerComputerName** – System from which the lockout originated.
- **SubjectUserName** – Account responsible for processing the lockout event.

---

## Investigation Steps

When an account lockout is detected:

1. Identify the affected user account.
2. Determine the source computer initiating the lockout.
3. Review preceding failed logon events (Event ID **4625**).
4. Verify whether multiple authentication failures occurred within a short period.
5. Determine whether the activity is legitimate or potentially malicious.
6. Reset or unlock the account if appropriate and document the investigation.

---

## Possible Threat Scenarios

- Brute-force password attack
- Password spraying attack
- Credential stuffing
- Stale cached credentials
- Incorrect password stored in scheduled tasks or services
- User repeatedly entering an incorrect password

---

## Recommended Response

- Validate the legitimacy of the authentication attempts.
- Investigate the source endpoint generating the lockout.
- Review authentication activity before and after the event.
- Reset the affected user's password if compromise is suspected.
- Enable additional monitoring for repeated lockout activity.
- Escalate confirmed malicious activity according to the incident response process.

---

## MITRE ATT&CK Mapping

| Tactic | Technique |
|---------|-----------|
| Credential Access | T1110 – Brute Force |

---

## Example Output

| Time | Locked Account | Source Computer |
|------|----------------|-----------------|
| 2026-07-31 10:15:24 | alice | WIN11-01 |
| 2026-07-31 10:18:42 | bob | WIN11-01 |

---

## Expected Outcome

This detection enables SOC analysts to quickly identify account lockout events, investigate their origin, and determine whether they are the result of normal user activity or malicious authentication attempts.
# Successful Login After Multiple Failed Authentication Attempts

## Overview

A successful authentication following multiple failed logon attempts may indicate that an attacker has successfully guessed or obtained valid user credentials. While legitimate users can occasionally mistype their passwords, repeated authentication failures immediately followed by a successful login should be investigated to determine whether unauthorized access has occurred.

This detection correlates Windows failed logon events (**Event ID 4625**) with successful logon events (**Event ID 4624**) occurring within a defined time window for the same user account.

---

## Detection Objective

- Detect successful authentication following multiple failed login attempts.
- Identify potential credential guessing or brute-force attacks.
- Monitor suspicious authentication sequences.
- Support investigations into possible account compromise.

---

## Detection Severity

**High**

A successful authentication immediately following multiple failed login attempts may indicate that valid credentials have been obtained by an attacker, making this a high-priority security event.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Initial Access | Valid Accounts | **T1078** |
| Defense Evasion | Valid Accounts | **T1078** |
| Persistence | Valid Accounts | **T1078** |

---

## Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4624** | Successful account logon |
| **4625** | Failed account logon |

---

## Log Source

- Windows Security Event Log

---

## Detection Logic

Generate an alert when multiple failed authentication attempts are followed by a successful logon for the same user account within a **10-minute** time window.

This authentication pattern may indicate:

- Successful brute-force attack
- Password guessing
- Credential stuffing
- Legitimate user authentication after several failed attempts

Analysts should investigate the event to determine whether the activity is authorized or malicious.

---

## SPL Detection Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
| transaction Account_Name maxspan=10m
| search EventCode=4625 EventCode=4624
```

---

## Query Explanation

- **index=main** – Searches events within the primary Splunk index.
- **EventCode=4624 OR EventCode=4625** – Filters successful and failed Windows authentication events.
- **transaction Account_Name** – Correlates authentication events for the same user account.
- **maxspan=10m** – Groups authentication events occurring within a ten-minute window.
- **search EventCode=4625 EventCode=4624** – Returns only transactions containing both failed and successful authentication events.

---

## Example Output

| Time | User Account | Source Computer | Failed Attempts | Result |
|------|--------------|-----------------|----------------:|--------|
| 2026-07-31 10:24 | alice | WIN11-01 | 6 | Successful Logon |
| 2026-07-31 14:18 | Administrator | DC01 | 5 | Successful Logon |

---

## Investigation Workflow

When this detection is triggered:

1. Identify the affected user account.
2. Review the sequence and number of failed authentication attempts.
3. Verify the successful authentication event and its logon type.
4. Identify the source workstation or IP address.
5. Determine whether the login originated from a trusted device or expected location.
6. Review authentication activity before and after the successful logon.
7. Check for privilege escalation, account modifications, or suspicious administrative activity.
8. Determine whether the authentication was legitimate or the result of compromised credentials.
9. Document findings and escalate according to the organization's incident response procedures.

---

## Possible False Positives

The following legitimate activities may generate this detection:

- User repeatedly entering an incorrect password before remembering the correct one.
- Expired cached credentials.
- Password manager synchronization issues.
- Keyboard layout changes.
- Applications or services retrying authentication before using updated credentials.

---

## Recommended Response

If malicious activity is suspected:

- Verify the identity of the authenticated user.
- Review authentication logs from the source system.
- Check for additional suspicious activity following the successful login.
- Reset the affected user's password.
- Require password rotation and, if available, enforce Multi-Factor Authentication (MFA).
- Review privileged account usage associated with the account.
- Preserve relevant security logs for forensic investigation.
- Escalate the incident according to the organization's incident response procedures.

---

## Expected Outcome

This detection enables SOC analysts to identify authentication sequences that may indicate successful credential compromise, allowing rapid investigation and response before an attacker can establish persistence or perform lateral movement within the environment.
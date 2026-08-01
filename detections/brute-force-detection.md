# Brute Force Detection

## Overview

Brute-force attacks are one of the most common techniques used by attackers to gain unauthorized access to user accounts by repeatedly attempting different passwords. Monitoring failed authentication events enables Security Operations Center (SOC) analysts to identify suspicious login behavior before an account is compromised.

This detection identifies multiple failed Windows logon attempts originating from the same source within a defined time window and generates an alert when the activity exceeds a specified threshold.

---

## Detection Objective

- Detect repeated failed authentication attempts.
- Identify potential brute-force attacks against Windows accounts.
- Monitor suspicious authentication activity across the environment.
- Enable rapid investigation and response to credential-based attacks.

---

## Detection Severity

**High**

Repeated authentication failures within a short period may indicate an active brute-force attack targeting user credentials.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Credential Access | Brute Force | **T1110** |

---

## Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4625** | Failed account logon attempt |

---

## Log Source

- Windows Security Event Log

---

## Detection Logic

Generate an alert when **five or more failed logon attempts** are observed for the **same user account** from the **same source IP address** within a **five-minute time window**.

This detection helps identify abnormal authentication activity that may indicate password guessing or automated credential attacks.

---

## SPL Detection Query

```spl
index=main EventCode=4625
| bucket _time span=5m
| stats count by _time Account_Name Source_Network_Address
| where count >= 5
| sort -count
```

---

## Query Explanation

- **index=main** – Searches events within the primary Splunk index.
- **EventCode=4625** – Filters failed Windows authentication events.
- **bucket _time span=5m** – Groups events into five-minute intervals.
- **stats count** – Counts failed logon attempts.
- **Account_Name** – Target user account.
- **Source_Network_Address** – Source IP initiating authentication requests.
- **where count >= 5** – Returns only suspicious authentication activity.
- **sort -count** – Displays the highest number of failed attempts first.

---

## Example Output

| Time | User Account | Source IP | Failed Attempts |
|------|--------------|-----------|----------------:|
| 10:05 | Administrator | 172.20.10.20 | 8 |
| 11:42 | alice | 192.168.100.25 | 6 |

---

## Investigation Workflow

When this detection is triggered:

1. Identify the targeted user account.
2. Determine the source IP address generating the failed logon attempts.
3. Review authentication history for the affected account.
4. Check for any successful logon events (Event ID **4624**) following the failures.
5. Determine whether the account was locked (Event ID **4740**).
6. Identify additional systems targeted from the same source IP.
7. Validate whether the activity originated from an authorized user or a malicious actor.
8. Document findings and escalate according to the organization's incident response procedures.

---

## Possible False Positives

The following legitimate activities may generate similar alerts:

- Users repeatedly entering incorrect passwords.
- Expired or cached credentials.
- Misconfigured scheduled tasks.
- Services running with outdated passwords.
- Automated scripts using invalid credentials.
- Legacy applications repeatedly attempting authentication.

---

## Recommended Response

If malicious activity is suspected:

- Investigate the source system initiating the authentication attempts.
- Verify whether any successful authentication occurred after the failures.
- Lock or disable the affected account if compromise is confirmed.
- Reset the user's password.
- Block the offending IP address when appropriate.
- Review authentication activity across other user accounts.
- Monitor the environment for additional credential-based attacks.
- Document the incident and preserve relevant logs for forensic analysis.

---

## Expected Outcome

This detection enables SOC analysts to rapidly identify brute-force authentication attempts, investigate affected accounts, determine whether unauthorized access was achieved, and respond before a successful compromise occurs.
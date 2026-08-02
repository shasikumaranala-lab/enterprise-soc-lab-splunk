# Incident Investigation Report: Brute Force Authentication Attempt

## Overview

This investigation documents a suspected brute-force authentication attack detected within the Enterprise SOC Lab. The incident was identified through a custom Splunk detection rule that monitors repeated failed Windows authentication attempts over a defined time period.

Multiple failed logon events originating from the same source were observed within a five-minute window, exceeding the organization's alert threshold and triggering a security investigation.

---

# Incident Summary

| Field | Value |
|--------|-------|
| Incident ID | SOC-001 |
| Incident Name | Brute Force Authentication Attempt |
| Detection Rule | Brute Force Detection |
| Severity | High |
| Priority | High |
| Status | Closed |
| Detection Time | YYYY-MM-DD HH:MM |
| Investigation Start | YYYY-MM-DD HH:MM |
| Investigation End | YYYY-MM-DD HH:MM |
| Analyst | Anala Shasi Kumar |

---

# Incident Description

The Enterprise SOC Dashboard generated a high-severity alert after detecting multiple failed Windows authentication attempts targeting the same user account within a five-minute period.

The activity matched the organization's brute-force detection logic and required immediate investigation to determine whether unauthorized access had been achieved.

---

# Detection Details

## Detection Rule

Repeated failed authentication attempts from the same source IP address targeting the same user account within a five-minute window.

### Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4625** | Failed Account Logon |
| **4624** | Successful Account Logon (Reviewed during investigation) |
| **4740** | Account Lockout (Reviewed during investigation) |

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

# Alert Information

| Field | Value |
|--------|-------|
| Alert Type | Scheduled Alert |
| Alert Frequency | Every 5 Minutes |
| Trigger Condition | Five or more failed authentication attempts |
| Data Source | Windows Security Event Log |
| SIEM Platform | Splunk Enterprise |

---

# Investigation Workflow

## Step 1 — Validate the Alert

### Objective

Confirm that the alert represents genuine authentication activity and is not a false positive.

### SPL Query

```spl
index=main EventCode=4625
```

### Findings

- Multiple failed authentication events were identified.
- Authentication failures occurred within a short time window.
- The alert met the configured detection threshold.

---

## Step 2 — Identify the Targeted Account

### Objective

Determine which account was targeted and identify the originating system.

### Fields Reviewed

- Account_Name
- ComputerName
- Source_Network_Address
- Logon_Type

### Findings

Repeated authentication attempts targeted the same user account from a single source system.

---

## Step 3 — Review Authentication Outcome

### Objective

Determine whether any failed authentication attempts eventually resulted in a successful login.

### SPL Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
```

### Findings

- Multiple failed authentication events were observed.
- No successful authentication (Event ID 4624) occurred following the failed attempts.
- No evidence of unauthorized account access was identified.

---

## Step 4 — Review Related Security Activity

### Objective

Identify any additional security events that may indicate account compromise or privilege escalation.

### Events Reviewed

| Event ID | Description |
|----------|-------------|
| 4720 | User Account Created |
| 4724 | Password Reset Attempt |
| 4728 | User Added to Global Security Group |
| 4732 | User Added to Local Security Group |
| 4740 | Account Lockout |

### Findings

No correlated administrative activity or privilege escalation events were detected.

---

# Timeline of Events

| Time | Activity |
|------|----------|
| 10:00 | Failed authentication attempts began |
| 10:03 | Detection rule triggered |
| 10:03 | Splunk generated security alert |
| 10:05 | SOC analyst initiated investigation |
| 10:10 | Authentication events reviewed |
| 10:12 | Related Windows security events analyzed |
| 10:15 | Investigation completed |
| 10:16 | Incident closed |

---

# Indicators of Compromise (IOCs)

| Indicator | Value |
|-----------|-------|
| Target User | Administrator |
| Source IP Address | 172.20.10.X |
| Source Host | WIN-SERVER-01 |
| Windows Event ID | 4625 |
| Attack Technique | Repeated Failed Authentication |

---

# Evidence Collected

The following evidence was reviewed during the investigation:

- Windows Security Event Logs
- Splunk Search Results
- Authentication Timeline
- Detection Rule Output
- Windows Event IDs
- Source Host Information

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Credential Access | Brute Force | T1110 |
| Defense Evasion | Valid Accounts (Reviewed) | T1078 |

---

# Risk Assessment

| Category | Assessment |
|----------|------------|
| Likelihood | Medium |
| Business Impact | Low |
| Successful Compromise | No |
| Privilege Escalation | Not Observed |
| Persistence | Not Observed |

---

# Investigation Findings

- Multiple failed authentication attempts were detected against a single user account.
- Authentication attempts originated from the same source system.
- No successful authentication was observed.
- No account lockout occurred during the investigation.
- No unauthorized account creation or privilege escalation events were identified.
- No evidence of persistence or lateral movement was found.

---

# Containment and Response

The following response actions are recommended:

- Continue monitoring authentication activity from the identified source.
- Verify the legitimacy of the source system.
- Review password complexity and account lockout policies.
- Reset credentials if suspicious activity continues.
- Block malicious source IP addresses where appropriate.
- Escalate recurring authentication attacks according to the incident response process.

---

# Lessons Learned

- SIEM correlation rules enable rapid detection of authentication attacks.
- Centralized Windows Event Log collection significantly improves investigation efficiency.
- Custom SPL detection rules reduce analyst response time.
- Mapping detections to the MITRE ATT&CK Framework provides additional context for threat analysis.

---

# Conclusion

The investigation concluded that the detected activity was consistent with a brute-force authentication attempt targeting a Windows user account. Although repeated failed logon attempts were observed, no successful authentication or additional malicious activity was identified during the investigation period.

The incident was documented, monitored, and closed after confirming that no compromise had occurred. Continued monitoring is recommended to identify any recurring authentication attacks against the affected account.
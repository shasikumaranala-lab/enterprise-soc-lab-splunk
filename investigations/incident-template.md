# Security Incident Investigation Template

This template provides a standardized approach for documenting security incidents identified during monitoring, alert triage, and incident response activities. It ensures that every investigation is performed consistently, documented thoroughly, and aligned with Security Operations Center (SOC) best practices.

---

# Incident Overview

## Incident Summary

Provide a brief overview of the incident, including how it was detected, the suspected threat, and the overall outcome of the investigation.

Example:

> A high-severity authentication alert was generated after multiple failed Windows logon attempts were detected against a privileged account within a five-minute period. The activity was investigated using Splunk Enterprise and Windows Security Event Logs to determine whether unauthorized access had occurred.

---

# Incident Information

| Field | Value |
|--------|-------|
| Incident ID | |
| Incident Name | |
| Detection Rule | |
| Severity | Low / Medium / High / Critical |
| Priority | Low / Medium / High |
| Status | Open / In Progress / Closed |
| Analyst | |
| Detection Time | |
| Investigation Start | |
| Investigation End | |
| Data Source | |
| SIEM Platform | |

---

# Incident Description

Describe the suspicious activity that triggered the investigation.

Include information such as:

- What happened?
- How was it detected?
- Why was the activity considered suspicious?
- Which systems or users were affected?

---

# Detection Details

## Detection Logic

Explain the logic used to generate the alert.

Example:

> Detect five or more failed authentication attempts against the same user account within a five-minute period.

### Detection Query

```spl

```

---

# Alert Information

| Field | Value |
|--------|-------|
| Alert Type | |
| Alert Frequency | |
| Trigger Condition | |
| Data Source | |
| Detection Rule | |

---

# Investigation Workflow

## Step 1 — Validate the Alert

### Objective

Describe the purpose of this step.

### Actions Performed

-

### Evidence Collected

-

### Findings

-

---

## Step 2 — Analyze the Activity

### Objective

### Actions Performed

-

### Evidence Collected

-

### Findings

-

---

## Step 3 — Review Related Events

### Objective

### Actions Performed

-

### Evidence Collected

-

### Findings

-

---

## Step 4 — Determine Impact

### Objective

### Actions Performed

-

### Evidence Collected

-

### Findings

-

---

# Timeline of Events

| Time | Activity |
|------|----------|
| | |

---

# Indicators of Compromise (IOCs)

| Indicator | Value |
|-----------|-------|
| Source IP Address | |
| Destination IP Address | |
| Username | |
| Hostname | |
| Process Name | |
| File Hash | |
| Domain | |
| URL | |
| Windows Event ID | |
| Other Indicators | |

---

# Evidence Collected

List all evidence reviewed during the investigation.

Examples:

- Windows Security Event Logs
- System Logs
- Application Logs
- Splunk Search Results
- Authentication Records
- Process Information
- Network Connections
- Security Alerts
- Screenshots
- Threat Intelligence References

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| | | |

---

# Risk Assessment

| Category | Assessment |
|----------|------------|
| Likelihood | |
| Business Impact | |
| Affected Assets | |
| Successful Compromise | Yes / No |
| Privilege Escalation | Yes / No |
| Persistence Observed | Yes / No |

---

# Investigation Findings

Summarize the key observations made during the investigation.

Examples:

- Suspicious activity was confirmed.
- No evidence of unauthorized access was identified.
- No privilege escalation was observed.
- Related events were reviewed.
- Additional monitoring is recommended.

---

# Containment and Response

Document all response actions performed or recommended.

Examples:

- Block malicious IP address
- Disable affected account
- Reset compromised credentials
- Isolate affected endpoint
- Remove malicious files
- Escalate to Incident Response Team
- Continue monitoring

---

# Root Cause Analysis

Identify the most likely cause of the incident.

Examples:

- Brute-force authentication attack
- Weak password policy
- Misconfigured application
- User error
- Malware infection
- Unauthorized administrative activity

---

# Lessons Learned

Document improvements that can reduce future risk.

Examples:

- Improve detection rules.
- Tune alert thresholds.
- Strengthen authentication policies.
- Implement Multi-Factor Authentication (MFA).
- Improve log visibility.
- Update security monitoring procedures.

---

# Conclusion

Provide a final summary of the investigation.

Include:

- Was the incident confirmed?
- Was unauthorized access successful?
- Was remediation completed?
- Are additional actions required?

Example:

> The investigation determined that the detected activity represented repeated failed authentication attempts consistent with a brute-force attack. No successful authentication or evidence of account compromise was identified. The incident was documented, monitored, and closed after confirming that no additional malicious activity occurred.

---

# References

- Related Detection Rule
- Related Investigation
- MITRE ATT&CK Technique
- Internal Security Playbook
- Windows Event Documentation
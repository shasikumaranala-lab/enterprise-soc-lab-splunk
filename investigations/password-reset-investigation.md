# Incident Investigation Report: Password Reset Activity

## Overview

This investigation documents the analysis of a Windows password reset event detected within the Enterprise SOC Lab. The activity was identified through Windows Security Event ID **4724**, which records an attempt to reset a user account password.

Password reset events are considered security-sensitive because they may indicate legitimate administrative maintenance or unauthorized account manipulation following a system compromise. The objective of this investigation was to verify whether the password reset was authorized, identify the administrator who initiated the action, and determine whether any malicious activity occurred before or after the event.

---

# Incident Summary

| Field | Value |
|--------|-------|
| Incident ID | SOC-004 |
| Incident Name | Password Reset Activity |
| Detection Rule | Password Reset Detection |
| Severity | Medium |
| Priority | Medium |
| Status | Closed |
| Detection Time | YYYY-MM-DD HH:MM |
| Investigation Start | YYYY-MM-DD HH:MM |
| Investigation End | YYYY-MM-DD HH:MM |
| Analyst | Anala Shasi Kumar |

---

# Incident Description

A password reset operation was detected through Windows Security Event ID **4724**. Since unauthorized password resets can provide attackers with persistent access to compromised accounts, the activity was investigated to determine whether the action was performed by an authorized administrator and whether any additional suspicious activity occurred.

---

# Detection Details

## Detection Logic

Generate an alert whenever a Windows account password reset event is recorded.

### Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4724** | Password Reset Attempt |
| **4624** | Successful Logon |
| **4625** | Failed Logon |
| **4722** | User Account Enabled |
| **4725** | User Account Disabled |

---

## SPL Detection Query

```spl
index=main EventCode=4724
| table _time Account_Name TargetUserName ComputerName
```

---

# Alert Information

| Field | Value |
|--------|-------|
| Alert Type | Scheduled Alert |
| Data Source | Windows Security Event Log |
| SIEM Platform | Splunk Enterprise |
| Detection Rule | Password Reset Detection |

---

# Investigation Workflow

## Step 1 — Validate the Alert

### Objective

Confirm that a password reset event occurred and verify the corresponding Windows Security Event.

### SPL Query

```spl
index=main EventCode=4724
```

### Findings

- Windows Security Event ID **4724** confirmed that a password reset operation occurred.
- The event contained details of both the initiating account and the affected user account.

---

## Step 2 — Identify the Initiating Account

### Objective

Determine which administrator or user initiated the password reset.

### Fields Reviewed

- Account_Name
- TargetUserName
- ComputerName

### Findings

The initiating account responsible for performing the password reset was successfully identified.

---

## Step 3 — Review Authentication Activity

### Objective

Determine whether the password reset was followed by successful or failed authentication attempts.

### SPL Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
```

### Findings

Authentication events following the password reset were reviewed. No unusual authentication activity or repeated failed logon attempts were identified.

---

## Step 4 — Verify Administrative Authorization

### Objective

Confirm that the password reset was performed as part of an approved administrative process.

### Findings

The password reset was verified as an authorized administrative action with a valid operational purpose.

---

# Timeline of Events

| Time | Activity |
|------|----------|
| 10:00 | Password reset initiated |
| 10:01 | Windows Event ID 4724 generated |
| 10:02 | Splunk detection rule triggered |
| 10:03 | SOC analyst initiated investigation |
| 10:06 | Authentication activity reviewed |
| 10:10 | Investigation completed |
| 10:11 | Incident closed |

---

# Indicators of Compromise (IOCs)

| Indicator | Value |
|-----------|-------|
| Initiating Account | Administrator |
| Target User | Alice |
| Hostname | DC01 |
| Windows Event ID | 4724 |

---

# Evidence Collected

The following evidence was reviewed during the investigation:

- Windows Security Event Logs
- Splunk Search Results
- Password Reset Events
- Authentication Logs
- Administrative Activity
- User Account Information

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Account Manipulation | T1098 |

---

# Risk Assessment

| Category | Assessment |
|----------|------------|
| Likelihood | Low |
| Business Impact | Low |
| Unauthorized Activity | No |
| Account Compromise | Not Observed |
| Privilege Escalation | Not Observed |

---

# Investigation Findings

- A Windows password reset event was successfully identified through Event ID **4724**.
- The initiating administrator account was verified.
- The affected user account was identified.
- Authentication activity following the password reset was reviewed.
- No unauthorized authentication attempts or privilege escalation events were detected.
- The password reset was determined to be an approved administrative operation.

---

# Containment and Response

The following actions are recommended after a password reset event:

- Verify that the password reset request was properly authorized.
- Notify the affected account owner.
- Review authentication activity following the password reset.
- Monitor the account for unusual login behavior.
- Confirm that password policies comply with organizational security standards.

---

# Lessons Learned

- Windows Security Event ID **4724** provides valuable visibility into password management activities.
- Reviewing authentication events after a password reset helps identify potential account compromise.
- Centralized log collection enables rapid verification of administrative actions.
- Continuous monitoring of password management events improves account security.

---

# Conclusion

The investigation determined that the password reset activity was performed by an authorized administrator as part of a legitimate administrative process. No evidence of unauthorized account access, privilege escalation, or malicious activity was identified during the investigation period.

The incident was documented and closed after confirming that the password reset complied with established administrative procedures.
# Incident Investigation Report: New User Account Creation

## Overview

This investigation documents the analysis of a newly created Active Directory user account detected within the Enterprise SOC Lab. The activity was identified through Windows Security Event ID **4720**, which records the creation of a new user account.

The objective of this investigation was to determine whether the account creation was authorized, verify the identity of the administrator who performed the action, review the assigned privileges, and identify any indicators of unauthorized administrative activity.

---

# Incident Summary

| Field | Value |
|--------|-------|
| Incident ID | SOC-002 |
| Incident Name | New User Account Creation |
| Detection Rule | New User Detection |
| Severity | Medium |
| Priority | Medium |
| Status | Closed |
| Detection Time | YYYY-MM-DD HH:MM |
| Investigation Start | YYYY-MM-DD HH:MM |
| Investigation End | YYYY-MM-DD HH:MM |
| Analyst | Anala Shasi Kumar |

---

# Incident Description

A new Active Directory user account was detected through Windows Security Event ID **4720**. Since unauthorized account creation may indicate privilege abuse, persistence, or unauthorized administrative activity, the event was reviewed to determine whether it was part of an approved administrative operation.

---

# Detection Details

## Detection Logic

Generate an alert whenever a new Active Directory user account is created.

### Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4720** | User Account Created |
| **4728** | User Added to Global Security Group |
| **4732** | User Added to Local Security Group |
| **4624** | Successful Logon (Reviewed) |

---

## SPL Detection Query

```spl
index=main EventCode=4720
| table _time Account_Name TargetUserName ComputerName
```

---

# Alert Information

| Field | Value |
|--------|-------|
| Alert Type | Scheduled Alert |
| Data Source | Windows Security Event Log |
| SIEM Platform | Splunk Enterprise |
| Detection Rule | New User Detection |

---

# Investigation Workflow

## Step 1 — Validate the Alert

### Objective

Confirm that a new user account was created and verify the associated Windows security event.

### SPL Query

```spl
index=main EventCode=4720
```

### Findings

- Windows Security Event ID **4720** confirmed the creation of a new user account.
- The event contained the administrator account responsible for creating the user.

---

## Step 2 — Identify the Administrator

### Objective

Determine which account performed the administrative action.

### Fields Reviewed

- Account_Name
- TargetUserName
- ComputerName

### Findings

The administrator account responsible for creating the user account was successfully identified.

---

## Step 3 — Review Assigned Privileges

### Objective

Verify whether the newly created account received elevated permissions.

### Windows Events Reviewed

| Event ID | Description |
|----------|-------------|
| 4728 | User Added to Global Security Group |
| 4732 | User Added to Local Security Group |

### Findings

No privileged group membership assignments were detected during the investigation.

---

## Step 4 — Verify Administrative Authorization

### Objective

Determine whether the account creation was part of an approved administrative activity.

### Findings

The account creation was confirmed as an authorized administrative action with a valid business purpose.

---

# Timeline of Events

| Time | Activity |
|------|----------|
| 10:00 | New user account created |
| 10:01 | Windows Security Event ID 4720 generated |
| 10:02 | Splunk detection rule triggered |
| 10:03 | SOC analyst initiated investigation |
| 10:06 | Administrative activity reviewed |
| 10:10 | Investigation completed |
| 10:11 | Incident closed |

---

# Indicators of Compromise (IOCs)

| Indicator | Value |
|-----------|-------|
| Administrator Account | Administrator |
| New User Account | Alice |
| Hostname | DC01 |
| Windows Event ID | 4720 |

---

# Evidence Collected

The following evidence was reviewed during the investigation:

- Windows Security Event Logs
- Active Directory User Information
- Splunk Search Results
- Administrative Account Activity
- Group Membership Events

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Create Account | T1136 |

---

# Risk Assessment

| Category | Assessment |
|----------|------------|
| Likelihood | Low |
| Business Impact | Low |
| Unauthorized Activity | No |
| Privilege Escalation | Not Observed |
| Persistence | Not Observed |

---

# Investigation Findings

- A new Active Directory user account was successfully created.
- The account creation event was confirmed through Windows Security Event ID **4720**.
- The administrator responsible for the action was successfully identified.
- No privileged group memberships were assigned to the newly created account.
- No indicators of malicious activity or unauthorized administrative actions were observed.
- The account creation was determined to be an approved administrative operation.

---

# Containment and Response

The following actions are recommended after new account creation:

- Verify that the account creation request was approved.
- Review assigned permissions and group memberships.
- Monitor initial authentication activity for the new account.
- Confirm compliance with organizational user provisioning procedures.
- Continue monitoring for any unexpected privilege changes.

---

# Lessons Learned

- Windows Security Event ID **4720** provides valuable visibility into account provisioning activities.
- Centralized log collection enables rapid validation of administrative actions.
- Reviewing related group membership events helps identify unauthorized privilege assignments.
- Monitoring newly created accounts improves visibility into potential persistence techniques.

---

# Conclusion

The investigation determined that the new Active Directory user account was created through an authorized administrative process. No evidence of privilege escalation, unauthorized administrative activity, or persistence mechanisms was identified during the investigation.

The incident was documented and closed after confirming that the account creation complied with expected administrative procedures.
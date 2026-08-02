# Incident Investigation Report: Privileged Group Membership Change

## Overview

This investigation documents the analysis of a privileged Active Directory group membership modification detected within the Enterprise SOC Lab. The activity was identified through Windows Security Event IDs **4728** and **4732**, which record users being added to privileged security groups.

Changes to privileged group memberships are considered high-risk administrative events because they may grant elevated permissions that could enable unauthorized access, privilege escalation, or persistence within the environment. The objective of this investigation was to verify whether the membership change was authorized, identify the administrator who performed the action, and determine whether the activity indicated malicious behavior.

---

# Incident Summary

| Field | Value |
|--------|-------|
| Incident ID | SOC-003 |
| Incident Name | Privileged Group Membership Change |
| Detection Rule | Privileged Group Membership Detection |
| Severity | High |
| Priority | High |
| Status | Closed |
| Detection Time | YYYY-MM-DD HH:MM |
| Investigation Start | YYYY-MM-DD HH:MM |
| Investigation End | YYYY-MM-DD HH:MM |
| Analyst | Anala Shasi Kumar |

---

# Incident Description

A Windows security event indicated that a user account was added to a privileged Active Directory security group. Since unauthorized privilege assignments may indicate account compromise or malicious administrative activity, the event was investigated to verify whether the modification was approved and consistent with organizational security policies.

---

# Detection Details

## Detection Logic

Generate an alert whenever a user account is added to a privileged Active Directory security group.

### Windows Event IDs

| Event ID | Description |
|----------|-------------|
| **4728** | Member Added to Global Security Group |
| **4732** | Member Added to Local Security Group |
| **4624** | Successful Logon (Reviewed) |
| **4720** | User Account Created (Reviewed) |

---

## SPL Detection Query

```spl
index=main (EventCode=4728 OR EventCode=4732)
| table _time MemberName GroupName ComputerName
```

---

# Alert Information

| Field | Value |
|--------|-------|
| Alert Type | Scheduled Alert |
| Data Source | Windows Security Event Log |
| SIEM Platform | Splunk Enterprise |
| Detection Rule | Privileged Group Membership Detection |

---

# Investigation Workflow

## Step 1 — Validate the Alert

### Objective

Confirm that a privileged group membership modification occurred.

### SPL Query

```spl
index=main (EventCode=4728 OR EventCode=4732)
```

### Findings

- Windows Security Event IDs **4728** and **4732** confirmed that a user account was added to a privileged security group.
- The event contained details of the affected account and the modified group.

---

## Step 2 — Identify the Modified Group

### Objective

Determine which privileged group was modified.

### Fields Reviewed

- MemberName
- GroupName
- ComputerName

### Findings

The affected security group was identified and verified as a privileged Active Directory group.

---

## Step 3 — Verify Administrative Authorization

### Objective

Determine whether the group membership change was approved and performed by an authorized administrator.

### Findings

The administrative account responsible for the modification was successfully identified. The membership change was verified as an approved administrative action.

---

## Step 4 — Review Related Authentication Activity

### Objective

Review recent authentication activity associated with the affected account to identify any indicators of compromise.

### SPL Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
```

### Findings

Authentication activity was reviewed following the group membership change. No suspicious authentication attempts or unauthorized administrative actions were observed.

---

# Timeline of Events

| Time | Activity |
|------|----------|
| 10:00 | User added to privileged security group |
| 10:01 | Windows Security Event generated |
| 10:02 | Splunk detection rule triggered |
| 10:03 | SOC analyst initiated investigation |
| 10:07 | Administrative activity verified |
| 10:10 | Authentication events reviewed |
| 10:12 | Investigation completed |
| 10:13 | Incident closed |

---

# Indicators of Compromise (IOCs)

| Indicator | Value |
|-----------|-------|
| Administrator Account | Administrator |
| Affected User | Alice |
| Privileged Group | Domain Admins |
| Hostname | DC01 |
| Windows Event ID | 4728 / 4732 |

---

# Evidence Collected

The following evidence was reviewed during the investigation:

- Windows Security Event Logs
- Active Directory Group Membership Information
- Splunk Search Results
- Authentication Logs
- Administrative Activity
- Group Membership Records

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Account Manipulation | T1098 |
| Privilege Escalation | Account Manipulation | T1098 |

---

# Risk Assessment

| Category | Assessment |
|----------|------------|
| Likelihood | Medium |
| Business Impact | High |
| Unauthorized Activity | No |
| Privilege Escalation | Not Observed |
| Persistence | Not Observed |

---

# Investigation Findings

- A privileged Active Directory security group membership change was successfully detected.
- The affected user account and privileged group were identified.
- The administrative account responsible for the modification was verified.
- Authentication activity associated with the affected account was reviewed.
- No evidence of unauthorized administrative activity or privilege abuse was identified.
- The group membership change was determined to be an approved administrative operation.

---

# Containment and Response

The following actions are recommended after privileged group membership modifications:

- Verify that the membership change was approved through the organization's change management process.
- Review assigned privileges to ensure compliance with the Principle of Least Privilege.
- Monitor authentication activity associated with the affected account.
- Audit future modifications to privileged security groups.
- Remove unnecessary privileged group memberships where appropriate.

---

# Lessons Learned

- Windows Security Event IDs **4728** and **4732** provide valuable visibility into privileged account management.
- Continuous monitoring of privileged group membership changes helps detect unauthorized privilege escalation.
- Centralized logging and SIEM correlation improve the ability to investigate high-risk administrative events.
- Regular privilege audits help reduce the risk of excessive permissions.

---

# Conclusion

The investigation determined that the privileged group membership change was performed by an authorized administrator as part of a legitimate administrative process. No evidence of unauthorized privilege escalation, account compromise, or malicious activity was identified during the investigation period.

The incident was documented and closed after confirming that the modification complied with established administrative procedures and security policies.
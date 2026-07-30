# Incident Investigation: Brute Force Authentication Attempt

## Incident Summary

A high number of failed authentication attempts were detected against a Windows account within a short period. The activity matched the organization's brute-force detection rule and triggered an alert in Splunk.

---

## Incident Information

| Field | Value |
|--------|-------|
| Incident ID | SOC-001 |
| Detection Name | Brute Force Detection |
| Severity | High |
| Status | Closed |
| Date | YYYY-MM-DD |
| Analyst | Shasi Kumar Yadav |

---

## Detection Rule

The following SPL query was used to identify repeated failed authentication attempts:

```spl
index=main EventCode=4625
| bucket _time span=5m
| stats count by _time Account_Name Source_Network_Address
| where count >= 5
| sort -count
```

---

## Alert Details

| Field | Value |
|--------|-------|
| Windows Event ID | 4625 |
| Alert Type | Scheduled Alert |
| Schedule | Every 5 Minutes |
| Trigger | More than 5 failed logins |

---

## Investigation Process

### Step 1 - Review Authentication Events

Search:

```spl
index=main EventCode=4625
```

Observation:

- Multiple failed login attempts detected.

---

### Step 2 - Identify Target User

Fields reviewed:

- Account_Name
- ComputerName
- Source_Network_Address

Result:

Repeated authentication failures against the same account.

---

### Step 3 - Check for Successful Authentication

Search:

```spl
index=main EventCode=4624
```

Observation:

No successful authentication observed after the failed attempts.

---

### Step 4 - Review Related Security Events

Reviewed:

- New User Creation (4720)
- Privileged Group Changes (4728 / 4732)
- Password Reset (4724)

No suspicious activity was identified.

---

## Timeline

| Time | Event |
|------|-------|
| 10:00 | Failed login attempts started |
| 10:03 | Splunk alert generated |
| 10:05 | Investigation initiated |
| 10:10 | Source host reviewed |
| 10:15 | Incident closed |

---

## Indicators of Compromise (IOCs)

| IOC | Value |
|------|------|
| Username | Administrator |
| Host | WIN-SERVER-01 |
| Source IP | 172.20.10.X |
| Event ID | 4625 |

---

## MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Brute Force | T1110 |
| Valid Accounts | T1078 |

---

## Findings

- Multiple failed authentication attempts detected.
- No successful login observed.
- No evidence of privilege escalation.
- No persistence mechanisms identified.

---

## Recommended Response

- Monitor future authentication attempts.
- Review account lockout policies.
- Enforce strong password requirements.
- Investigate repeated authentication failures from the same source.

---

## Lessons Learned

- Centralized logging enables rapid identification of authentication attacks.
- Splunk alerts help reduce investigation time.
- Windows Event IDs provide valuable information for incident analysis.
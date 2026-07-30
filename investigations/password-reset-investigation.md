# Incident Investigation: Password Reset Activity

## Incident Summary

A Windows account password reset was detected and investigated to determine whether it was authorized.

---

## Incident Information

| Field | Value |
|--------|-------|
| Incident ID | SOC-004 |
| Severity | Medium |
| Status | Closed |

---

## Detection Rule

```spl
index=main EventCode=4724
| table _time Account_Name TargetUserName ComputerName
```

---

## Investigation Steps

1. Identify the affected account.
2. Verify who initiated the password reset.
3. Confirm the change request.
4. Review recent login activity.

---

## Findings

- Password reset completed successfully.
- No suspicious activity observed.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Account Manipulation | T1098 |

---

## Recommended Response

- Notify the account owner.
- Monitor subsequent authentication events.
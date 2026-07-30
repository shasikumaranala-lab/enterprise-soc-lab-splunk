# Incident Investigation: New User Account Created

## Incident Summary

A new Active Directory user account was created. The event was detected through Windows Security Event ID 4720 and reviewed to determine whether the account creation was authorized.

---

## Incident Information

| Field | Value |
|--------|-------|
| Incident ID | SOC-002 |
| Detection Name | New User Detection |
| Severity | Medium |
| Status | Closed |
| Analyst | Shasi Kumar Yadav |

---

## Detection Rule

```spl
index=main EventCode=4720
| table _time Account_Name TargetUserName ComputerName
```

---

## Investigation Steps

1. Identify the account that created the new user.
2. Verify the newly created username.
3. Review group memberships.
4. Confirm the request with the administrator.

---

## Findings

- A new user account was successfully created.
- The account creation was authorized.
- No suspicious privilege assignments were identified.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Create Account | T1136 |

---

## Recommended Response

- Verify approval.
- Review assigned permissions.
- Monitor initial login activity.
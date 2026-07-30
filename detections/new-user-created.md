# New User Account Created

## Objective

Detect creation of new Windows user accounts.

---

## MITRE ATT&CK

| Technique | ID |
|------------|------|
| Create Account | T1136 |

---

## Severity

Medium

---

## Windows Event IDs

- 4720

---

## SPL Query

```spl
index=main EventCode=4720
| table _time Account_Name TargetUserName ComputerName
```

---

## Investigation Steps

1. Verify who created the account.
2. Confirm business justification.
3. Check group memberships.
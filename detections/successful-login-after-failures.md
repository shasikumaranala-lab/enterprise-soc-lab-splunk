# Successful Login After Multiple Failed Attempts

## Objective

Detect a successful Windows logon that follows multiple failed authentication attempts.

---

## MITRE ATT&CK

| Technique | ID |
|------------|------|
| Valid Accounts | T1078 |

---

## Severity

High

---

## Windows Event IDs

- 4624
- 4625

---

## SPL Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
| transaction Account_Name maxspan=10m
| search EventCode=4625 EventCode=4624
```

---

## Investigation Steps

1. Review failed logon attempts.
2. Verify successful authentication.
3. Confirm source workstation.
4. Determine if credentials were compromised.
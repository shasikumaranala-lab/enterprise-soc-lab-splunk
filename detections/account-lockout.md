# Account Lockout Detection

## Objective

Detect locked Windows accounts.

---

## Event ID

4740

---

## SPL

```spl
index=main EventCode=4740
| table _time TargetUserName CallerComputerName
```
# Privileged Group Membership Change

## Objective

Detect users being added to privileged security groups.

---

## MITRE ATT&CK

| Technique | ID |
|------------|------|
| Account Manipulation | T1098 |

---

## Severity

High

---

## Windows Event IDs

- 4728
- 4732

---

## SPL Query

```spl
index=main (EventCode=4728 OR EventCode=4732)
| table _time MemberName GroupName ComputerName
```
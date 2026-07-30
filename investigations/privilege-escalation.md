# Incident Investigation: Privileged Group Membership Change

## Incident Summary

A user account was added to a privileged Active Directory security group.

---

## Incident Information

| Field | Value |
|--------|-------|
| Incident ID | SOC-003 |
| Severity | High |
| Status | Closed |

---

## Detection Rule

```spl
index=main (EventCode=4728 OR EventCode=4732)
| table _time MemberName GroupName ComputerName
```

---

## Investigation Steps

1. Identify the modified group.
2. Verify the user added.
3. Confirm administrative approval.
4. Review recent authentication activity.

---

## Findings

- User was added to a privileged group.
- Administrative approval was confirmed.

---

## MITRE ATT&CK

| Technique | ID |
|-----------|----|
| Account Manipulation | T1098 |

---

## Recommended Response

- Review group membership.
- Apply least privilege.
- Audit future membership changes.
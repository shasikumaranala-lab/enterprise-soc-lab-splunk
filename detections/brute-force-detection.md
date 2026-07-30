# Brute Force Detection

## Objective

Detect repeated failed Windows authentication attempts that may indicate a brute-force attack against a user account.

---

## MITRE ATT&CK

| Technique | ID |
|------------|------|
| Brute Force | T1110 |

---

## Severity

High

---

## Windows Event IDs

- 4625 - Failed Logon

---

## Detection Logic

Generate an alert when five or more failed logon attempts are observed for the same account within a five-minute window.

---

## SPL Query

```spl
index=main EventCode=4625
| bucket _time span=5m
| stats count by _time Account_Name Source_Network_Address
| where count >= 5
| sort -count
```

---

## Example Output

| Time | User | Source IP | Count |
|------|------|-----------|------|
|10:05|Administrator|172.20.10.20|8|

---

## Investigation Steps

1. Verify the targeted user account.
2. Identify the source IP address.
3. Review additional authentication activity.
4. Determine whether a successful login occurred.
5. Check for account lockout events.

---

## Possible False Positives

- User repeatedly entering an incorrect password.
- Misconfigured scheduled tasks.
- Services using outdated credentials.

---

## Recommended Response

- Lock the affected account if malicious activity is confirmed.
- Block the source IP if appropriate.
- Reset the user's password.
- Review additional authentication logs.
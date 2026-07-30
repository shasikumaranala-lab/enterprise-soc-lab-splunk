# Authentication Queries

This document contains common SPL queries used to investigate Windows authentication events.

---

## Successful Logins

### Purpose

Display successful Windows logon events.

```spl
index=main EventCode=4624
| table _time Account_Name ComputerName Source_Network_Address Logon_Type
```

---

## Failed Logins

### Purpose

Display failed Windows logon attempts.

```spl
index=main EventCode=4625
| table _time Account_Name ComputerName Source_Network_Address Failure_Reason
```

---

## Top Failed Login Accounts

### Purpose

Identify accounts with the highest number of failed logins.

```spl
index=main EventCode=4625
| stats count by Account_Name
| sort -count
```

---

## Authentication Activity by Host

### Purpose

View authentication activity grouped by computer.

```spl
index=main (EventCode=4624 OR EventCode=4625)
| stats count by ComputerName
```
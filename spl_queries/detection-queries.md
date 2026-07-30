# Detection Queries

This document contains the SPL queries used for security detections.

---

## Brute Force Detection

```spl
index=main EventCode=4625
| bucket _time span=5m
| stats count by _time Account_Name Source_Network_Address
| where count >= 5
```

---

## Successful Login After Failed Attempts

```spl
index=main (EventCode=4624 OR EventCode=4625)
| transaction Account_Name maxspan=10m
| search EventCode=4625 EventCode=4624
```

---

## New User Created

```spl
index=main EventCode=4720
| table _time Account_Name TargetUserName
```

---

## Privileged Group Membership Change

```spl
index=main (EventCode=4728 OR EventCode=4732)
| table _time MemberName GroupName
```

---

## Password Reset

```spl
index=main EventCode=4724
| table _time Account_Name TargetUserName
```

---

## Account Lockout

```spl
index=main EventCode=4740
| table _time TargetUserName CallerComputerName
```
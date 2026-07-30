# Windows Event Queries

Reference queries for commonly monitored Windows Security Events.

---

## User Account Created

**Event ID:** 4720

```spl
index=main EventCode=4720
```

---

## User Account Deleted

**Event ID:** 4726

```spl
index=main EventCode=4726
```

---

## Password Reset

**Event ID:** 4724

```spl
index=main EventCode=4724
```

---

## Account Lockout

**Event ID:** 4740

```spl
index=main EventCode=4740
```

---

## Failed Login

**Event ID:** 4625

```spl
index=main EventCode=4625
```

---

## Successful Login

**Event ID:** 4624

```spl
index=main EventCode=4624
```

---

## Privileged Group Membership Change

**Event IDs:** 4728, 4732

```spl
index=main (EventCode=4728 OR EventCode=4732)
```

---

## Logoff Events

**Event ID:** 4634

```spl
index=main EventCode=4634
```
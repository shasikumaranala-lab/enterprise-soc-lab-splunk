# Password Reset Detection

## Objective

Monitor Windows password reset activity.

---

## Event ID

4724

---

## SPL

```spl
index=main EventCode=4724
| table _time Account_Name TargetUserName
```
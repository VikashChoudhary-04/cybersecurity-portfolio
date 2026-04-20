# 🔴 SQL Injection (Authentication Bypass)

## Description

- Login functionality is vulnerable to SQL Injection.

---

## Payload

```sql
admin' OR 1=1--
```

---

## Impact

* Full system compromise
* Admin access

---

## Fix

* Use prepared statements
* Validate inputs

---

# 🟠 IDOR Vulnerability

## Description

- Users can access other users’ data by modifying object IDs.

---

## Example

```http
GET /rest/basket/2
```

---

## Impact

* Unauthorized data access
* Privacy violation

---

## Fix

* Implement access control checks

---

# 🔥 High-Impact Vulnerability Reports

---

## 🔴 SQL Injection → Authentication Bypass

### Severity

- Critical

---

### Description

- The login functionality is vulnerable to SQL Injection, allowing an attacker to bypass authentication and gain administrative access.

---

### Steps to Reproduce

1. Navigate to login page
2. Enter the following payload:

```
admin' OR 1=1--
```

3. Enter any password
4. Submit the request

---

### Result

* Authentication bypass successful
* Logged in as administrator

---

### Impact

- An attacker can gain full administrative access without valid credentials, allowing:

  * Complete control over application functionality
  * Access to all user data
  * Ability to perform privileged operations

---

### Recommendation

* Use parameterized queries (prepared statements)
* Avoid dynamic SQL queries
* Implement input validation

---

## 🟠 IDOR → Unauthorized Data Access

### Severity

- High

---

### Description

- The application fails to enforce proper authorization checks, allowing users to access other users’ data by modifying object identifiers.

---

### Steps to Reproduce

1. Send request:

```
GET /rest/basket/1
```

2. Modify the ID:

```
GET /rest/basket/2
```

3. Observe response

---

### Result

* Data belonging to another user is returned

---

### Impact

- An attacker can access sensitive user data without authorization, leading to:

  * Privacy violations
  * Exposure of user-specific information
  * Potential misuse of data

---

### Recommendation

* Implement strict server-side authorization checks
* Validate ownership of resources before returning data

---

# 🧾 Final Vulnerability Reports

---

# 🔴 SQL Injection → Authentication Bypass

## 🧩 Vulnerability

- SQL Injection

## 🎯 Severity

- Critical

---

## 📝 Description

- The login functionality is vulnerable to SQL Injection due to improper input sanitization.
- An attacker can manipulate the SQL query to bypass authentication and gain administrative access.

---

## 🔁 Steps to Reproduce

1. Navigate to login page
2. Enter the following payload:

```
admin' OR 1=1--
```

3. Enter any password
4. Submit the login request

---

## ✅ Result

* Authentication bypass successful
* Logged in as administrator

---

## 💥 Impact

- An attacker can gain full administrative access without valid credentials.

- This allows:

  * Full control over the application
  * Access to all user data
  * Ability to perform privileged operations

---

## 🛡️ Recommendation

* Use parameterized queries (prepared statements)
* Avoid dynamic SQL queries
* Validate and sanitize all user inputs

---

# 🟠 IDOR → Unauthorized Data Access

## 🧩 Vulnerability

- Insecure Direct Object Reference (IDOR)

## 🎯 Severity

- High

---

## 📝 Description

- The application does not enforce proper authorization checks when accessing user-specific resources.
- An attacker can modify object identifiers to access data belonging to other users.

---

## 🔁 Steps to Reproduce

1. Send request:

```
GET /rest/basket/1
```

2. Modify the ID:

```
GET /rest/basket/2
```

3. Observe the response

---

## ✅ Result

* Data from another user is returned without authorization

---

## 💥 Impact

- An attacker can access sensitive user data without permission.

- This can lead to:

  * Privacy violations
  * Exposure of user-specific data
  * Potential misuse of user information

---

## 🛡️ Recommendation

* Enforce strict server-side authorization checks
* Validate ownership of resources before returning data
* Implement access control mechanisms

---

# 🧾 Draft Vulnerability Reports

---

## 🔴 1. SQL Injection → Authentication Bypass

### Severity

- Critical

### Description

- The login functionality is vulnerable to SQL Injection, allowing an attacker to bypass authentication and gain administrative access.

---

### Steps to Reproduce

1. Go to login page
2. Enter the following payload:

```
admin' OR 1=1--
```

3. Enter any password
4. Submit the request

---

### Result

* Authentication bypass successful
* Logged in as admin

---

### Impact

* Full system compromise
* Access to all user data
* Ability to perform privileged actions

---

### Recommendation

* Use parameterized queries (prepared statements)
* Implement input validation
* Apply proper authentication checks

---

## 🟠 2. IDOR → Unauthorized Data Access

### Severity

- High

### Description

- The application does not properly validate ownership of resources, allowing users to access other users’ data by modifying object IDs.

---

### Steps to Reproduce

1. Send request:

```
GET /rest/basket/2
```

2. Modify ID:

```
GET /rest/basket/3
```

---

### Result

* Access to other users' basket data

---

### Impact

* Exposure of sensitive user data
* Privacy violation

---

### Recommendation

* Implement server-side authorization checks
* Validate user ownership for each request

---

## 🟡 3. DOM-based XSS

### Severity

- Medium

### Description

- The search functionality is vulnerable to DOM-based XSS, allowing execution of arbitrary JavaScript in the user's browser.

---

### Steps to Reproduce

1. Enter the following payload in search:

```html
<img src=x onerror=alert(1)>
```

---

### Result

* JavaScript executes in browser

---

### Impact

* Client-side manipulation
* Limited data exposure (non-sensitive cookies only)

---

### Recommendation

* Sanitize user input
* Use secure output encoding
* Implement Content Security Policy (CSP)

---

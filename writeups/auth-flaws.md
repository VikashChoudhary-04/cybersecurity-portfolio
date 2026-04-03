# 🔐 Authentication Flaws — OWASP Juice Shop

---

## 📌 Objective

- Assess authentication mechanisms for weaknesses, including login bypass, password reset flaws, and token/session handling.

---

# 🧪 1. Login Bypass via Input Manipulation

## 🎯 Endpoint

POST /rest/user/login

---

## 🪜 Steps to Reproduce

1. Intercepted login request using Burp Suite
2. Modified request payload as follows:

```json
{
  "email": "admin' OR 1=1--",
  "password": "123"
}
```

3. Sent modified request to server

---

## 🔍 Observation

* Server responded with **HTTP 200 OK**
* Authentication was successful despite invalid credentials
* Response contained a valid JWT token

```json
{
  "role": "admin",
  "email": "admin@juice-sh.op"
}
```

* User was successfully logged in as **administrator**

---

## 💣 Vulnerability

- The application is vulnerable to **authentication bypass via SQL injection or improper input validation**.

- User input is not properly sanitized before being processed in authentication logic.

---

## 💥 Impact

- An attacker can:

  * Bypass authentication completely
  * Log in as any user (including admin)
  * Gain full control over application functionality

---

## 🧠 Business Impact

- This vulnerability can lead to:

  * Complete account takeover
  * Unauthorized administrative access
  * Data exposure and modification
  * Full compromise of application integrity

---

# 🧪 2. Password Reset Analysis

## 🎯 Feature

- Forgot Password functionality

---

## 🪜 Steps Performed

1. Accessed password reset feature
2. Intercepted request using Burp Suite
3. Observed parameters and validation logic

---

## 🔍 Observation

* Password reset requires proper validation (email/security question/token)
* No direct bypass identified during testing

---

## 💣 Conclusion

- No exploitable vulnerability identified in password reset flow during initial testing.

---

# 🧪 3. Token / Session Analysis

## 🎯 Mechanism

- JWT-based authentication

---

## 🪜 Steps Performed

1. Captured JWT token from login response
2. Decoded token using a JWT decoder
3. Observed contents:

   * User ID
   * Email
   * Role (admin)

---

## 🔍 Observation

* Token contains sensitive user information
* Token is used for authentication in subsequent requests
* Signature validation appears to be enforced (no successful tampering observed)

---

## 💣 Conclusion

* JWT is securely signed and cannot be modified directly
* However, token exposure combined with login bypass increases risk significantly

---

# ⚠️ Overall Security Impact

* **Severity:** Critical
* **Attack Vector:** Remote

- An attacker can gain administrative access without valid credentials, leading to complete compromise of the application.

---

# 🛠️ Recommended Fixes

* Implement proper input validation and sanitization
* Use parameterized queries to prevent SQL injection
* Avoid direct use of user input in authentication logic
* Implement account lockout and rate limiting
* Ensure secure handling of authentication tokens

---

# 🧠 Key Takeaways

* Authentication systems must never trust raw user input
* Improper validation can lead to full system compromise
* Even a single flaw in login logic can expose the entire application

---

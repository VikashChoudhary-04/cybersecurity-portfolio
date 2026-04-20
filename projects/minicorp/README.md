# 🏢 MiniCorp Security Assessment

## 📌 Overview

- This project demonstrates a structured penetration test performed on a simulated web application (MiniCorp).

- The objective was to identify vulnerabilities, validate their impact, and present findings in a professional format aligned with real-world pentesting practices.

---

## 🎯 Scope

* Authentication system
* User data access
* Input handling mechanisms

---

## 🧠 Methodology

The assessment followed a structured workflow:

1. Reconnaissance (attack surface mapping)
2. Input identification
3. Vulnerability testing (XSS, IDOR, SQL Injection)
4. Exploitation
5. Validation (false positive removal)
6. Reporting

---

## 🔥 Key Findings

### 🔴 SQL Injection → Authentication Bypass

* Successfully bypassed login using injection payload
* Gained administrative access

---

### 🟠 IDOR → Unauthorized Data Access

* Accessed other users’ data by modifying object IDs
* No ownership validation present

---

### 🟡 XSS → Client-side Execution

* Executed arbitrary JavaScript in browser
* Impact limited due to secure cookie handling

---

## 📊 Impact Summary

* Unauthorized system access
* Exposure of user data
* Potential client-side manipulation

---

## 🛡️ Recommendations

* Use parameterized queries (prevent SQL Injection)
* Implement strict access control (prevent IDOR)
* Sanitize and encode user input (prevent XSS)

---

## 📌 Conclusion

- This assessment demonstrates the ability to identify and validate real-world vulnerabilities using a structured and professional approach.

---

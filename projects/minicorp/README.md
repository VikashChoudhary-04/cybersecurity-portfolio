# 🏢 MiniCorp Security Assessment (Simulation)

## 📌 Overview

- MiniCorp is a simulated web application used to demonstrate real-world penetration testing methodology.

- The goal was to identify vulnerabilities, validate them, and assess their impact.

---

## 🔍 Scope

* Authentication system
* User data access
* Input fields

---

## 🔥 Key Findings

### 🔴 SQL Injection → Authentication Bypass

* Bypassed login using crafted input
* Gained administrative access

---

### 🟠 IDOR → Unauthorized Data Access

* Accessed other users’ data by modifying IDs

---

### 🟡 XSS → Client-side Execution

* Executed JavaScript in browser

---

## 🧠 Attack Flow

Recon → Input Mapping → Exploitation → Validation → Reporting

---

## 📊 Impact

* Unauthorized access
* Data exposure
* System compromise

---

## 🛡️ Recommendations

* Input validation
* Parameterized queries
* Proper authorization checks

---

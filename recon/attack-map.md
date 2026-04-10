# 🧠 Attack Surface Map — OWASP Juice Shop

---

## 📌 Objective

- Combine reconnaissance and exploitation findings to build a complete attack surface map and identify potential attack paths.

---

## 🌐 1. Identified Services (Nmap)

* Port 3000 — Node.js (OWASP Juice Shop)
* Port 80 — Apache HTTP Server
* Port 3306 — MariaDB (Database)
* Port 22 — SSH
* Port 36791 — Unknown service

---

## 🔍 2. Discovered Endpoints (ffuf + dirsearch)

### API Endpoints

* /rest/products
* /rest/user
* /rest/basket

---

### Additional Endpoint

* /.well-known/security.txt

---

### ⚠️ Observation

* Application uses SPA behavior
* Invalid routes return identical responses
* Required filtering to remove false positives

---

## 💣 3. Identified Vulnerabilities

### Web Application

* DOM-based XSS (Search input)
* Authentication bypass (SQL Injection in login)
* IDOR (Basket manipulation)
* File upload functionality

---

### Infrastructure

* Database exposed (Port 3306)
* SSH service exposed (Port 22)
* Unknown service (Port 36791)

---

## 🎯 4. Entry Points

* Search functionality
* Login form
* API endpoints
* File upload feature

---

## 🔗 5. Attack Chains

### Chain 1 — XSS → Account Takeover

* Inject JavaScript via search
* Steal session/token
* Hijack user account

---

### Chain 2 — SQL Injection → Admin Access

* Bypass login authentication
* Gain admin privileges
* Access sensitive functionality

---

### Chain 3 — IDOR → Data Exposure

* Modify object IDs
* Access other users’ data
* Extract sensitive information

---

### Chain 4 — File Upload → Potential RCE

* Upload malicious file
* Attempt execution (if bypass achieved)

---

## 🧠 6. Attack Surface Summary

- The application exposes multiple attack vectors:

  * Web layer vulnerabilities (XSS, SQLi, IDOR)
  * API-level weaknesses
  * Infrastructure exposure (database, SSH)
  * Hidden or unknown services

---

## ⚠️ Risk Assessment

* High risk due to authentication bypass
* Critical impact if database access is achieved
* Multiple vulnerability chaining possibilities

---

## 🧠 Key Takeaways

* Reconnaissance + exploitation must be combined
* Attack surface includes both application and infrastructure
* Vulnerability chaining significantly increases impact
* Understanding system architecture is critical for real pentesting

---

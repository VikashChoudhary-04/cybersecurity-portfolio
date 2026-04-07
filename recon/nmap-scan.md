# 🌐 Nmap Scan — Attack Surface Analysis

---

## 📌 Objective

- Identify open ports, running services, and potential attack surface using Nmap.

---

## 🧪 1. Full Port Scan

### Command Used

```bash
nmap -p- localhost
```

---

### 🔍 Open Ports Identified

* 22/tcp — SSH
* 80/tcp — HTTP
* 3306/tcp — MySQL (MariaDB)
* 36791/tcp — Unknown service

---

## 🧪 2. Service Detection

### Command Used

```bash
nmap -sC -sV localhost
```

---

### 🔍 Services and Versions

#### 🔹 Port 22 — SSH

* Service: OpenSSH
* Version: OpenSSH 10.2p1 Debian

---

#### 🔹 Port 80 — HTTP

* Service: Apache HTTP Server
* Version: Apache 2.4.65 (Debian)
* Page: Default Apache page ("It works")

---

#### 🔹 Port 3306 — Database

* Service: MariaDB
* Version: 11.8.3-MariaDB
* Authentication: mysql_native_password

---

#### 🔹 Port 36791 — Unknown

* Service: Not identified
* Requires further investigation

---

### 🧠 Attack Surface Analysis

The system exposes multiple services, increasing the overall attack surface:

---

### 🌐 Web Services

* Port 80 (Apache) → Possible misconfigurations, outdated modules
* Port 3000 (Juice Shop) → Main application target

---

### 🗄️ Database Exposure (High Risk)

* Port 3306 (MariaDB) is accessible
* Potential risks:

  * Unauthorized database access
  * Weak credentials
  * Data exposure

---

### 🔐 SSH Access

* Port 22 (SSH) exposed
* Potential risks:

  * Brute-force attacks
  * Credential reuse

---

### ❓ Unknown Service

* Port 36791 open
* May expose hidden functionality or internal service
* Requires further enumeration

---

## ⚠️ Security Risks

* Multiple exposed services increase attack surface
* Database service exposed externally (high risk)
* Unknown port may indicate hidden attack vector

---

## 🧠 Key Takeaways

* Full port scanning revealed services not visible in browser testing
* Service detection helps identify technologies and versions
* Attack surface includes web, database, and system-level services

---
---

# 🔍 Service Vulnerability Analysis (Day 10)

## 🔹 Port 80 — Apache HTTP Server

### Potential Vulnerabilities

* Misconfiguration (default settings)
* Directory listing exposure
* Outdated modules or known CVEs

### Attack Ideas

* Perform directory brute force (ffuf)
* Check for sensitive endpoints (/server-status, /admin)
* Identify misconfigured files

---

## 🔹 Port 3000 — Node.js (Juice Shop)

### Observed Vulnerabilities

* DOM-based XSS
* Authentication bypass (login injection)
* File upload functionality

### Attack Ideas

* Further API fuzzing
* Chain vulnerabilities (XSS + auth bypass)
* Parameter manipulation and logic flaws

---

## 🔹 Port 3306 — MariaDB (Critical Exposure)

### Potential Vulnerabilities

* Weak or default credentials
* Unauthorized remote access
* Data exposure

### Attack Ideas

* Attempt login with common credentials
* Test database access remotely
* Enumerate databases if access is gained

---

## 🔹 Port 22 — SSH

### Potential Vulnerabilities

* Weak credentials
* Brute-force susceptibility

### Attack Ideas

* Attempt SSH login with known credentials
* Test authentication mechanisms

---

## 🔹 Port 36791 — Unknown Service

### Potential Vulnerabilities

* Hidden or undocumented service
* Misconfigured internal service

### Attack Ideas

* Perform further service detection
* Attempt manual connection
* Fuzz the service for hidden functionality

---

## 🎯 Attack Prioritization

1. Port 3000 — Primary target (confirmed vulnerabilities)
2. Port 3306 — High-risk database exposure
3. Port 36791 — Unknown service (needs investigation)
4. Port 80 — Secondary web surface
5. Port 22 — Low priority

---

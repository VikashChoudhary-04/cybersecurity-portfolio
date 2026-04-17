# 🧪 Day 19 — Validation

## 📌 Objective

- Validate all identified vulnerabilities and eliminate false positives to ensure accuracy.

---

## 🔥 Confirmed Vulnerabilities

### 1. SQL Injection (Authentication Bypass)

#### Payload

```
admin' OR 1=1--
```

#### Result

* Successfully bypassed authentication
* Logged in as admin

#### Classification

* Critical severity

---

### 2. IDOR (Horizontal Access)

#### Endpoints

```
/rest/basket/2
/rest/basket/3
```

#### Result

* Access to other users' data
* No ownership validation

#### Classification

* High severity

---

### 3. DOM-based XSS

#### Payload

```html
<img src=x onerror=alert(1)>
```

#### Result

* JavaScript execution confirmed
* Only non-sensitive cookies accessible

#### Classification

* Medium severity

---

### 🟢 Non-Vulnerable Areas

#### File Upload

* No execution possible
* Strong validation present

---

## ❌ False Positives Eliminated

* Search endpoint SQL Injection → Not vulnerable
* Path traversal → Not vulnerable
* SSTI → Not vulnerable
* Parameter manipulation → No impact
* File upload RCE → Not possible

---

## 🧠 Key Takeaways

* Validation ensures accuracy and credibility
* Not all inputs lead to vulnerabilities
* Removing false positives is critical in real pentesting
* Confirmed vulnerabilities should be reproducible

---

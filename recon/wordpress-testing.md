# 🌐 WordPress Testing — Plugin & AJAX Analysis

---

## 📌 Objective

- Analyze WordPress plugin endpoints, test `admin-ajax.php`, and perform parameter manipulation to identify potential vulnerabilities.

---

## 🔍 1. Target Overview

* Platform: WordPress
* Key components:

  * Plugins (e.g., WPBakery, Slider Revolution)
  * AJAX endpoint (`admin-ajax.php`)

---

## 🧪 2. admin-ajax.php Testing

### Endpoint

```
/wp-admin/admin-ajax.php
```

---

### Observations

* Most requests returned:

  * `0`
  * Blank response

---

### 🧠 Analysis

* Indicates invalid or unauthorized actions
* Endpoint requires correct `action` parameter
* Some actions may require authentication

---

## 🧪 3. Action Enumeration

### Tested Parameters

* action=login
* action=upload
* action=reset
* action=register

---

### Result

* No valid action discovered
* Responses remained consistent (`0` or empty)

---

## 🧪 4. Parameter Manipulation

### Tests Performed

* Modified parameters (e.g., user_id, file paths)
* Attempted traversal-like input
* Tested different input formats

---

### Result

* No abnormal behavior observed
* No data leakage detected

---

## 🧪 5. Request Method Testing

### GET Requests

* Limited responses
* Mostly returned `0`

---

### POST Requests

* Tested with various parameters
* No significant difference observed

---

## 🧪 6. Plugin Endpoint Analysis

### Observations

* Plugin directories identified
* No direct vulnerable endpoints discovered

---

### Potential Attack Areas

* Plugin-specific AJAX actions
* File upload functionality
* Misconfigured plugin endpoints

---

## 🧠 Analysis

* WordPress AJAX requires valid action names
* Plugins significantly expand attack surface
* Lack of response does not indicate absence of vulnerabilities

---

## ⚠️ Security Assessment

* No confirmed vulnerabilities identified
* Attack surface exists but requires deeper enumeration

---

## 🧠 Key Takeaways

* WordPress testing requires action enumeration
* Plugin endpoints are critical attack vectors
* AJAX endpoints often require precise parameters
* Real-world testing often involves inconclusive results

---

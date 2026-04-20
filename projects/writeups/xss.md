# 🟡 XSS Vulnerability

## Description

- The application is vulnerable to DOM-based XSS via the search functionality.

---

## Payload

```html
<img src=x onerror=alert(1)>
```

---

## Impact

* Arbitrary JavaScript execution
* Limited due to secure cookie handling

---

## Fix

* Sanitize input
* Encode output
* Use CSP

---

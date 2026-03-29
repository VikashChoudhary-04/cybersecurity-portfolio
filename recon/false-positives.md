# ❌ False Positives Log

This file tracks findings that initially appeared vulnerable but were not exploitable.

---

## 📅 Day 0

(No false positives yet — observation phase)

---

## 📅 Day 1

### ❌ Server-side Reflected XSS

* Tested payloads via Burp Suite (`<img>`, `<svg>`, etc.)
* Server returned `400 Bad Request` for multiple payloads
* `<script>` payload accepted but not executed

👉 Conclusion:

* No server-side reflected XSS
* Vulnerability exists as DOM-based XSS instead

---

# 💻 Command Injection Testing — OWASP Juice Shop

---

## 📌 Objective

- Test application inputs for command injection vulnerabilities, including blind and time-based techniques.

---

## 🧪 1. Input Points Tested

* Search parameter (`q=`)
* Feedback form
* API inputs

---

## 🪜 2. Payloads Tested

### Basic Injection

* `test; whoami`
* `test && whoami`
* `test | whoami`

---

### Blind Injection

* `test; sleep 5`

---

### Error-Based

* `test; invalidcommand`

---

## 🔍 Observation

* No command output observed
* No abnormal response behavior
* No response delay detected
* No error messages indicating command execution

---

## 💣 Conclusion

- No command injection vulnerability identified during testing.

---

## ⚠️ Security Impact

* **Severity:** None (based on current testing)

---

## 🛠️ Recommendations

* Continue validating and sanitizing all user inputs
* Avoid passing user input to system-level commands
* Use safe APIs instead of shell execution

---

## 🧠 Key Takeaways

* Not all applications are vulnerable to command injection
* Blind testing techniques are essential when no output is visible
* Proper input handling prevents critical system-level vulnerabilities

---

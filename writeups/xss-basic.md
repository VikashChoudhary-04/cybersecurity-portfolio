# 🔓 Reflected DOM-Based XSS — Search Functionality

---

## 📌 Objective

- Identify and exploit Cross-Site Scripting (XSS) vulnerability in the search functionality.

---

## 🧠 Vulnerability Summary

- The application is vulnerable to **DOM-based Cross-Site Scripting (XSS)** in the search functionality.

- User-controlled input from the `q` parameter is processed by client-side JavaScript and injected into the DOM without proper sanitization.

---

## 🎯 Affected Endpoint

```
GET /rest/products/search?q=
```

---

## 🪜 Steps to Reproduce

1. Navigate to the search functionality in the application
2. Enter the following payload in the search bar:

```
<img src=x onerror=alert(1)>
```

3. Observe that a JavaScript alert is triggered in the browser

---

## 🔍 Technical Analysis

* The payload is not executed via server response
* Instead, the frontend JavaScript processes the input and injects it into the DOM
* This indicates a **DOM-based XSS vulnerability**

---

### 🧪 Burp Suite Testing

- Using Burp Suite:

  * Intercepted request:

  ```
  GET /rest/products/search?q=test
  ```

  * Modified payload:

  ```
  q=<img src=x onerror=alert(1)>
  ```

  * Result:

    * Server returned **400 Bad Request** for certain payloads
    * Indicates presence of server-side filtering

---

### ⚠️ Key Finding

* Payload executes in browser but not via direct server response
* Confirms:

```
DOM-based XSS (client-side execution)
```

---

## 💥 Impact

- An attacker can:

  * Execute arbitrary JavaScript in victim’s browser
  * Steal session tokens (JWT)
  * Perform actions on behalf of the user
  * Deface the application UI

---

## 🧠 Business Impact

- This vulnerability can lead to:

  * Account compromise
  * Unauthorized actions using victim’s session
  * Exposure of sensitive user data
  * Loss of user trust and reputational damage

---

## 🛠️ Recommended Fix

* Sanitize and encode user input before inserting into DOM
* Avoid using unsafe DOM manipulation methods (e.g., `innerHTML`)
* Implement Content Security Policy (CSP)
* Validate input on both client and server side

---

## 🧠 Key Takeaways

* Not all XSS originates from server responses
* DOM-based XSS requires analyzing frontend behavior
* Burp Suite alone is not sufficient — browser inspection is critical

---

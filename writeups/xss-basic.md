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

---

## 🧪 Context Analysis (Day 2)

### 🔍 HTML Context

Test Payload:

```html
<b>test</b>
```

Result:

* Input is interpreted as HTML
* Indicates insertion into DOM as HTML

---

### 🔍 Attribute Context

Test Payload:

```html
" autofocus onfocus=alert(1) x="
```

Result:

* Attribute injection attempt blocked or not reflected
* No successful execution observed

---

### 🔍 JavaScript Context

Test Payload:

```javascript
";alert(1);//
```

Result:

* No execution observed
* Input not injected into JavaScript context

---

### ✅ Confirmed Context

The vulnerability exists in **HTML DOM context**, where user input is inserted into the page without sanitization.

---

### 🔧 Payload Refinement

Working Payload:

```html
<img src=x onerror=alert(1)>
```

Additional Variations Tested (Worked):

```html
<img src=1 onerror=alert(1)>
<img src=x onerror=confirm(1)>
<img src=x onerror=alert(document.domain)>
```

---

### 🧠 Key Insight

* `<script>` tags are filtered or not executed
* Event-based payloads (`onerror`) successfully bypass restrictions
* Indicates partial filtering but improper output encoding

---
---

## 🔬 Advanced Analysis (Day 3)

### 🔍 Source

User-controlled input is taken from the `q` parameter in the search functionality:

```
/rest/products/search?q=
```

---

### 🎯 Sink

The application inserts user input into the DOM using unsafe methods (e.g., `innerHTML`), which allows execution of injected HTML content.

---

### 🔄 DOM-Based Execution

* The payload is not executed via server response
* Instead, it is processed and rendered by client-side JavaScript
* This confirms a DOM-based XSS vulnerability

---

### 🛡️ Filter Bypass Analysis

* `<script>` tags are blocked or not executed
* Event-based payloads such as `<img onerror>` successfully bypass filters

👉 This indicates:

* Partial input filtering
* Lack of proper output encoding

---

### 💣 Exploitation Insight

The vulnerability allows execution of arbitrary JavaScript via DOM manipulation, making it possible to:

* Steal JWT tokens
* Perform actions on behalf of the user
* Manipulate application behavior

---

### 🧠 Key Learning

* DOM XSS requires analyzing frontend behavior, not just server responses
* Filters can be bypassed using alternative payloads
* Understanding source and sink is critical for exploitation

---

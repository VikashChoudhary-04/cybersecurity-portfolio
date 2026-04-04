# 📤 File Upload Vulnerability — OWASP Juice Shop

---

## 📌 Objective

- Test file upload functionality for extension bypass, MIME validation, and potential remote code execution (RCE).

---

## 🧪 1. File Upload Functionality

### 🎯 Endpoint

POST /rest/memories

---

### 🪜 Steps to Reproduce

1. Navigated to file upload feature
2. Uploaded a valid image file (`.jpg`)
3. Intercepted request using Burp Suite

---

### 🔍 Observed Request

```http id="reqsample"
POST /rest/memories HTTP/1.1
Content-Type: multipart/form-data

Content-Disposition: form-data; name="image"; filename="my"
Content-Type: image/jpeg
```

---

### 🔍 Observation

* Upload successful for `.jpg` files
* File stored at:

```id="path"
/assets/public/images/uploads/<filename>.jpg
```

* Uploaded files are publicly accessible

---

## 🧪 2. Extension Bypass Testing

### 🪜 Payloads Tested

* `shell.php.jpg`
* `file.jpg.php`
* `test.php`

---

### 🔍 Observation

* Server rejected all malicious extensions
* No bypass achieved

---

### 💣 Conclusion

- The application enforces **strict extension validation**, preventing direct upload of executable files.

---

## 🧪 3. MIME Type Manipulation

### 🪜 Steps Performed

1. Intercepted upload request
2. Observed:

```http id="mimeobs"
Content-Type: image/jpeg
```

3. Attempted to manipulate MIME type

---

### 🔍 Observation

* Server behavior suggests validation of file type
* No successful bypass observed

---

## 🧪 4. Execution Attempt

### 🪜 Steps Performed

1. Accessed uploaded file via browser:

```id="execpath"
/assets/public/images/uploads/<filename>.jpg
```

---

### 🔍 Observation

* File served as static content
* No code execution observed

---

### 💣 Conclusion

* Application does not execute uploaded files
* No Remote Code Execution (RCE) possible in current setup

---

## ⚠️ Security Impact

* **Severity:** Medium

- Although RCE is not possible, the application allows:

  * Public access to uploaded files
  * Storage of user-controlled content

---

## 💥 Potential Risks

* Malicious file hosting
* Phishing content distribution
* Stored XSS (if combined with other vulnerabilities)

---

## 🛠️ Recommended Fixes

* Restrict file access using authentication
* Validate file content (not just extension/MIME)
* Rename uploaded files securely
* Store files outside public directory
* Implement file scanning (antivirus)

---

## 🧠 Key Takeaways

* File upload vulnerabilities are not always RCE
* Even restricted uploads can be abused
* Security depends on storage, validation, and access control

---

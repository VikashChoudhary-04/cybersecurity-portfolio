# 🔍 Directory and Endpoint Discovery — ffuf

---

## 📌 Objective

- Discover hidden directories and endpoints using ffuf to expand the application attack surface.

---

## 🧪 1. Directory Fuzzing

### Command Used

```bash
ffuf -u http://127.0.0.1:3000/FUZZ -w /usr/share/wordlists/dirb/common.txt -fc 404 -t 10
```

---

### 🔍 Initial Results

- The scan returned multiple paths with HTTP 200 responses, including:

  * /.bashrc
  * /.htpasswd
  * /.git/HEAD
  * /.profile
  * /.mysql_history

---

### ⚠️ Analysis (False Positives)

- All responses had identical characteristics:

  * Status Code: 200
  * Response Size: 75055
  * Same number of words and lines

- This indicates that the application returns a **uniform response for non-existent paths**, likely due to SPA (Single Page Application) behavior.

---

### 💣 Conclusion

* No sensitive files were actually exposed
* The results represent **false positives caused by identical server responses**
* Status code alone is not reliable for endpoint discovery

---

## 🧪 2. Improved Filtering

### Command Used

```bash
ffuf -u http://127.0.0.1:3000/FUZZ -w /usr/share/wordlists/dirb/common.txt -fc 404 -fs 75055 -t 10
```

---

### 🔍 Result

* Filtering by response size (`-fs 75055`) removed duplicate responses
* Improved accuracy of fuzzing results
* Only meaningful endpoints remain visible

---

## 🧪 3. API Fuzzing

### Command Used

```bash
ffuf -u http://127.0.0.1:3000/rest/FUZZ -w /usr/share/wordlists/dirb/common.txt -fc 404 -t 10
```

---

### 🔍 Findings

- The scan identified API-related endpoints, including:

  * /rest/products
  * /rest/user
  * /rest/basket

- These endpoints were already observed during manual testing, confirming API structure.

---

## 🧠 Analysis

* The application uses SPA behavior, returning identical responses for invalid routes
* Response size filtering is essential to eliminate false positives
* API fuzzing confirms and expands understanding of backend endpoints

---

## ⚠️ Security Impact

* Hidden endpoints may still exist but require proper filtering to identify
* Misinterpretation of fuzzing results can lead to incorrect conclusions
* Accurate analysis is critical in the discovery phase

---

## 🧠 Key Takeaways

* Status codes alone are insufficient for fuzzing analysis
* Response size/content filtering is essential for accuracy
* Understanding application behavior prevents false positives
* Discovery phase requires both tooling and analytical thinking

---

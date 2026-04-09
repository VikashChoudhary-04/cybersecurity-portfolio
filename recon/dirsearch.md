# 🔍 Directory Discovery — dirsearch

---

## 📌 Objective

- Perform directory and endpoint discovery using dirsearch and compare results with ffuf.

---

## 🧪 1. Directory Scan

### Command Used

```bash id="9prr9s"
dirsearch -u http://127.0.0.1:3000 -e * -t 10
```

---

### 🔍 Results

* /.well-known/security.txt — Status 200

---

### 🧠 Analysis

* The endpoint `/.well-known/security.txt` is a valid discovery
* This file is commonly used to provide security contact information

---

### ⚠️ Tool Behavior

- During scanning, dirsearch encountered multiple errors:

```id="mhh3np"
Cannot connect to: 127.0.0.1:3000  
Too many request errors
```

---

### 🧠 Interpretation

* The target application became unstable under fuzzing load
* Connection failures caused the scan to stop prematurely
* This behavior was also observed during ffuf scanning

---

## 🧪 2. API Scan

### Command Used

```bash id="njaz0p"
dirsearch -u http://127.0.0.1:3000/rest/ -e * -t 10
```

---

### 🔍 Results

* No additional meaningful endpoints discovered
* Scan affected by connection instability

---

## 🧠 Comparison with ffuf

### 🔍 Observations

* Both tools experienced instability during scanning
* ffuf produced many false positives due to identical responses
* dirsearch produced fewer false positives but was less stable

---

## ⚖️ Tool Comparison

### ffuf

* More flexible and controllable
* Requires response filtering (status/size)
* Better suited for targeted fuzzing

---

### dirsearch

* Easier to use for quick scans
* Less flexible filtering
* More prone to failure under unstable conditions

---

## 💣 Conclusion

* One valid endpoint discovered: `/.well-known/security.txt`
* No high-impact hidden endpoints identified
* Target instability affected fuzzing accuracy

---

## 🧠 Key Takeaways

* Tool failures can indicate target instability, not absence of endpoints
* Multiple tools help validate findings
* Fuzzing results must always be analyzed critically
* Stability and filtering are crucial for accurate discovery

---

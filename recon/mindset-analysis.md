# 🧠 Mindset Analysis — Day 0

---

## 🎯 Target Overview

* **Application Name:** OWASP Juice Shop
* **Type:** Modern Single Page Application (SPA) using API-based backend communication
* **Purpose:** E-commerce platform for browsing and purchasing fruit-based products, allowing users to search items, manage a basket, and submit reviews
* **Authentication Required:** Partially required (guest users can browse/search, but actions like adding items to basket and posting reviews require authentication)

---

## 🔑 User Roles

### 👤 Guest (Unauthenticated User)

* Can browse products
* Can search for items
* Can view product details

❌ Cannot:

* Add items to basket
* Post product reviews
* Access user-specific data

---

### 👤 Authenticated User

* Can log in and maintain a session
* Can add items to basket
* Can submit product reviews
* Can interact with user-specific features

👉 **Security Note:**
Application relies on proper session/token validation → potential attack surface for authentication and authorization flaws

---

### 👑 Admin (Privileged User)

* Not visible in UI by default
* Likely has access to administrative functionality and sensitive endpoints

👉 **Security Note:**
Hidden admin functionality may expose high-impact attack vectors if access control is weak

---

## 🚪 Entry Points (Attack Surface)

### 🌐 Web Inputs

* Login form (email, password)
* Registration form
* Search functionality (`q` parameter in URL)
* Product review input fields
* Feedback forms
* Basket interactions (add/remove items, quantity changes)
* URL parameters (product IDs, basket IDs)

---

### ⚙️ API / Backend Inputs

* `/rest/products/search?q=` → user-controlled search input
* `/rest/basket/{id}` → basket access using client-controlled ID
* `/api/Quantitys/` → product quantity data
* Authentication endpoints (`/rest/user/login`)
* File upload endpoint (`/rest/memories`)

👉 **Security Note:**
Application heavily relies on API requests → improper server-side validation may lead to vulnerabilities

---

### 🍪 Other Inputs

* Cookies (session/token storage)
* Authorization header (JWT token)
* HTTP headers (User-Agent, Referer)
* Local storage / session storage

👉 **Security Note:**
Client-controlled data sources can be manipulated → potential for authentication bypass or privilege escalation

---

## 🔐 Trust Boundaries

* User-controlled resource identifiers are trusted

  * Example: `/rest/basket/{id}`
  * 👉 Risk: Unauthorized access to other users’ data (IDOR)

* Search input is directly processed by backend

  * 👉 Risk: Reflected or stored XSS, injection attacks

* API endpoints rely on client-provided parameters

  * 👉 Risk: Manipulation of application logic

* Authentication token (JWT) is trusted for identity and role

  * 👉 Risk: Token tampering or privilege escalation

* File upload functionality trusts client-provided file type

  * 👉 Risk: File upload bypass → potential remote code execution

* Client-side values (basket, quantity) are trusted

  * 👉 Risk: Business logic manipulation

---

## 🔄 Data Flow

### 🔐 Authentication Flow

1. User submits credentials via POST request to `/rest/user/login`
2. Backend validates credentials
3. Server generates JWT token containing user information
4. Token is returned to client and stored
5. Token is used in subsequent requests for authentication

---

### 🧺 Basket Access Flow

1. Client sends GET request to `/rest/basket/{id}`
2. Request includes Authorization token
3. Backend retrieves basket based on provided ID
4. Database returns associated basket data
5. Response is returned to client

👉 **Observation:**
Basket ID is client-controlled → potential IDOR

---

### 📦 File Upload Flow

1. User uploads file via POST request to `/rest/memories`
2. File is sent as multipart form-data
3. Backend processes and stores file
4. File path is saved in database
5. Response returns stored file location

👉 **Observation:**
File type validation appears weak → potential upload bypass

---

## 💣 Attack Hypotheses

1. Search parameter may reflect user input → possible reflected XSS
2. Product reviews may store unsanitized input → possible stored XSS
3. Basket ID manipulation may allow access to other users’ baskets → IDOR
4. JWT token may be tampered to escalate privileges → authentication bypass
5. File upload functionality may allow malicious file execution → possible RCE
6. API endpoints may expose sensitive data without proper authorization checks
7. Client-controlled parameters may allow business logic manipulation

---

## 🧠 Thinking Log

* Selected target due to realistic application behavior and API-driven architecture
* Most vulnerable areas appear to be:

  * API endpoints
  * File upload functionality
  * Token-based authentication
* First testing focus will be:

  * XSS in search and review inputs
* Ignoring admin panel initially as it is not directly exposed

---

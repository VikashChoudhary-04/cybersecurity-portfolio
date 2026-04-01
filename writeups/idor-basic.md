# IDOR Vulnerability (Basic)

## Target
- OWASP Juice Shop

## Objective
- Test for unauthorized access via ID manipulation

---

## Endpoint Identified
```
GET /api/user?id=101
```
---

## Testing Steps

1. Captured request using Burp Suite
2. Identified parameter: id=101
3. Modified ID to:
   - 102
   - 103
   - 1

---

## Proof of Vulnerability

### Original Request
GET /api/user?id=101

### Modified Request
GET /api/user?id=102

### Result
- Received data of another user
- No authorization check present

---

## Impact

- Unauthorized access to user data
- Potential data leakage
- Possible account takeover (if chained)

---

## Severity

High

---

## Remediation

- Implement proper authorization checks
- Validate ownership of resources
- Avoid exposing direct object references

---

## Thinking Log

- Why I tested this:
  ID parameters often lack authorization checks

- What I ignored:
  Static pages without identifiers

- What I would test next:
  POST endpoints, API calls, and multi-step flows

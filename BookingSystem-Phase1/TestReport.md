# 1️⃣ Introduction

**Testers**  
- Name:  Divya Shrestha, Pawan Man Malego

**Purpose:**  
- Identify vulnerabilities in registration and authentication flows.

**Scope:**  
- Tested components: Registration page (client & server behavior)   
- Exclusions:  Admin Functions, other endpoints
- Test approach: Black-box 

**Test environment & dates:**  
- Start:  2025-11-26
- End:  2025-11-26
- Test environment details (OS, runtime, DB, browsers): Docker local environment, Browser: Chrome, Server: localhost:8000, Tool: OWASP ZAP

**Assumptions & constraints:**  
- Testing performed only on the local Docker instance.

---

# 2️⃣ Executive Summary

**Short summary (1-2 sentences):**  
Local scan found several medium/low issues (missing CSRF tokens, missing security headers). No confirmed SQLi.

**Overall risk level:** Medium

**Top 5 immediate actions:**  
1.  Implement Anti-CSRF tokens for forms.
2.  Add Content-Security-Policy header.
3.  Add X-Frame-Options / CSP frame-ancestors.
4.  Hide server error details; implement custom error pages.
5.  Add X-Content-Type-Options: nosniff

---

# 3️⃣ Severity scale & definitions

|  **Severity Level**  | **Description**                                                                                                              | **Recommended Action**           |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|      🔴 **High**     | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | *Immediate fix required*         |
|     🟠 **Medium**    | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF).                              | *Fix ASAP*                       |
|      🟡 **Low**      | A minor issue or configuration weakness (e.g., server version disclosure).                                                   | *Fix soon*                       |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers).                                            | *Monitor and fix in maintenance* |


---

# 4️⃣ Findings


| ID | Severity | Finding | Description | Evidence / Proof |
|------|-----------|----------|--------------|------------------|
| F-01 | 🟠 Medium | Absence of Anti-CSRF Tokens | No CSRF token on registration form | ZAP evidence: `<form action="/register">` |
| F-02 | 🟠 Medium | CSP Header Missing | CSP not present on / and /register  | ZAP alert |
| F-03 | 🟠 Medium | Missing Anti-clickjacking Header | No X-Frame-Options or frame-ancestors | ZAP alert |
| F-04 | 🟡 Low | Application Error Disclosure | 500 error observed on POST /register | ZAP evidence |
| F-05 | 🟡 Low | X-Content-Type-Options Missing |  `X-Content-Type-Options` not set | ZAP alert |

---


---

# 5️⃣ OWASP ZAP Test Report (Attachment)

**Purpose:**  
- This section contains the results of the automated security scan performed using OWASP ZAP.  
The full scan results are included as a separate Markdown file.

---


### 📎 ZAP Report (Markdown)
 **[Click here to view the full ZAP report part1](./ZAP-Report-round1.md)**
 **[Click here to view the full ZAP report part2](./ZAP-Report-round2.md)**

 ### Notes
- The ZAP scan was run against the local testing environment.
- No manual edits were made to the ZAP output, as required.
  
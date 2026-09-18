# Vortex Tech — Week 3: Basic Security Audit

## Overview

As part of Week 3 of the Vortex Tech Cybersecurity Internship 2026, I performed a basic security audit of **OWASP Juice Shop**, a deliberately vulnerable web application designed for security training and testing.

The assessment focused on identifying common web application security issues using manual testing, browser developer tools, and **OWASP ZAP**.

> **Scope:** This assessment was performed only against a local OWASP Juice Shop instance running at `http://localhost:3000`.

---

## Objectives

The main objectives of this audit were to:

- Explore the application manually for common security weaknesses.
- Use OWASP ZAP to assist with vulnerability discovery.
- Inspect HTTP requests and responses using browser/network tools.
- Identify vulnerabilities across multiple security categories.
- Document the discovery process, potential impact, and remediation.
- Relate the findings to concepts covered during the Week 1 OWASP Top 10 research.

---

## Tools & Environment

| Tool | Purpose |
|---|---|
| OWASP Juice Shop | Deliberately vulnerable practice application |
| OWASP ZAP | Automated and assisted web security testing |
| Firefox | Browser-based testing |
| Browser Developer Tools | HTTP request/response inspection |
| Kali Linux | Security testing environment |

**Target:**

```text
http://localhost:3000
```
## Assessment Methodology

The audit followed a simple structured process:

1. Started the local OWASP Juice Shop instance.
2. Explored the application manually.
3. Tested application inputs for unexpected behavior.
4. Used OWASP ZAP to crawl and scan the application.
5. Reviewed HTTP responses and security headers.
6. Investigated interesting responses manually.
7. Reproduced selected findings.
8. Captured screenshots as evidence.
9. Documented the potential impact and recommended remediation.

---

## Findings Summary

| ID | Finding | Category | Severity |
| :--- | :--- | :--- | :--- |
| **F-01** | SQL Injection | Injection | High |
| **F-02** | Missing Content Security Policy Header | Security Misconfiguration | Medium |
| **F-03** | DOM-Based Cross-Site Scripting | Cross-Site Scripting | High* |

*\*Severity shown here represents the security significance of the demonstrated vulnerability in the practice environment. OWASP Juice Shop itself is intentionally vulnerable, so severity should not be interpreted as a production risk rating.*

---

## F-01 — SQL Injection

### Description
During testing of the product search functionality, specially crafted input caused the application to return a database error.  
The application exposed an SQLite error containing the SQL statement being processed.

### Evidence

**Affected Endpoint:**  
`http://localhost:3000/rest/products/search`
The tested request included a specially crafted search parameter.

### Testing Process

1. Navigated to the product search functionality.
2. Tested the search parameter with unexpected SQL-related characters.
3. The application returned:

```http
HTTP/1.1 500 Internal Server Error
```
The response exposed an SQLite database error.

The error revealed part of the SQL query being executed.
The response contained:

```text
SQLITE_ERROR: near "(": syntax error
```
and exposed the query structure:

```sql
SELECT * FROM Products WHERE ((name LIKE ...)
```

### Potential Impact

In a real application, SQL injection can potentially allow an attacker to manipulate database queries.  
Depending on the application's database permissions and query construction, successful SQL injection may result in:

* **Unauthorized access** to database information.
* **Modification or deletion** of database records.
* **Authentication bypass** in vulnerable login queries.
* **Exposure** of sensitive application data.

In this practice environment, the observed database error also demonstrates excessive error information disclosure.

---

### Recommended Remediation

Use parameterized queries or prepared statements instead of constructing SQL statements directly from user-controlled input.

Additionally:

* **Validate and constrain** search input.
* **Avoid returning** raw database errors to users.
* **Log detailed** database errors server-side only.
* **Return generic** error messages to clients.

---

## F-02 — Missing Content Security Policy Header

### Description
During the ZAP-assisted security audit, the application was identified as missing a Content Security Policy (CSP) response header.  
A CSP helps control which sources of scripts, styles, images, frames, and other resources a browser is allowed to load.

---

### Evidence

#### Testing Process

1. Intercepted/inspected HTTP responses from the Juice Shop application.
2. Reviewed the security-related response headers.
3. The response contained headers such as:

```http
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
```
However, a `Content-Security-Policy` header was not present.

OWASP ZAP consequently reported the missing CSP header.

---

### Potential Impact

A missing CSP does not automatically mean that XSS exists.  
However, when an application contains an XSS vulnerability, the absence of an effective CSP can remove an additional browser-level mitigation layer.

---

### Recommended Remediation

Implement a restrictive Content Security Policy appropriate for the application's resources.

For example, an application should define trusted sources for scripts and other resources rather than allowing unrestricted loading. The policy should be tested carefully before deployment to avoid breaking legitimate application functionality.

---

## F-03 — DOM-Based Cross-Site Scripting

### Description
During manual testing of the application, a DOM-based Cross-Site Scripting vulnerability was successfully demonstrated.  
The test resulted in JavaScript executing in the browser, confirming that attacker-controlled input could reach a client-side execution context.

---

### Evidence

#### Testing Process

1. Explored client-side functionality in OWASP Juice Shop.
2. Tested application-controlled input using a JavaScript payload.
3. The input was processed by the application's client-side code.
4. A JavaScript alert was successfully triggered in the browser.
5. A screenshot was captured as evidence of the successful execution.

---

### Potential Impact

In a real-world application, DOM-based XSS could allow an attacker to execute JavaScript in another user's browser when the vulnerable functionality is triggered.  
Depending on the application's architecture and browser protections, potential consequences can include:

* **Manipulation** of page content.
* **Performing actions** using the victim's browser session.
* **Phishing** or UI manipulation.
* **Access to data** available to client-side JavaScript.
* **Redirection** to malicious content.

---

### Recommended Remediation

Client-side code should treat all user-controlled data as untrusted.

Recommended controls include:

* **Avoid inserting untrusted data** using dangerous DOM APIs such as `innerHTML`.
* **Prefer safe DOM APIs** such as `textContent` where appropriate.
* **Validate and encode data** according to its output context.
* **Avoid dynamically constructing executable JavaScript** from user-controlled values.
* **Use an effective CSP** as an additional defense layer.

---

## Additional ZAP Observations

OWASP ZAP also identified other observations during the automated scan, including:

* **Cross-domain configuration concerns**
* **Missing anti-clickjacking protections** on certain responses
* **Session ID appearing in URL rewriting**
* **Private IP address disclosure**
* **Informational and low-risk observations**

These were reviewed during the assessment but were not selected as the primary three findings documented in this report.

---

## Security Lessons Learned

This audit demonstrated several important web application security concepts:

1. **Input Handling Matters**  
   Unexpected input can expose vulnerabilities or cause backend errors. Applications should never trust data supplied by users.

2. **Error Messages Can Leak Information**  
   Database errors should not be returned directly to users because they can reveal implementation details useful to an attacker.

3. **Security Headers Provide Defense in Depth**  
   Headers such as CSP can provide additional protection against certain classes of browser-based attacks.

4. **Client-Side Code Is Part of the Attack Surface**  
   DOM-based vulnerabilities can occur even when the server-side application does not directly reflect malicious input.

5. **Automated Scanners Need Manual Verification**  
   Tools such as OWASP ZAP are useful for identifying potential issues, but findings should be manually reviewed and reproduced before being documented as confirmed vulnerabilities.

---

## Evidence

The following screenshots were captured during the assessment:

| Evidence | Description |
| :--- | :--- |
| `01-juice-shop-running.png` | Local OWASP Juice Shop environment |
| `02-sql-injection.png` | SQL injection / database error evidence |
| `03-missing-csp-header.png` | Missing CSP response header |
| `04-dom-xss.png` | Successful DOM XSS demonstration |

---

## Conclusion

The Week 3 assessment provided practical experience performing a structured security audit against a deliberately vulnerable web application.

The assessment combined:

* Manual application testing
* HTTP request/response analysis
* Browser Developer Tools
* OWASP ZAP
* Vulnerability reproduction
* Evidence collection
* Risk and remediation documentation

The exercise reinforced the importance of secure input handling, safe client-side coding, appropriate security headers, and careful manual verification of automated scanner results.

---

## Scope & Ethics

This assessment was performed exclusively against a locally hosted OWASP Juice Shop training environment. No unauthorized testing was performed against real production systems.

The techniques documented in this report are intended for authorized security testing, education, and defensive security research.

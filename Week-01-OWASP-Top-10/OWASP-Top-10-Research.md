# OWASP Top 10:2025 — Vulnerability Research

## 1. A01:2025 — Broken Access Control

**What it is:**
Broken Access Control occurs when an application fails to properly restrict what
authenticated users are allowed to do. Instead of enforcing strict rules about
which resources or actions each user can access, the system trusts input it
shouldn't — letting users view, modify, or delete data that isn't theirs simply
by changing an ID, URL, or request parameter.

**How an attacker could exploit it:**

For example, an attacker might modify an object identifier in a URL or API
request, such as changing `order_id=1042` to `order_id=1043`, and attempt to
access another user's order. If the application does not verify that the
authenticated user is authorized to access the requested resource, the
attacker may be able to view or modify data belonging to another user.

Another form of broken access control occurs when an application hides
administrator functionality from normal users but fails to enforce the
restriction on the server side. An attacker may attempt to access the
restricted endpoint directly.

**Real-World Example — Authorized Bug Bounty Finding**

During authorized bug bounty testing of a live e-commerce platform through
Intigriti, I identified and reported a broken access control vulnerability
affecting the checkout flow. The issue allowed unauthorized manipulation of
order-related information by bypassing the application's intended
authorization controls.

The finding was submitted through the platform's responsible disclosure
process and was subsequently triaged. This experience helped me understand
how broken access control can affect real production applications and
highlighted the importance of enforcing authorization checks on the
server side.

**Prevention:**

- Enforce authorization checks on the server side for every request.
- Verify that the authenticated user is authorized to access the requested
  resource before allowing read, modify, or delete operations.
- Do not rely solely on hidden UI elements to enforce permissions.
- Apply the principle of least privilege.
- Deny access by default unless the required permission is explicitly granted.
- Test both horizontal and vertical access controls during security testing.

 **Potential Impact:**

Broken access control can lead to unauthorized access to sensitive
information, modification of other users' data, privilege escalation,
financial manipulation, or unauthorized administrative actions, depending
on the affected functionality.

---

## 2. A02:2025 — Security Misconfiguration

**What it is:**

Security Misconfiguration happens when systems are deployed with insecure
default settings, unnecessary features enabled, overly permissive
configurations, or missing security hardening — not necessarily because of a
coding flaw, but because of how the application or infrastructure was set up.

**How an attacker could exploit it:**

An attacker could find an exposed administrative interface with default
credentials, discover verbose error messages that reveal stack traces or
internal file paths, or find directory listing enabled on a web server,
potentially exposing files or application components that should remain
private.

**Real-World Example:**

A well-known example of security misconfiguration is the 2019 Capital One
cloud security incident. Capital One stated that an attacker exploited a
configuration vulnerability in its infrastructure, which resulted in
unauthorized access to customer and applicant information.

Court records later described a misconfigured firewall and permissions that
were broader than intended. The incident demonstrates how an insecure
infrastructure configuration can contribute to unauthorized access and data
exposure, even when the underlying application is not necessarily the direct
cause of the breach.

**Prevention:**

- Establish a repeatable security-hardening process for every environment.
- Remove unnecessary services, features, accounts, and sample applications.
- Change default credentials and disable unused accounts.
- Disable directory listing and unnecessary debugging functionality.
- Configure applications to avoid exposing detailed stack traces or
  sensitive error information.
- Review cloud storage and service permissions regularly.
- Use secure security headers and secure configuration defaults.
- Automate configuration checks where possible.
- Regularly review configurations after changes or deployments.
- Apply the principle of least privilege to cloud and infrastructure
  permissions.

**Potential Impact:**

Security misconfiguration can result in sensitive information disclosure,
unauthorized access, privilege abuse, exposure of internal application
details, or provide attackers with additional information that can be used
for further attacks. The severity depends on what component has been
misconfigured and what resources it can access.

---

## 3. A04:2025 — Cryptographic Failures

**What it is:**

Cryptographic Failures occur when an application fails to properly protect
sensitive data through the appropriate use of cryptography. This can include
using weak or outdated cryptographic algorithms, transmitting sensitive data
without adequate encryption, improperly storing passwords, or using
cryptographic keys incorrectly.

**How an attacker could exploit it:**

An attacker may attempt to intercept sensitive information when it is
transmitted without adequate encryption, obtain sensitive data that has been
improperly stored, or exploit weak cryptographic implementations. For
example, if passwords are stored using an unsuitable hashing method or
sensitive information is transmitted over an insecure connection, an attacker
who gains access to that data may be able to recover or misuse it.

**Real-World Example:**

A well-known example of cryptographic failure is the 2012 LinkedIn
password breach. Millions of LinkedIn password hashes were exposed, and
the passwords had been stored using unsalted SHA-1 hashing. Because the
hashing approach was not sufficiently resistant to modern password
cracking techniques, many of the exposed passwords could eventually be
recovered.

This incident demonstrates why sensitive credentials must be protected
using modern password-hashing algorithms and appropriate cryptographic
controls rather than relying on outdated or weak hashing methods.

**Prevention:**

- Encrypt sensitive data both at rest and in transit.
- Use modern, well-tested cryptographic algorithms and libraries.
- Use HTTPS/TLS for sensitive communications and properly enforce secure
  connections.
- Never use deprecated algorithms such as MD5 or SHA-1 for security-sensitive
  purposes.
- Store passwords using strong, adaptive, salted password-hashing algorithms
  such as Argon2, scrypt, or PBKDF2.
- Generate cryptographic keys and random values using secure cryptographic
  random number generators.
- Never hard-code cryptographic keys in source code or public repositories.
- Implement proper key storage, rotation, and management.
- Avoid storing sensitive information when it is not necessary.

**Potential Impact:**

Cryptographic failures can expose sensitive information such as passwords,
personal data, financial information, session tokens, or business secrets.
Depending on the weakness, attackers may be able to recover sensitive data,
hijack user sessions, or compromise systems and accounts.

---

## 4. A05:2025 — Injection

**What it is:**

Injection occurs when an application sends untrusted user input to an
interpreter, such as a database, operating system command shell, or web
browser, without properly separating data from commands. This can cause
the interpreter to treat part of the user's input as executable instructions
instead of ordinary data.

Common examples include SQL Injection, NoSQL Injection, OS Command
Injection, LDAP Injection, and Cross-Site Scripting (XSS).

**How an attacker could exploit it:**

An attacker may provide specially crafted input through a form field, URL
parameter, HTTP header, cookie, or API request. If the application directly
uses that input inside a query or command without proper protection, the
attacker may be able to change the intended operation.

For example, in a vulnerable SQL query, an attacker might manipulate an
input parameter to alter the query's logic and access records that should
not be available to them. In an OS command injection vulnerability, specially
crafted input could cause the server to execute unintended operating-system
commands.

**Real-World Example:**

A well-known example of SQL Injection is the 2008 Heartland Payment Systems
breach. Attackers exploited SQL injection vulnerabilities in Heartland's
web-facing systems and gained unauthorized access to payment-card data.

The incident affected millions of payment card records and demonstrated how
an injection vulnerability can move beyond unauthorized database access and
result in major financial and business consequences.

This case shows why applications must treat user-supplied input as
untrusted data and ensure that it cannot alter the structure or meaning of
database queries.

**Prevention:**

- Keep user-supplied data separate from commands and queries.
- Use parameterized queries or prepared statements for database operations.
- Prefer safe APIs and secure ORM features instead of dynamically constructing
  queries or commands.
- Perform positive server-side input validation where appropriate.
- Avoid directly concatenating untrusted input into SQL queries or operating
  system commands.
- Apply context-specific output encoding when handling data that will be
  interpreted by another component.
- Use security testing such as SAST, DAST, and fuzzing to identify injection
  vulnerabilities before deployment.
- Run application components with the minimum privileges required.
- Regularly review and test input-handling logic.

**Potential Impact:**

Injection vulnerabilities can allow attackers to access unauthorized
information, modify or delete data, bypass application controls, execute
unintended commands, or potentially take control of affected systems.
The impact depends on the type of interpreter involved and the privileges
available to the vulnerable application.

---

## 5. A07:2025 — Authentication Failures

**What it is:**

Authentication Failures occur when an application incorrectly verifies a
user's identity, allowing an attacker to gain access to an account or
continue using an authenticated session without proper authorization.

Common examples include weak or default passwords, missing multi-factor
authentication, ineffective password recovery, brute-force protection
failures, credential stuffing, and incorrect session management.

**How an attacker could exploit it:**

An attacker may attempt to use stolen username and password combinations
through credential stuffing, repeatedly guess passwords against an account
when brute-force protections are missing, or exploit weak password-reset
mechanisms.

Authentication weaknesses can also occur when an application fails to
properly invalidate sessions after logout or exposes session identifiers in
insecure locations. If these controls are not implemented correctly, an
attacker may be able to gain or maintain unauthorized access to a victim's
account.

**Real-World Example:**

A well-known example of authentication-related weaknesses is the 2021
attack against Colonial Pipeline. The attackers gained access to the
company's network using a compromised VPN account that did not have
multi-factor authentication enabled.

The incident demonstrates how relying on a single authentication factor can
allow stolen credentials to become an entry point into an organization's
network. Strong authentication controls, particularly multi-factor
authentication, can significantly reduce the risk associated with
compromised credentials.

**Prevention:**

- Implement multi-factor authentication wherever possible.
- Do not use default, weak, or hard-coded credentials.
- Protect accounts against brute-force and credential-stuffing attacks by
  limiting or delaying repeated failed login attempts.
- Check new passwords against known breached and commonly used passwords.
- Use secure password-hashing algorithms such as Argon2, scrypt, or PBKDF2.
- Implement secure password-reset and account-recovery mechanisms.
- Use secure, server-side session management.
- Generate a new random session identifier after successful authentication.
- Store session identifiers securely and never expose them in URLs.
- Properly invalidate sessions and authentication tokens after logout and
  when sessions expire.
- Use generic authentication error messages to reduce account enumeration.
- Log authentication failures and alert on suspicious authentication
  activity.

  **Potential Impact:**

Authentication failures can allow attackers to gain unauthorized access to
user or administrator accounts. This may result in data theft, account
takeover, unauthorized transactions, privilege abuse, exposure of sensitive
information, or further compromise of the application and its resources.

---

## Personal Reflection

The vulnerability that surprised me the most was Broken Access Control
because I initially thought that authentication alone provided strong
protection for user data and functionality. While researching this topic,
I learned that correctly identifying a user is only one part of security;
the application must also verify what that user is actually allowed to
access or modify. My experience with authorized bug bounty testing also
helped me understand how access control issues can occur in real-world
applications. This research made me more aware of the importance of
server-side authorization checks and the principle of least privilege.

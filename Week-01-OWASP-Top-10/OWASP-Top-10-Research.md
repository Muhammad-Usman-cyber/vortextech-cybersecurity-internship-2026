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

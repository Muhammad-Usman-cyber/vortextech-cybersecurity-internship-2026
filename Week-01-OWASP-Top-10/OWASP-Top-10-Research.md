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

# Week 4 — Mini Incident Response Plan (Advanced)

Final task of the Vortex Tech Cybersecurity Internship 2026.

This project develops a structured incident response plan for a
fictional cybersecurity breach using a NIST-aligned incident response
lifecycle (Preparation, Detection & Analysis, Containment, Eradication,
Recovery, Post-Incident/Lessons Learned).

**Scenario:** NovaCart Technologies (fictional e-commerce company) — an
API endpoint failed to enforce authorization, allowing unauthorized
access to customer names, emails, shipping addresses, and order data.

## Files in this folder

- **`incident-response-plan.md`** — the full response plan: incident
  scenario, objectives, all six NIST phases, preventative measures,
  and a final assessment. Points to the two files below for the
  detailed communication plan and timeline.
- **`communication-plan.md`** — a detailed breakdown of who gets
  notified, when, and with what information, from the SOC through to
  executive leadership, legal/compliance, customers, and regulators.
- **`incident-timeline.md`** — a phase-by-phase hypothetical timeline
  of the incident, from initial detection through recovery and
  post-recovery monitoring, with observations on the reasoning behind
  the sequencing.

## Key takeaways

- Authorization must be enforced server-side on every protected
  endpoint — never assumed from the client.
- Early containment (disabling the endpoint, revoking credentials,
  invalidating sessions) should happen without destroying evidence
  needed for the investigation.
- Communication should scale with confirmed impact: technical teams
  first, then security/executive leadership, then legal, then
  customers and regulators only once facts are verified.

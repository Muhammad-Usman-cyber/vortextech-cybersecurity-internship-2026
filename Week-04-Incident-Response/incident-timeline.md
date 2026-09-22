# Incident Timeline

## Vortex Tech Cybersecurity Internship 2026 — Week 4

### Incident: Unauthorized Customer Database Access Through a Vulnerable API Endpoint

---

## Purpose

This document provides a simplified, hypothetical timeline of the
NovaCart Technologies incident, from initial detection through
recovery and increased monitoring. It complements
`Mini-Incident-Response-Plan.md` and `Incident-Communication-Plan.md`
in this folder.

---

## Timeline

| Time | Event | Phase |
|---|---|---|
| 09:10 | Security monitoring detects abnormal API activity | Detection & Analysis |
| 09:15 | SOC analyst begins triage | Detection & Analysis |
| 09:30 | Affected API endpoint identified | Detection & Analysis |
| 09:45 | Unauthorized access is confirmed | Detection & Analysis |
| 10:00 | Incident response team activated | Detection & Analysis |
| 10:15 | Affected endpoint restricted | Containment |
| 10:30 | Relevant logs and evidence preserved | Containment |
| 11:00 | Scope investigation begins | Detection & Analysis |
| 13:00 | API authorization weakness identified as likely root cause | Eradication |
| 14:00 | Remediation begins | Eradication |
| 16:00 | Security validation completed | Eradication |
| 17:00 | Service recovery begins | Recovery |
| 18:00 | Increased monitoring activated | Recovery |

> Times are hypothetical and are included to demonstrate a realistic
> incident-response workflow, aligned to the NIST Incident Response
> lifecycle phases shown in the table above.

---

## Observations

- The gap between detection (09:10) and confirmed unauthorized access
  (09:45) reflects a realistic triage window for an initial alert.
- Containment (10:15–10:30) happens before deep scope investigation
  (11:00) — stopping the bleeding takes priority over full root-cause
  analysis, while evidence is still preserved.
- Root cause identification (13:00) and remediation (14:00–16:00) make
  up the longest phase of the timeline, consistent with how eradication
  of an authorization flaw typically requires code changes and
  validation before it can be trusted.
- Recovery (17:00) only begins after eradication is validated, and
  monitoring stays elevated (18:00 onward) rather than ending at
  service restoration.

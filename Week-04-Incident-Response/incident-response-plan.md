# Mini Incident Response Plan

## Vortex Tech Cybersecurity Internship 2026 — Week 4

### Incident: Unauthorized Customer Database Access Through a Vulnerable API Endpoint

---

## 1. Executive Summary

This document presents a hypothetical incident response plan for
NovaCart Technologies, a fictional e-commerce company.

The scenario involves unauthorized access to customer information
through a vulnerable API endpoint that failed to enforce appropriate
authorization controls.

The incident response plan follows a NIST-aligned lifecycle:

1. Preparation
2. Detection & Analysis
3. Containment
4. Eradication
5. Recovery
6. Post-Incident / Lessons Learned

The objective is to provide a structured response that allows the
security team to detect, contain, investigate, remediate, and recover
from the incident while reducing the likelihood of recurrence.

> **Note:** NovaCart Technologies and this incident are entirely
> fictional and are used for educational purposes.

---

# 2. Incident Scenario

## 2.1 Organization

**Company:** NovaCart Technologies

**Industry:** E-commerce

**Environment:**

- Customer-facing web application
- Mobile application
- REST API infrastructure
- Customer database
- Authentication services
- Cloud-hosted application servers
- Centralized application and security logging

## 2.2 Initial Incident

NovaCart's security monitoring system identifies an unusual increase
in requests to a customer-data API endpoint.

Initial investigation indicates that the endpoint can be accessed
without proper authorization checks.

An unauthorized party appears to have queried customer records
through the vulnerable endpoint.

Potentially exposed information includes:

- Customer names
- Email addresses
- Shipping addresses
- Order information
- Account-related metadata

No evidence initially confirms that payment-card information was
accessed.

## 2.3 How the Incident Was Discovered

The incident is initially identified through abnormal API activity.

The security monitoring team observes:

- Unusual request volume
- Repeated requests to a customer-data endpoint
- Requests originating from an unfamiliar source
- Access patterns inconsistent with normal application behaviour

The alert triggers an investigation by the security team.

## 2.4 Initial Security Assessment

The initial assessment indicates that the likely root cause is an
authorization failure in the API.

The endpoint should have required authenticated and authorized access
but was instead accessible without adequate authorization enforcement.

At this stage, the organization treats the incident as a potential
customer-data exposure until investigation determines the actual
scope.

---

# 3. Incident Response Objectives

The response team will focus on the following objectives:

1. Stop unauthorized access.
2. Preserve evidence required for investigation.
3. Determine the scope and duration of the incident.
4. Identify affected systems and data.
5. Remove the root cause.
6. Restore services safely.
7. Communicate appropriately with internal stakeholders.
8. Implement controls to reduce the likelihood of recurrence.

---

# 4. Preparation

Preparation covers the security capabilities that should already exist
before an incident occurs.

## 4.1 Required Preparation

NovaCart should maintain:

- Documented incident response procedures
- Defined security and IT response roles
- Centralized application and security logging
- API access logging
- Database audit logging
- Authentication and authorization monitoring
- Secure backups
- Asset and system inventories
- Vulnerability management processes
- Access-control reviews
- Incident communication procedures

## 4.2 Monitoring

The security team should monitor for:

- Unusual API request patterns
- Repeated authorization failures
- Unusual database queries
- Unexpected geographic or source changes
- Excessive data retrieval
- Suspicious account activity

## 4.3 Evidence Preparation

Systems should be configured so that relevant logs are retained and
protected from unauthorized modification.

Important sources include:

- API gateway logs
- Web server logs
- Application logs
- Authentication logs
- Database audit logs
- Firewall/WAF logs
- Endpoint/security monitoring logs

---

# 5. Detection & Analysis

The Detection & Analysis phase begins when the unusual API activity
is identified.

## 5.1 Initial Detection

The security monitoring system generates an alert because API activity
shows an abnormal request pattern.

The SOC analyst reviews the alert and confirms that the activity is
outside the expected baseline.

## 5.2 Initial Investigation

The response team should:

1. Identify the affected API endpoint.
2. Determine when abnormal activity began.
3. Identify source IP addresses and request patterns.
4. Review authentication information associated with requests.
5. Review API and application logs.
6. Review database query activity.
7. Determine what records may have been accessed.
8. Check whether other endpoints were targeted.
9. Identify evidence of persistence or additional compromise.

## 5.3 Scope Analysis

The investigation should determine:

- First observed suspicious request
- Last observed suspicious request
- Number of requests
- Potential number of records accessed
- Types of information involved
- Systems accessed
- Accounts potentially affected
- Whether additional vulnerabilities were exploited

## 5.4 Evidence Preservation

Relevant logs and other forensic evidence should be preserved before
major remediation changes are made.

Evidence should include:

- API request logs
- Authentication records
- Application logs
- Database audit logs
- Relevant system logs
- Security alerts
- Configuration snapshots

---

# 6. Containment

The immediate objective of containment is to stop additional
unauthorized access while preserving sufficient evidence for the
investigation.

## 6.1 Immediate Containment

The security team should:

1. Disable or restrict the affected API endpoint.
2. Deploy or strengthen temporary access-control rules.
3. Block identified malicious sources where appropriate.
4. Revoke potentially compromised API credentials.
5. Review active sessions and invalidate suspicious sessions.
6. Restrict access to affected systems.
7. Increase monitoring on related services.

## 6.2 Short-Term Containment

The team should also:

- Review related API endpoints for similar weaknesses.
- Restrict unnecessary database access.
- Apply temporary WAF/API gateway controls.
- Increase logging and alerting.
- Monitor for continued exploitation attempts.

Containment should be performed carefully so that evidence is not
unnecessarily destroyed.

---

# 7. Eradication

Eradication removes the root cause and any unauthorized access
mechanisms associated with the incident.

## 7.1 Remove Root Cause

The vulnerable API endpoint should be corrected so that:

- Authentication is properly enforced.
- Authorization is checked for every protected resource.
- Users can access only data they are permitted to access.
- Sensitive endpoints are not exposed without appropriate controls.

## 7.2 Security Review

The response team should perform a broader review of:

- API authorization controls
- Authentication mechanisms
- Access-control policies
- Application configuration
- Database permissions
- Secrets and API keys
- Related endpoints

## 7.3 Credential and Access Review

If there is evidence that credentials or sessions were exposed:

- Rotate affected credentials.
- Revoke unnecessary tokens.
- Invalidate suspicious sessions.
- Review privileged accounts.
- Confirm least-privilege access.

## 7.4 Validation

Before returning systems to normal operation, the security team
should verify that the vulnerability has been removed and that
related controls are functioning as expected.

---

# 8. Recovery

Recovery focuses on safely restoring normal operations.

## 8.1 Restore Services

Once remediation has been validated:

1. Restore the affected API functionality.
2. Re-enable required services gradually.
3. Verify authentication and authorization.
4. Confirm expected application behaviour.
5. Monitor API activity closely.

## 8.2 Increased Monitoring

For an initial monitoring period after recovery, the SOC should pay
particular attention to:

- API access patterns
- Authorization failures
- Database queries
- Authentication anomalies
- Repeated requests against previously affected endpoints
- Attempts to exploit related vulnerabilities

## 8.3 Recovery Validation

The team should confirm:

- The original vulnerability is fixed.
- No unauthorized access remains.
- Logs are functioning correctly.
- Security controls are active.
- Application functionality has returned to normal.
- Backups remain available if needed.

---

# 9. Post-Incident / Lessons Learned

After recovery, NovaCart should conduct a formal post-incident review.

## 9.1 Root Cause

The primary root cause in this scenario was an API authorization
failure that allowed access to customer data without sufficient
authorization checks.

## 9.2 Contributing Factors

Potential contributing factors include:

- Insufficient API security testing
- Incomplete access-control reviews
- Lack of monitoring for abnormal data access
- Excessive permissions
- Insufficient security testing during deployment

## 9.3 Lessons Learned

The organization should review:

- Why the vulnerability reached production.
- Why it was not detected earlier.
- Whether similar endpoints contain the same weakness.
- Whether monitoring generated sufficient visibility.
- Whether incident escalation procedures worked effectively.
- Whether evidence collection and communication were timely.

## 9.4 Improvements

The post-incident review should result in concrete actions such as:

- Stronger API authorization testing
- Regular security assessments
- Improved logging and monitoring
- Security review of sensitive endpoints
- Updated incident response procedures
- Better access-control verification

---

# 10. Internal Communication Plan

Communication should follow the organization's incident severity and
data-impact assessment.

| Time | Stakeholder | Communication |
|---|---|---|
| Immediately | SOC / Security Team | Begin investigation and incident tracking |
| Immediately | IT / Engineering | Notify technical owners of affected systems |
| Early in investigation | Security Leadership | Provide initial scope and status |
| Once material impact is suspected | Executive Leadership | Provide incident summary and business impact |
| During investigation | Legal / Compliance | Review potential privacy and regulatory implications |
| When facts are established | Affected Customers | Provide appropriate notification where required |
| When legally or contractually required | Regulators / Authorities | Follow applicable notification requirements |

All communications should be based on verified information and should
avoid speculation about the incident's scope.

---

# 11. Preventative Measures

The following preventative measures are directly related to the root
cause of the incident.

## 11.1 Strong API Authorization

Every protected API endpoint should enforce authentication and
resource-level authorization.

Authorization should be validated server-side rather than relying
on the client application.

## 11.2 Continuous Security Testing

Sensitive APIs should be included in:

- Secure code reviews
- Automated security testing
- Manual penetration testing
- Access-control testing
- Pre-production security assessments

## 11.3 Security Monitoring & Alerting

Centralized monitoring should detect:

- Unusual API access
- Excessive record retrieval
- Authorization failures
- Suspicious source changes
- Abnormal database activity

This provides earlier visibility into attempted or successful
unauthorized access.

---

# 12. Incident Timeline

A simplified incident timeline is provided below.

| Time | Event |
|---|---|
| 09:10 | Security monitoring detects abnormal API activity |
| 09:15 | SOC analyst begins triage |
| 09:30 | Affected API endpoint identified |
| 09:45 | Unauthorized access is confirmed |
| 10:00 | Incident response team activated |
| 10:15 | Affected endpoint restricted |
| 10:30 | Relevant logs and evidence preserved |
| 11:00 | Scope investigation begins |
| 13:00 | API authorization weakness identified as likely root cause |
| 14:00 | Remediation begins |
| 16:00 | Security validation completed |
| 17:00 | Service recovery begins |
| 18:00 | Increased monitoring activated |

> Times are hypothetical and are included to demonstrate a realistic
> incident-response workflow.

---

# 13. Final Assessment

This incident demonstrates how a relatively small application security
weakness can develop into a broader security incident when sensitive
data is accessible through an improperly protected API.

The response requires coordination between security, engineering,
IT, leadership, and legal/compliance stakeholders.

The key defensive lessons are:

- Enforce authorization at the server.
- Monitor access to sensitive resources.
- Preserve useful security logs.
- Test APIs for access-control weaknesses.
- Maintain a documented incident response process.
- Review and improve controls after every significant incident.

---

# 14. Conclusion

A structured incident response process allows an organization to move
from initial detection through containment, eradication, recovery, and
continuous improvement.

This hypothetical exercise demonstrates the importance of combining
technical controls, monitoring, evidence preservation, communication,
and preventive security measures when responding to a customer-data
security incident.

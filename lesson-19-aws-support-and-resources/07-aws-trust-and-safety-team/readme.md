# 🛡️ AWS Trust and Safety Team

## File Structure

```
lesson-19-aws-support-and-resources/
└── 07-aws-trust-and-safety-team/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The AWS Trust and Safety Team is responsible for addressing abuse issues related to AWS resources. This team handles reports of suspected abusive, illegal, or harmful activities originating from AWS infrastructure. Understanding when and how to contact this team, as well as compliance resources, is important for the AWS Certified Cloud Practitioner exam.

## What is the AWS Trust and Safety Team?

The AWS Trust and Safety Team investigates and responds to:

- Abuse reports regarding AWS resources
- Violations of the AWS Acceptable Use Policy
- Security concerns related to AWS infrastructure
- Illegal content or activities hosted on AWS

```
┌────────────────────────────────────────────────────────────────────────────┐
│                    AWS TRUST AND SAFETY TEAM                                │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│                      ┌─────────────────────────┐                           │
│                      │   AWS Trust & Safety    │                           │
│                      │        Team             │                           │
│                      └───────────┬─────────────┘                           │
│                                  │                                         │
│              ┌───────────────────┼───────────────────┐                    │
│              │                   │                   │                     │
│              ▼                   ▼                   ▼                     │
│     ┌────────────────┐  ┌────────────────┐  ┌────────────────┐            │
│     │    Abuse       │  │   Policy       │  │   Security     │            │
│     │    Reports     │  │   Violations   │  │   Incidents    │            │
│     └────────────────┘  └────────────────┘  └────────────────┘            │
│                                                                            │
│     Spam, phishing,     AWS Acceptable     Malware, DDoS,                 │
│     malicious content   Use Policy         intrusion attempts             │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## AWS Acceptable Use Policy (AUP)

### Overview

The AWS Acceptable Use Policy defines prohibited activities for all AWS customers. Violations can result in account suspension or termination.

### Prohibited Activities

| Category | Examples |
|----------|----------|
| **Illegal Content** | Child exploitation material, illegal gambling |
| **Security Violations** | Hacking, unauthorized access attempts |
| **Network Abuse** | DDoS attacks, spam distribution |
| **Harmful Content** | Malware hosting, phishing sites |
| **Email Abuse** | Sending unsolicited bulk emails |
| **Copyright Violations** | Pirated content distribution |

### AUP Violation Categories

```
┌────────────────────────────────────────────────────────────────────────────┐
│                  ACCEPTABLE USE POLICY VIOLATIONS                           │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   ILLEGAL ACTIVITIES                                                       │
│      - Content that violates laws                                          │
│      - Fraudulent activities                                               │
│      - Intellectual property violations                                    │
│                                                                            │
│   SECURITY THREATS                                                         │
│      - Unauthorized access attempts                                        │
│      - Network probing/scanning                                            │
│      - Distributing malware                                                │
│                                                                            │
│   MESSAGING ABUSE                                                          │
│      - Spam distribution                                                   │
│      - Phishing campaigns                                                  │
│      - Unsolicited communications                                          │
│                                                                            │
│   HARMFUL CONDUCT                                                          │
│      - DDoS attacks                                                        │
│      - Resource exhaustion                                                 │
│      - Interference with AWS services                                      │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## Reporting Abuse

### How to Report

If you observe abusive activities originating from AWS resources:

| Method | Details |
|--------|---------|
| **Web Form** | abuse.amazonaws.com |
| **Email** | abuse@amazonaws.com |
| **Information Required** | IP addresses, timestamps, evidence |

### What to Include in a Report

```
┌────────────────────────────────────────────────────────────────────────────┐
│                    ABUSE REPORT REQUIREMENTS                                │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   Required Information:                                                    │
│   ─────────────────────                                                    │
│                                                                            │
│   1. Source IP Address(es)                                                 │
│      - IP addresses involved in the abuse                                  │
│                                                                            │
│   2. Timestamps (UTC)                                                      │
│      - When the activity occurred                                          │
│                                                                            │
│   3. Log Files / Evidence                                                  │
│      - Server logs, email headers, screenshots                             │
│                                                                            │
│   4. Type of Abuse                                                         │
│      - Spam, phishing, DDoS, malware, etc.                                │
│                                                                            │
│   5. Your Contact Information                                              │
│      - Email for follow-up                                                 │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### Common Abuse Types

| Abuse Type | Description | Evidence Needed |
|------------|-------------|-----------------|
| **Spam** | Unsolicited emails from AWS IPs | Email headers, message samples |
| **Phishing** | Fraudulent sites mimicking legitimate ones | URLs, screenshots |
| **Malware** | Hosting malicious software | URLs, file hashes |
| **Port Scanning** | Unauthorized network reconnaissance | Firewall logs, IPs |
| **DDoS** | Distributed denial of service attacks | Traffic logs, timestamps |
| **Intrusion Attempts** | Unauthorized access attempts | Security logs, IPs |

## AWS Response to Abuse Reports

### Investigation Process

```
┌────────────────────────────────────────────────────────────────────────────┐
│                    ABUSE INVESTIGATION PROCESS                              │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   1. Report Received                                                       │
│      │                                                                     │
│      ▼                                                                     │
│   2. Initial Review                                                        │
│      │   AWS validates the report                                          │
│      ▼                                                                     │
│   3. Investigation                                                         │
│      │   Identify the AWS customer responsible                             │
│      ▼                                                                     │
│   4. Customer Notification                                                 │
│      │   AWS contacts the account owner                                    │
│      ▼                                                                     │
│   5. Remediation Required                                                  │
│      │   Customer must address the issue                                   │
│      ▼                                                                     │
│   6. Verification                                                          │
│      │   AWS confirms issue is resolved                                    │
│      ▼                                                                     │
│   7. Case Closed or Escalation                                             │
│         Non-compliance may result in account action                        │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### Potential Actions

| Severity | AWS Response |
|----------|--------------|
| **Minor** | Warning notification to customer |
| **Moderate** | Required remediation with deadline |
| **Severe** | Immediate resource suspension |
| **Critical/Repeated** | Account termination |

## Compliance Resources

### AWS Compliance Programs

AWS maintains compliance with numerous regulatory frameworks and industry standards:

| Category | Programs |
|----------|----------|
| **Global** | ISO 27001, ISO 27017, ISO 27018, SOC 1/2/3 |
| **US Government** | FedRAMP, GovCloud, ITAR |
| **Healthcare** | HIPAA, HITRUST |
| **Financial** | PCI DSS, SOX |
| **Privacy** | GDPR, CCPA |

### AWS Artifact

AWS Artifact provides on-demand access to compliance documentation:

```
┌────────────────────────────────────────────────────────────────────────────┐
│                         AWS ARTIFACT                                        │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   ┌─────────────────────────────────────────────────────────────────┐     │
│   │                    Reports & Certifications                      │     │
│   │   - SOC reports                                                  │     │
│   │   - ISO certifications                                           │     │
│   │   - PCI compliance reports                                       │     │
│   │   - Third-party audit reports                                    │     │
│   └─────────────────────────────────────────────────────────────────┘     │
│                                                                            │
│   ┌─────────────────────────────────────────────────────────────────┐     │
│   │                    Agreements                                    │     │
│   │   - Business Associate Addendum (BAA) for HIPAA                  │     │
│   │   - GDPR Data Processing Addendum                                │     │
│   │   - Custom agreements                                            │     │
│   └─────────────────────────────────────────────────────────────────┘     │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### Compliance Center

AWS provides a Compliance Center with:

- Compliance program information
- Security documentation
- Industry-specific guidance
- Regulatory requirements

## Customer vs AWS Responsibilities

### Shared Responsibility for Compliance

```
┌────────────────────────────────────────────────────────────────────────────┐
│              COMPLIANCE SHARED RESPONSIBILITY                               │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   AWS Responsibility:                                                      │
│   ──────────────────                                                       │
│   - Infrastructure compliance                                              │
│   - Physical security certifications                                       │
│   - Network infrastructure compliance                                      │
│   - AWS service certifications                                             │
│                                                                            │
│   Customer Responsibility:                                                 │
│   ───────────────────────                                                  │
│   - Data classification                                                    │
│   - Application security                                                   │
│   - Access management                                                      │
│   - Operating system/network configuration                                 │
│   - Regulatory compliance for their applications                          │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## Trust and Safety vs AWS Support

| Aspect | Trust and Safety | AWS Support |
|--------|-----------------|-------------|
| **Purpose** | Abuse and policy violations | Technical and account help |
| **Who Contacts** | External reporters, law enforcement | AWS customers |
| **Issues Handled** | Spam, malware, illegal content | Technical problems, billing |
| **Contact** | abuse@amazonaws.com | Support Center |
| **Response** | Investigation and enforcement | Technical assistance |

## Protecting Your AWS Resources

### Best Practices

| Practice | Description |
|----------|-------------|
| **Secure Credentials** | Protect AWS access keys and passwords |
| **Monitor Usage** | Watch for unauthorized resource usage |
| **Enable Logging** | Use CloudTrail and VPC Flow Logs |
| **Update Software** | Keep systems patched and updated |
| **Incident Response** | Have a plan for security incidents |

### If You Receive an Abuse Notice

```
┌────────────────────────────────────────────────────────────────────────────┐
│                RESPONDING TO AN ABUSE NOTICE                                │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   1. Don't Ignore It                                                       │
│      - Respond promptly to avoid escalation                                │
│                                                                            │
│   2. Investigate Immediately                                               │
│      - Determine if your resources are compromised                         │
│      - Check for unauthorized access                                       │
│                                                                            │
│   3. Take Corrective Action                                                │
│      - Stop the abusive activity                                           │
│      - Remove malicious content                                            │
│      - Secure compromised resources                                        │
│                                                                            │
│   4. Respond to AWS                                                        │
│      - Explain actions taken                                               │
│      - Provide timeline for remediation                                    │
│                                                                            │
│   5. Implement Preventive Measures                                         │
│      - Strengthen security controls                                        │
│      - Monitor for future issues                                           │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## 🎯 Exam Tips

- **AWS Trust and Safety Team** handles abuse reports, NOT technical support issues
- Use **abuse@amazonaws.com** to report suspected abuse from AWS resources
- The **AWS Acceptable Use Policy** defines prohibited activities
- **AWS Artifact** provides compliance reports and certifications
- Know the difference between **Trust and Safety** (abuse) and **AWS Support** (technical help)
- Customers are responsible for **their own compliance** with regulations
- AWS provides **infrastructure compliance** through various certifications
- Abuse violations can result in **account suspension or termination**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| AWS Trust and Safety | Team that investigates abuse reports and policy violations |
| Acceptable Use Policy (AUP) | AWS policy defining prohibited activities |
| Abuse Report | Notification of suspected harmful activities from AWS resources |
| AWS Artifact | Service providing compliance documentation and agreements |
| Compliance Program | Set of controls meeting regulatory requirements |
| BAA | Business Associate Addendum for HIPAA compliance |
| SOC Report | System and Organization Controls audit report |

## 💡 Key Takeaways

1. **AWS Trust and Safety Team** handles abuse issues, not technical support
2. Report abuse to **abuse@amazonaws.com** with evidence (IPs, timestamps, logs)
3. **Acceptable Use Policy** violations can lead to account suspension
4. **AWS Artifact** provides on-demand access to compliance documents
5. **Shared responsibility** applies to compliance - AWS secures infrastructure, customers secure their data
6. Respond promptly to abuse notices to avoid account escalation
7. Different from AWS Support - Trust and Safety handles **abuse**, Support handles **technical issues**
8. AWS maintains numerous **compliance certifications** (ISO, SOC, PCI, HIPAA, etc.)

---

*Previous: [06 - AWS Partner Network](../06-aws-partner-network/readme.md)*

---

## Lesson Summary

This lesson covered AWS Support and Resources, including:

1. **AWS Support Plans** - Five tiers from Basic to Enterprise with varying features and response times
2. **AWS Support Center** - Creating and managing support cases with severity levels
3. **AWS Trusted Advisor** - Five categories of automated best practice recommendations
4. **AWS Health Dashboard** - Personal and Service Health Dashboards for monitoring AWS health
5. **Technical Resources** - Documentation, whitepapers, re:Post, and Knowledge Center
6. **AWS Partner Network** - Consulting and Technology Partners for implementation help
7. **AWS Trust and Safety Team** - Handling abuse reports and compliance resources

*Return to: [Lesson 19 Overview](../readme.md)*

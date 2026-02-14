# 🤝 AWS Trust and Safety Team

## File Structure

```
lesson-08-security-resources-and-components/
└── 05-aws-trust-and-safety-team/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The AWS Trust and Safety Team is responsible for addressing abuse of AWS services and helping customers who are affected by or concerned about abusive activities. They work to maintain AWS as a safe and trustworthy platform.

## What is the AWS Trust and Safety Team?

```
+------------------------------------------------------------------+
|                  AWS TRUST AND SAFETY TEAM                        |
+------------------------------------------------------------------+
|                                                                   |
|   Mission: Protect AWS and its customers from abusive activities  |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                    RESPONSIBILITIES                       |   |
|   +----------------------------------------------------------+   |
|   |                                                           |   |
|   |   +------------------+    +------------------+            |   |
|   |   |  INVESTIGATE     |    |   RESPOND TO     |            |   |
|   |   |  Abuse Reports   |    |   Complaints     |            |   |
|   |   +------------------+    +------------------+            |   |
|   |                                                           |   |
|   |   +------------------+    +------------------+            |   |
|   |   |  TAKE ACTION     |    |   ASSIST         |            |   |
|   |   |  Against Abuse   |    |   Customers      |            |   |
|   |   +------------------+    +------------------+            |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Types of Abuse Handled

| Abuse Type | Description | Example |
|------------|-------------|---------|
| Spam | Unsolicited bulk messages | Email spam from EC2 |
| Malware | Malicious software distribution | Hosting malware |
| Phishing | Fraudulent websites | Fake login pages |
| DDoS | Distributed denial of service | Attack traffic from AWS |
| Port scanning | Unauthorized network scanning | Scanning external hosts |
| Intrusion attempts | Unauthorized access attempts | Brute force attacks |
| Copyright infringement | Hosting infringing content | Pirated content |

## When to Contact Trust and Safety

| Scenario | Action |
|----------|--------|
| You receive abuse notification | Respond and remediate |
| You detect abuse from AWS resources | Report to Trust and Safety |
| Your resources are being attacked | Contact AWS Support |
| You notice suspicious activity | Report to Trust and Safety |
| Third-party reports abuse to you | Investigate and report |

## How to Report Abuse

```
+------------------------------------------------------------------+
|                    REPORTING ABUSE TO AWS                         |
+------------------------------------------------------------------+
|                                                                   |
|   Method 1: AWS Abuse Form                                        |
|   +----------------------------------------------------------+   |
|   | https://support.aws.amazon.com/#/contacts/report-abuse    |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   Method 2: Email                                                 |
|   +----------------------------------------------------------+   |
|   | abuse@amazonaws.com                                       |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   Include in your report:                                         |
|   • IP addresses involved                                         |
|   • Timestamps (UTC preferred)                                    |
|   • Log excerpts                                                  |
|   • Description of abuse                                          |
|   • Evidence (screenshots, headers)                               |
|                                                                   |
+------------------------------------------------------------------+
```

## Receiving Abuse Notifications

If AWS detects abuse from your resources, you will receive a notification.

| Step | Action Required |
|------|----------------|
| 1. Receive notice | Check email associated with AWS account |
| 2. Investigate | Identify the source of abuse |
| 3. Remediate | Stop the abusive activity |
| 4. Respond | Reply to the Trust and Safety Team |
| 5. Prevent | Implement controls to prevent recurrence |

## Common Causes of Abuse Notifications

| Cause | Prevention |
|-------|------------|
| Compromised credentials | Enable MFA, rotate keys |
| Vulnerable applications | Patch and update software |
| Misconfigured security groups | Follow least privilege |
| Insider threat | Monitor user activity |
| Malware infection | Use antivirus, monitor |

## Trust and Safety Response Actions

| Severity | AWS Action |
|----------|------------|
| Low | Warning notification |
| Medium | Request for remediation |
| High | Temporary suspension |
| Critical | Immediate termination |

## Best Practices to Avoid Abuse Issues

1. **Enable security services** (GuardDuty, Config)
2. **Monitor for unusual activity** (CloudWatch, CloudTrail)
3. **Keep systems patched** and updated
4. **Use strong authentication** (MFA everywhere)
5. **Follow least privilege** for all access
6. **Respond promptly** to any abuse notifications
7. **Implement outbound filtering** where possible

## AWS Abuse Report Process

```
+------------------------------------------------------------------+
|                   ABUSE REPORT WORKFLOW                           |
+------------------------------------------------------------------+
|                                                                   |
|   External Party         AWS Trust          AWS Customer          |
|   Reports Abuse          & Safety           (Account Holder)      |
|   +----------+          +----------+        +----------+          |
|   | Submit   | -------> | Review & | -----> | Receive  |          |
|   | Report   |          | Validate |        | Notice   |          |
|   +----------+          +----------+        +----------+          |
|                              |                    |               |
|                              v                    v               |
|                         +----------+        +----------+          |
|                         | Monitor  | <----- | Remediate|          |
|                         | Response |        | Issue    |          |
|                         +----------+        +----------+          |
|                                                                   |
+------------------------------------------------------------------+
```

## Acceptable Use Policy (AUP)

AWS has an Acceptable Use Policy that all customers must follow.

| Prohibited Activity | Description |
|--------------------|-------------|
| Illegal activities | Anything violating law |
| Network abuse | DDoS, spam, unauthorized access |
| Security violations | Hacking, cracking |
| Content violations | Child exploitation, hate speech |
| Email abuse | Spam, spoofing |

## Trust and Safety vs Other Teams

| Team | Responsibility |
|------|----------------|
| Trust and Safety | Abuse investigation and response |
| AWS Support | Technical issues, troubleshooting |
| AWS Security | AWS infrastructure security |
| Customer Security | Customer's own security |

## 🎯 Exam Tips

- **Trust and Safety Team** handles abuse reports and complaints
- Report abuse to **abuse@amazonaws.com** or via the abuse form
- **Respond promptly** to abuse notifications to avoid suspension
- Abuse can result from **compromised credentials** or **vulnerable applications**
- Know the difference between **Trust and Safety** and **AWS Support**
- AWS can **suspend or terminate** accounts for serious violations
- Follow the **Acceptable Use Policy** (AUP)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Trust and Safety | AWS team handling abuse issues |
| Abuse Report | Notification of policy violation |
| AUP | Acceptable Use Policy |
| Remediation | Actions to fix abuse issues |
| Suspension | Temporary account restriction |

## 💡 Key Takeaways

1. AWS Trust and Safety Team handles abuse-related issues
2. Report abuse via email (abuse@amazonaws.com) or the abuse form
3. Respond promptly to any abuse notifications you receive
4. Common causes include compromised credentials and vulnerable software
5. AWS can suspend accounts for serious or repeated violations
6. Prevention through security best practices is essential
7. All AWS customers must comply with the Acceptable Use Policy

---

*Next: [Lesson 09 - Deploying and Operating in AWS](../../lesson-09-deploying-and-operating-in-aws/01-aws-management-tools-overview/readme.md)*

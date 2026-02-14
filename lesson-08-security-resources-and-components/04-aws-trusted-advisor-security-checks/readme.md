# ✅ AWS Trusted Advisor Security Checks

## File Structure

```
lesson-08-security-resources-and-components/
└── 04-aws-trusted-advisor-security-checks/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Trusted Advisor is a service that provides real-time guidance to help you optimize your AWS environment. It includes security checks that identify potential security vulnerabilities and recommend best practices.

## What is AWS Trusted Advisor?

Trusted Advisor inspects your AWS environment and provides recommendations across five categories.

```
+------------------------------------------------------------------+
|                    AWS TRUSTED ADVISOR                            |
+------------------------------------------------------------------+
|                                                                   |
|   +----------+  +----------+  +----------+  +----------+  +-----+ |
|   |   COST   |  |PERFORMANCE|  | SECURITY |  |  FAULT   |  |SERV | |
|   |OPTIMIZATION|  |          |  |          |  |TOLERANCE |  |LIMIT| |
|   +----------+  +----------+  +----------+  +----------+  +-----+ |
|                               |                                   |
|                               v                                   |
|                    +------------------+                           |
|                    |  SECURITY CHECKS |                           |
|                    +------------------+                           |
|                    | • IAM policies   |                           |
|                    | • MFA on root    |                           |
|                    | • Security groups|                           |
|                    | • S3 buckets     |                           |
|                    | • EBS encryption |                           |
|                    +------------------+                           |
|                                                                   |
+------------------------------------------------------------------+
```

## Trusted Advisor Tiers

| Tier | Security Checks Available | Cost |
|------|--------------------------|------|
| Basic | 7 core security checks | Free (all accounts) |
| Developer | 7 core security checks | Included with Support |
| Business | All security checks | Included with Support |
| Enterprise | All security checks + API access | Included with Support |

## Free Security Checks (All Accounts)

| Check | Description | Risk Level |
|-------|-------------|------------|
| S3 Bucket Permissions | Public read/write access | High |
| Security Groups - Unrestricted | Specific ports open to 0.0.0.0/0 | High |
| IAM Use | Whether IAM is being used | Medium |
| MFA on Root Account | Root account MFA enabled | High |
| EBS Public Snapshots | Publicly shared snapshots | High |
| RDS Public Snapshots | Publicly shared DB snapshots | High |
| Service Limits | Approaching service limits | Medium |

## Business/Enterprise Security Checks

| Check | Description |
|-------|-------------|
| IAM Access Key Rotation | Keys older than 90 days |
| IAM Password Policy | Password requirements met |
| Exposed Access Keys | Keys exposed on GitHub, etc. |
| CloudTrail Logging | Whether CloudTrail is enabled |
| ELB Listener Security | HTTPS/SSL configuration |
| ELB Security Groups | Load balancer security |
| CloudFront Custom SSL | Certificate configuration |
| Route 53 SPF Resource Records | Email security |

## Security Check Categories

```
+------------------------------------------------------------------+
|                  SECURITY CHECK CATEGORIES                        |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------------+    +------------------------+        |
|   |    ACCESS CONTROL      |    |    DATA PROTECTION     |        |
|   +------------------------+    +------------------------+        |
|   | • Security groups      |    | • S3 bucket policies   |        |
|   | • IAM policies         |    | • EBS encryption       |        |
|   | • MFA enabled          |    | • RDS encryption       |        |
|   | • Access key rotation  |    | • Public snapshots     |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
|   +------------------------+    +------------------------+        |
|   |    LOGGING & AUDIT     |    |    NETWORK SECURITY    |        |
|   +------------------------+    +------------------------+        |
|   | • CloudTrail enabled   |    | • Open security groups |        |
|   | • VPC Flow Logs        |    | • ELB security         |        |
|   | • S3 bucket logging    |    | • CloudFront SSL       |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## Check Status Indicators

| Color | Status | Meaning |
|-------|--------|---------|
| Green | OK | No issues found |
| Yellow | Warning | Investigation recommended |
| Red | Action Required | Security issue detected |
| Gray | Not Available | Check not accessible |

## How to Access Trusted Advisor

```
1. AWS Console -> Trusted Advisor
2. Dashboard shows all categories
3. Click "Security" for security checks
4. Review each check status
5. Follow recommendations
```

## Key Security Checks Explained

### MFA on Root Account

| Status | Meaning |
|--------|---------|
| Green | MFA is enabled on root |
| Red | MFA not enabled - immediate action needed |

### Security Groups - Specific Ports Unrestricted

| Port | Service | Risk |
|------|---------|------|
| 22 | SSH | Remote access exploitation |
| 3389 | RDP | Windows remote access |
| 3306 | MySQL | Database access |
| 5432 | PostgreSQL | Database access |

### S3 Bucket Permissions

| Issue | Risk |
|-------|------|
| Public read | Data exposure |
| Public write | Data tampering |
| ACL issues | Unauthorized access |

## Trusted Advisor vs Other Services

| Service | Focus |
|---------|-------|
| Trusted Advisor | Best practice recommendations |
| Security Hub | Security findings aggregation |
| Config | Configuration compliance |
| Inspector | Vulnerability scanning |
| GuardDuty | Threat detection |

## Automated Remediation

Trusted Advisor can trigger automated responses:

```
+------------------------------------------------------------------+
|                AUTOMATED REMEDIATION FLOW                         |
+------------------------------------------------------------------+
|                                                                   |
|   Trusted Advisor    EventBridge      Lambda        Fix           |
|   +-------------+    +----------+    +--------+    +--------+     |
|   |  Detects    | -> | Triggers | -> | Runs   | -> | Applied|     |
|   |  Issue      |    | Event    |    | Fix    |    |        |     |
|   +-------------+    +----------+    +--------+    +--------+     |
|                                                                   |
+------------------------------------------------------------------+
```

## Best Practices

1. **Review security checks weekly**
2. **Address red items immediately**
3. **Enable all available checks** (upgrade support if needed)
4. **Set up notifications** for status changes
5. **Automate remediation** where possible
6. **Document exceptions** for yellow/red items

## 🎯 Exam Tips

- **Trusted Advisor** provides real-time best practice recommendations
- **7 core checks are free** for all accounts, including key security checks
- **Business/Enterprise Support** unlocks all checks
- **Security checks** include MFA, security groups, S3 permissions, IAM
- Know the **color coding**: Green (OK), Yellow (Warning), Red (Action)
- **Cannot replace** specialized security services like GuardDuty
- Trusted Advisor checks **account-wide** configuration

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Trusted Advisor | AWS best practice recommendation service |
| Core Checks | 7 free checks available to all accounts |
| Security Pillar | Security category in Trusted Advisor |
| Check Status | Green, Yellow, Red, or Gray indicator |
| Business Support | Support tier with all Trusted Advisor checks |

## 💡 Key Takeaways

1. Trusted Advisor provides security best practice recommendations
2. Seven core security checks are free for all AWS accounts
3. Full security checks require Business or Enterprise Support
4. Key free checks: MFA, security groups, S3 permissions, public snapshots
5. Status indicators show OK (green), Warning (yellow), Action Required (red)
6. Trusted Advisor complements but doesn't replace dedicated security services
7. Regular review and remediation of findings improves security posture

---

*Next: [05 - AWS Trust and Safety Team](../05-aws-trust-and-safety-team/readme.md)*

# 🛡️ AWS Security Services Overview

## File Structure

```
lesson-08-security-resources-and-components/
└── 01-aws-security-services-overview/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides a comprehensive suite of security services to help protect your cloud infrastructure, data, and applications. These services cover identity management, threat detection, data protection, compliance, and network security.

## Security Service Categories

```
+------------------------------------------------------------------+
|               AWS SECURITY SERVICES ECOSYSTEM                     |
+------------------------------------------------------------------+
|                                                                   |
|  +------------------+  +------------------+  +------------------+ |
|  |    IDENTITY      |  |    DETECTION     |  |   PROTECTION    | |
|  +------------------+  +------------------+  +------------------+ |
|  | IAM              |  | GuardDuty        |  | WAF             | |
|  | IAM Identity Ctr |  | Security Hub     |  | Shield          | |
|  | Cognito          |  | Inspector        |  | Firewall Manager| |
|  | Directory Service|  | Detective        |  | Network Firewall| |
|  +------------------+  +------------------+  +------------------+ |
|                                                                   |
|  +------------------+  +------------------+  +------------------+ |
|  |      DATA        |  |   COMPLIANCE     |  |   MONITORING    | |
|  +------------------+  +------------------+  +------------------+ |
|  | KMS              |  | Artifact         |  | CloudTrail      | |
|  | CloudHSM         |  | Audit Manager    |  | Config          | |
|  | Secrets Manager  |  | Security Lake    |  | CloudWatch      | |
|  | Macie            |  |                  |  | Access Analyzer | |
|  +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Identity and Access Management Services

| Service | Purpose | Key Features |
|---------|---------|--------------|
| IAM | Identity and access control | Users, groups, roles, policies |
| IAM Identity Center | Single sign-on | Centralized access, federation |
| Cognito | App user identity | User pools, identity pools |
| Directory Service | Active Directory | Managed AD, AD Connector |
| STS | Temporary credentials | AssumeRole, federation |

## Threat Detection Services

| Service | Purpose | Key Features |
|---------|---------|--------------|
| GuardDuty | Intelligent threat detection | ML-based, continuous monitoring |
| Security Hub | Security posture dashboard | Aggregates findings, compliance |
| Inspector | Vulnerability assessment | EC2, ECR, Lambda scanning |
| Detective | Security investigation | Analyze, visualize events |
| Macie | Data discovery | Sensitive data identification |

## Data Protection Services

| Service | Purpose | Key Features |
|---------|---------|--------------|
| KMS | Key management | Create, manage encryption keys |
| CloudHSM | Hardware security modules | Dedicated HSM clusters |
| Secrets Manager | Secrets storage | Automatic rotation |
| Certificate Manager | SSL/TLS certificates | Free public certificates |

## Network Security Services

| Service | Purpose | Key Features |
|---------|---------|--------------|
| WAF | Web application firewall | SQL injection, XSS protection |
| Shield | DDoS protection | Standard (free), Advanced |
| Firewall Manager | Central firewall management | Cross-account policies |
| Network Firewall | VPC-level firewall | Stateful inspection |
| VPC Security | Network isolation | Security groups, NACLs |

## Compliance and Governance Services

| Service | Purpose | Key Features |
|---------|---------|--------------|
| Artifact | Compliance reports | SOC, PCI, ISO documents |
| Audit Manager | Audit preparation | Continuous auditing |
| Config | Resource configuration | Track changes, compliance |
| CloudTrail | API logging | Who did what, when |
| Organizations | Multi-account management | SCPs, consolidated billing |

## Security Service Integration

```
+------------------------------------------------------------------+
|                    SECURITY SERVICES FLOW                         |
+------------------------------------------------------------------+
|                                                                   |
|   Data Sources          Detection          Response               |
|   +---------+          +---------+        +---------+             |
|   |CloudTrail| ------> |GuardDuty| -----> |EventBridge|           |
|   |VPC Logs  |         |Security |        |Lambda   |             |
|   |DNS Logs  |         |Hub      |        |SNS      |             |
|   +---------+          +---------+        +---------+             |
|        |                    |                  |                  |
|        v                    v                  v                  |
|   +---------+          +---------+        +---------+             |
|   | Config  |          |Detective|        |Incident |             |
|   | Rules   |          |Analysis |        |Response |             |
|   +---------+          +---------+        +---------+             |
|                                                                   |
+------------------------------------------------------------------+
```

## Choosing the Right Security Service

| Need | Recommended Service |
|------|---------------------|
| Encrypt data at rest | KMS |
| Protect web applications | WAF |
| DDoS protection | Shield |
| Detect threats | GuardDuty |
| Track API calls | CloudTrail |
| Compliance reports | Artifact |
| Aggregate security findings | Security Hub |
| Manage secrets | Secrets Manager |
| Find sensitive data | Macie |

## 🎯 Exam Tips

- **GuardDuty** = threat detection using ML
- **Inspector** = vulnerability scanning (EC2, containers, Lambda)
- **Macie** = sensitive data discovery in S3
- **Security Hub** = aggregates findings from multiple services
- **Detective** = investigate and analyze security issues
- **WAF** = protect web apps from common attacks
- **Shield Standard** = free DDoS protection for all customers
- Know which services are **free** (Shield Standard, IAM) vs **paid**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| GuardDuty | Intelligent threat detection service |
| Security Hub | Centralized security findings dashboard |
| Inspector | Automated vulnerability assessment |
| Macie | Sensitive data discovery service |
| Detective | Security investigation service |
| WAF | Web Application Firewall |
| Shield | DDoS protection service |

## 💡 Key Takeaways

1. AWS provides security services across identity, detection, protection, and compliance
2. GuardDuty uses machine learning for intelligent threat detection
3. Security Hub aggregates findings from multiple security services
4. WAF and Shield protect against web attacks and DDoS
5. KMS and Secrets Manager handle encryption and secrets
6. CloudTrail and Config provide auditing and compliance capabilities
7. Most security services integrate with each other for comprehensive protection

---

*Next: [02 - AWS Marketplace Security Products](../02-aws-marketplace-security-products/readme.md)*

# Security Pillar

## Overview

The **Security** pillar focuses on protecting information, systems, and assets while delivering business value through risk assessments and mitigation strategies. Security is a foundational element that must be integrated into every aspect of your architecture.

## Definition

> Security is the ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies.

## Design Principles

| Principle | Description |
|-----------|-------------|
| **Implement a strong identity foundation** | Use least privilege, centralize identity management |
| **Enable traceability** | Monitor, alert, and audit all actions and changes |
| **Apply security at all layers** | Defense in depth - edge, VPC, load balancer, instance, OS, application |
| **Automate security best practices** | Use software-based security mechanisms |
| **Protect data in transit and at rest** | Encrypt data and manage encryption keys |
| **Keep people away from data** | Reduce direct access and manual processing |
| **Prepare for security events** | Have incident response procedures |

## Key Focus Areas

```
┌────────────────────────────────────────────────────────────────────────┐
│                         Security Pillar                                 │
├────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐   │
│  │  Identity & │  │Infrastructure│  │    Data     │  │  Incident   │   │
│  │   Access    │  │  Protection  │  │  Protection │  │  Response   │   │
│  │  Management │  │              │  │             │  │             │   │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘   │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────┐       │
│  │              Detection & Monitoring                          │       │
│  └─────────────────────────────────────────────────────────────┘       │
│                                                                         │
└────────────────────────────────────────────────────────────────────────┘
```

## Best Practices

### 1. Identity and Access Management (IAM)
- Use **IAM** for user and permission management
- Implement **least privilege** principle
- Use **MFA** (Multi-Factor Authentication)
- Use **IAM roles** instead of long-term credentials
- Regularly rotate credentials

### 2. Detection
- Enable **AWS CloudTrail** for API logging
- Use **Amazon GuardDuty** for threat detection
- Implement **AWS Security Hub** for security posture
- Use **Amazon Detective** for investigation

### 3. Infrastructure Protection
- Use **VPCs** to isolate networks
- Implement **Security Groups** and **NACLs**
- Use **AWS WAF** for web application protection
- Deploy **AWS Shield** for DDoS protection

### 4. Data Protection
- Encrypt data **at rest** (S3, EBS, RDS)
- Encrypt data **in transit** (TLS/SSL)
- Use **AWS KMS** for key management
- Classify data and implement appropriate controls

### 5. Incident Response
- Prepare incident response **runbooks**
- Practice with **game days**
- Use **AWS Config** rules for auto-remediation
- Implement **CloudWatch alarms** for security events

## AWS Security Services

| Category | Services |
|----------|----------|
| **Identity** | IAM, AWS Organizations, AWS SSO, Cognito |
| **Detection** | GuardDuty, Security Hub, Detective, Macie |
| **Network Protection** | VPC, Security Groups, WAF, Shield, Firewall Manager |
| **Data Protection** | KMS, CloudHSM, Certificate Manager, Secrets Manager |
| **Compliance** | CloudTrail, Config, Audit Manager, Artifact |

## Defense in Depth

```
                    ┌──────────────────┐
                    │   AWS Shield     │  ← Edge Protection
                    │   (DDoS)         │
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │    AWS WAF       │  ← Web Application Firewall
                    │                  │
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │   VPC / NACLs    │  ← Network Layer
                    │                  │
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │ Security Groups  │  ← Instance Level
                    │                  │
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │  OS / App Layer  │  ← Application Security
                    │                  │
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │  Data (KMS)      │  ← Data Encryption
                    │                  │
                    └──────────────────┘
```

## Shared Responsibility Model

Remember: Security is a **shared responsibility** between AWS and the customer.

| AWS Responsibility | Customer Responsibility |
|--------------------|------------------------|
| Physical security | Data classification |
| Network infrastructure | IAM configuration |
| Hypervisor security | Security group rules |
| Managed service security | Application security |
| | Data encryption |

## Exam Tips

- **Least privilege** is a fundamental security principle
- **MFA** should be enabled, especially for root account
- Know the difference between **Security Groups** (stateful) and **NACLs** (stateless)
- **Encryption** at rest and in transit is a common exam topic
- **CloudTrail** logs API calls, **GuardDuty** detects threats
- Security is a **shared responsibility**

## Key Takeaways

1. **Defense in depth** - Apply security at all layers
2. **Least privilege** - Give minimum permissions necessary
3. **Encrypt everything** - Data at rest and in transit
4. **Automate** - Use security automation to scale
5. **Prepare** - Have incident response procedures ready
6. **Monitor** - Enable logging and detection services

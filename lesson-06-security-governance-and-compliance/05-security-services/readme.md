# 🛡️ AWS Security Services

## File Structure

```
lesson-06-security-governance-and-compliance/
└── 05-security-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides a comprehensive suite of security services that help protect your infrastructure, data, and applications. Understanding these services is crucial for the Cloud Practitioner exam and for building secure cloud architectures.

## Security Service Categories

```
+------------------------------------------------------------------+
|                    AWS SECURITY SERVICES                          |
+------------------------------------------------------------------+
|                                                                   |
|  +------------------+  +------------------+  +------------------+ |
|  | Identity &       |  | Detection &      |  | Network &        | |
|  | Access           |  | Response         |  | Application      | |
|  +------------------+  +------------------+  +------------------+ |
|  | • IAM            |  | • GuardDuty      |  | • WAF            | |
|  | • IAM Identity   |  | • Security Hub   |  | • Shield         | |
|  |   Center         |  | • Inspector      |  | • Firewall Mgr   | |
|  | • Cognito        |  | • Detective      |  | • Network FW     | |
|  +------------------+  +------------------+  +------------------+ |
|                                                                   |
|  +------------------+  +------------------+  +------------------+ |
|  | Data             |  | Compliance &     |  | Incident         | |
|  | Protection       |  | Privacy          |  | Response         | |
|  +------------------+  +------------------+  +------------------+ |
|  | • KMS            |  | • Artifact       |  | • CloudTrail     | |
|  | • CloudHSM       |  | • Audit Manager  |  | • CloudWatch     | |
|  | • Secrets Mgr    |  | • Macie          |  | • EventBridge    | |
|  | • ACM            |  | • Config         |  | • Systems Mgr    | |
|  +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Threat Detection Services

### Amazon GuardDuty

Intelligent threat detection service that continuously monitors for malicious activity.

| Feature | Description |
|---------|-------------|
| Data Sources | VPC Flow Logs, CloudTrail, DNS logs |
| Detection Types | Reconnaissance, instance compromise, account compromise |
| ML-Based | Uses machine learning to identify anomalies |
| Integration | Sends findings to Security Hub, EventBridge |

**What GuardDuty Detects:**
- Unauthorized access attempts
- Cryptocurrency mining
- Compromised EC2 instances
- Data exfiltration attempts
- Malicious IP addresses

### Amazon Inspector

Automated vulnerability assessment service.

| Feature | Description |
|---------|-------------|
| Scope | EC2 instances, container images, Lambda functions |
| Assessment Types | Network reachability, software vulnerabilities |
| Automation | Continuous scanning |
| Output | Prioritized findings with remediation guidance |

### AWS Security Hub

Central security view and compliance checks.

| Feature | Description |
|---------|-------------|
| Aggregation | Collects findings from multiple services |
| Standards | CIS, PCI DSS, AWS Foundational Security |
| Automation | Automated compliance checks |
| Dashboard | Single pane of glass for security |

### Amazon Detective

Analyze and investigate security findings.

| Feature | Description |
|---------|-------------|
| Data Analysis | Automatically collects and analyzes log data |
| Visualization | Graph-based investigation |
| Integration | Works with GuardDuty and Security Hub |
| ML-Based | Uses machine learning for analysis |

## Network Security Services

### AWS WAF (Web Application Firewall)

Protects web applications from common exploits.

| Feature | Description |
|---------|-------------|
| Protection | SQL injection, XSS, common exploits |
| Integration | CloudFront, ALB, API Gateway |
| Rules | AWS Managed Rules, custom rules |
| Bot Control | Managed bot protection |

### AWS Shield

DDoS protection service.

| Tier | Protection | Cost |
|------|------------|------|
| Shield Standard | Layer 3/4 DDoS | Free (automatic) |
| Shield Advanced | Layer 3/4/7 DDoS, 24/7 support | Subscription |

**Shield Advanced Benefits:**
- Enhanced DDoS protection
- DDoS Response Team (DRT) access
- Cost protection for scaling
- Advanced metrics and reports

### AWS Network Firewall

Managed network firewall service for VPCs.

| Feature | Description |
|---------|-------------|
| Inspection | Stateful and stateless packet inspection |
| Rules | Custom rules, AWS Managed Rules |
| Deployment | Across Availability Zones |
| Logging | Flow logs, alert logs |

### AWS Firewall Manager

Centrally manage firewall rules across accounts.

| Feature | Description |
|---------|-------------|
| Scope | AWS Organizations-wide |
| Rules | WAF, Shield Advanced, Security Groups, Network Firewall |
| Automation | Automatic rule application |
| Compliance | Ensures consistent security posture |

## Data Protection Services

### AWS Secrets Manager

Securely store and rotate secrets.

| Feature | Description |
|---------|-------------|
| Storage | Database credentials, API keys, tokens |
| Rotation | Automatic secret rotation |
| Encryption | KMS encryption |
| Access | IAM-based access control |

### AWS Certificate Manager (ACM)

Provision and manage SSL/TLS certificates.

| Feature | Description |
|---------|-------------|
| Certificates | Public and private certificates |
| Renewal | Automatic renewal |
| Integration | CloudFront, ELB, API Gateway |
| Cost | Public certificates are free |

### Amazon Macie

Discover and protect sensitive data.

| Feature | Description |
|---------|-------------|
| Discovery | Automatically finds sensitive data in S3 |
| Classification | PII, financial data, credentials |
| Alerts | Generates findings for sensitive data |
| Compliance | Helps with GDPR, HIPAA, etc. |

## Security Service Comparison

| Service | Primary Function | Use Case |
|---------|-----------------|----------|
| GuardDuty | Threat detection | Identify security threats |
| Inspector | Vulnerability scanning | Find software vulnerabilities |
| Security Hub | Centralized view | Aggregate security findings |
| Detective | Investigation | Analyze security incidents |
| WAF | Web app protection | Block web attacks |
| Shield | DDoS protection | Protect against DDoS |
| Macie | Data discovery | Find sensitive data |

## 🎯 Exam Tips

- **GuardDuty** = threat detection (uses ML, monitors logs)
- **Inspector** = vulnerability assessment (EC2, containers, Lambda)
- **Security Hub** = central dashboard for security findings
- **WAF** = web application firewall (blocks SQL injection, XSS)
- **Shield Standard** = free DDoS protection
- **Shield Advanced** = paid, enhanced DDoS protection with support
- **Macie** = discovers sensitive data in S3
- **Secrets Manager** = stores and rotates credentials

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| GuardDuty | ML-based threat detection service |
| Inspector | Vulnerability assessment service |
| Security Hub | Centralized security findings dashboard |
| WAF | Web Application Firewall |
| Shield | DDoS protection service |
| Macie | Sensitive data discovery service |
| Detective | Security investigation service |
| ACM | AWS Certificate Manager |

## 💡 Key Takeaways

1. GuardDuty provides continuous threat detection using machine learning
2. Inspector scans for vulnerabilities in EC2, containers, and Lambda
3. Security Hub aggregates findings from multiple security services
4. WAF protects web applications from common attacks
5. Shield Standard is free; Shield Advanced provides enhanced DDoS protection
6. Macie automatically discovers sensitive data in S3 buckets
7. Secrets Manager securely stores and rotates credentials

---

*Next: [06 - Governance and Auditing Services](../06-governance-and-auditing-services/readme.md)*

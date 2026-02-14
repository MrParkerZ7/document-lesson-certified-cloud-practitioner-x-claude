# 👤 Customer Responsibilities - Security IN the Cloud

## File Structure

```
lesson-05-aws-shared-responsibility-model/
└── 03-customer-responsibilities/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Overview

Customers are responsible for **"Security IN the Cloud"** - this encompasses everything that customers deploy, configure, and manage within AWS. The customer maintains complete control over their security configuration and must implement appropriate security measures.

## Customer Responsibility Categories

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     CUSTOMER RESPONSIBILITY LAYERS                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  DATA SECURITY                                                        │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐     │  │
│  │  │ Data Class- │ │ Encryption  │ │  Backup &   │ │   Data      │     │  │
│  │  │ ification   │ │ (Rest/Trans)│ │  Recovery   │ │   Privacy   │     │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  IDENTITY & ACCESS MANAGEMENT (IAM)                                   │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐     │  │
│  │  │  Users &    │ │   Roles &   │ │   MFA       │ │  Password   │     │  │
│  │  │   Groups    │ │  Policies   │ │  Setup      │ │   Policies  │     │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  APPLICATION SECURITY                                                 │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐     │  │
│  │  │  Secure     │ │   Input     │ │ Application │ │  API        │     │  │
│  │  │   Code      │ │ Validation  │ │   Auth      │ │  Security   │     │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  OPERATING SYSTEM & NETWORK                                           │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐     │  │
│  │  │  OS         │ │  Security   │ │   Network   │ │    VPC      │     │  │
│  │  │  Patching   │ │   Groups    │ │    ACLs     │ │   Config    │     │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

## 1. Data Protection

Data protection is **always** the customer's responsibility, regardless of which AWS service is used.

### Data Classification

| Classification Level | Description | Examples |
|---------------------|-------------|----------|
| **Public** | Can be shared openly | Marketing materials, public APIs |
| **Internal** | For organizational use | Internal docs, employee data |
| **Confidential** | Restricted access | Financial data, customer PII |
| **Highly Confidential** | Strictest controls | Trade secrets, credentials |

### Encryption Responsibilities

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENCRYPTION RESPONSIBILITIES                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ENCRYPTION AT REST                 ENCRYPTION IN TRANSIT       │
│  ┌─────────────────────────┐       ┌─────────────────────────┐ │
│  │ Customer Decides:       │       │ Customer Configures:     │ │
│  │ • Enable encryption     │       │ • TLS/SSL certificates   │ │
│  │ • KMS key management    │       │ • HTTPS endpoints        │ │
│  │ • Key rotation policy   │       │ • VPN connections        │ │
│  │ • Access to keys        │       │ • Private connectivity   │ │
│  └─────────────────────────┘       └─────────────────────────┘ │
│                                                                 │
│  AWS PROVIDES THE TOOLS:                                        │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • AWS KMS (Key Management Service)                       │   │
│  │ • AWS CloudHSM (Hardware Security Module)                │   │
│  │ • AWS Certificate Manager (ACM)                          │   │
│  │ • S3 Server-Side Encryption options                      │   │
│  │ • EBS encryption                                         │   │
│  │ • RDS encryption                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  CUSTOMER MUST:                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ Enable encryption on resources                        │   │
│  │ ✓ Manage key policies                                   │   │
│  │ ✓ Rotate keys appropriately                             │   │
│  │ ✓ Control key access                                    │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Data Backup and Recovery

| Responsibility | Customer Actions |
|---------------|------------------|
| **Backup Strategy** | Define RPO/RTO requirements |
| **Backup Implementation** | Configure automated backups |
| **Backup Testing** | Regularly test restoration |
| **Disaster Recovery** | Design and implement DR plans |
| **Data Retention** | Define and enforce retention policies |

## 2. Identity and Access Management (IAM)

IAM is a critical customer responsibility - controlling who can access what in your AWS environment.

### IAM Best Practices

```
┌─────────────────────────────────────────────────────────────────┐
│                     IAM BEST PRACTICES                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. ROOT ACCOUNT PROTECTION                                     │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ Enable MFA on root account                            │   │
│  │ ✓ Never use root for daily tasks                        │   │
│  │ ✓ Store root credentials securely                       │   │
│  │ ✓ Delete root access keys                               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  2. LEAST PRIVILEGE PRINCIPLE                                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ Grant minimum permissions needed                      │   │
│  │ ✓ Use IAM policies to restrict access                   │   │
│  │ ✓ Regularly review and revoke unused permissions        │   │
│  │ ✓ Use permission boundaries                             │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  3. USE IAM ROLES                                               │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ Use roles for applications (not access keys)          │   │
│  │ ✓ Use roles for cross-account access                    │   │
│  │ ✓ Use roles for EC2 instances                           │   │
│  │ ✓ Use roles for Lambda functions                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  4. ENABLE MFA                                                  │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ Require MFA for all users                             │   │
│  │ ✓ Use hardware MFA for privileged accounts              │   │
│  │ ✓ Enable MFA delete on S3 buckets                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  5. STRONG PASSWORD POLICY                                      │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ Minimum length (14+ characters)                       │   │
│  │ ✓ Require uppercase, lowercase, numbers, symbols        │   │
│  │ ✓ Enable password expiration                            │   │
│  │ ✓ Prevent password reuse                                │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### IAM Components Customer Manages

| Component | Customer Responsibility |
|-----------|------------------------|
| **IAM Users** | Create, manage, delete users |
| **IAM Groups** | Organize users, apply group policies |
| **IAM Roles** | Define roles, trust policies |
| **IAM Policies** | Write and attach permission policies |
| **Access Keys** | Rotate, manage, secure access keys |
| **MFA Devices** | Enable and manage MFA |
| **Password Policy** | Configure account password policy |

## 3. Application Security

Customers are fully responsible for the security of applications they deploy.

### Application Security Checklist

```
┌─────────────────────────────────────────────────────────────────┐
│                   APPLICATION SECURITY                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SECURE DEVELOPMENT                                             │
│  ├─ Follow OWASP guidelines                                     │
│  ├─ Implement input validation                                  │
│  ├─ Use parameterized queries (prevent SQL injection)           │
│  ├─ Sanitize outputs (prevent XSS)                              │
│  ├─ Implement proper error handling                             │
│  └─ Conduct code reviews                                        │
│                                                                 │
│  AUTHENTICATION & AUTHORIZATION                                 │
│  ├─ Implement strong authentication                             │
│  ├─ Use AWS Cognito or external IdP                             │
│  ├─ Implement session management                                │
│  ├─ Apply role-based access control                             │
│  └─ Use OAuth/OIDC for API access                               │
│                                                                 │
│  API SECURITY                                                   │
│  ├─ Use API Gateway for management                              │
│  ├─ Implement rate limiting                                     │
│  ├─ Use API keys and usage plans                                │
│  ├─ Enable request/response validation                          │
│  └─ Use WAF for protection                                      │
│                                                                 │
│  SECRETS MANAGEMENT                                             │
│  ├─ Use AWS Secrets Manager                                     │
│  ├─ Never hardcode credentials                                  │
│  ├─ Rotate secrets regularly                                    │
│  └─ Use environment variables                                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Application Logging and Monitoring

| Component | Customer Configures |
|-----------|-------------------|
| **CloudWatch Logs** | Application logging, log retention |
| **CloudWatch Alarms** | Threshold alerts, notifications |
| **X-Ray** | Application tracing and debugging |
| **CloudTrail** | API audit logging |

## 4. Operating System Security

For IaaS services like EC2, customers manage the guest operating system.

### OS Patching and Updates

```
┌─────────────────────────────────────────────────────────────────┐
│                    OS PATCHING WORKFLOW                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│    ┌─────────────┐     ┌─────────────┐     ┌─────────────┐     │
│    │  Identify   │────▶│   Test      │────▶│   Deploy    │     │
│    │   Patches   │     │   Patches   │     │   Patches   │     │
│    └─────────────┘     └─────────────┘     └─────────────┘     │
│          │                   │                   │              │
│          ▼                   ▼                   ▼              │
│    ┌─────────────┐     ┌─────────────┐     ┌─────────────┐     │
│    │  Security   │     │  Staging    │     │  Production │     │
│    │  Bulletins  │     │  Environment│     │  Environment│     │
│    └─────────────┘     └─────────────┘     └─────────────┘     │
│                                                                 │
│  AWS TOOLS TO HELP:                                             │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • AWS Systems Manager Patch Manager                      │   │
│  │ • Amazon Inspector (vulnerability scanning)              │   │
│  │ • AWS Config (compliance checking)                       │   │
│  │ • Amazon EventBridge (scheduling)                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  CUSTOMER RESPONSIBILITIES:                                     │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ ✓ Define patching schedule                               │   │
│  │ ✓ Test patches before deployment                         │   │
│  │ ✓ Apply security patches promptly                        │   │
│  │ ✓ Maintain patching documentation                        │   │
│  │ ✓ Handle patch failures                                  │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### OS Hardening

| Hardening Task | Description |
|---------------|-------------|
| **Disable unused services** | Reduce attack surface |
| **Remove unnecessary software** | Minimize vulnerabilities |
| **Configure local firewall** | OS-level firewall rules |
| **Enable audit logging** | Track system changes |
| **Apply security baselines** | CIS Benchmarks, STIG |
| **Antivirus/Antimalware** | Install and maintain |

## 5. Network Security Configuration

Customers configure and manage network security controls.

### Security Groups vs NACLs

```
┌─────────────────────────────────────────────────────────────────┐
│              SECURITY GROUPS vs NETWORK ACLs                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SECURITY GROUPS (Instance Level)    NETWORK ACLs (Subnet Level)│
│  ┌─────────────────────────────┐    ┌─────────────────────────┐ │
│  │ • Stateful                  │    │ • Stateless             │ │
│  │ • Allow rules only          │    │ • Allow AND deny rules  │ │
│  │ • Applies to instance       │    │ • Applies to subnet     │ │
│  │ • Return traffic automatic  │    │ • Return traffic explicit│ │
│  │ • Evaluates all rules       │    │ • Evaluates in order    │ │
│  └─────────────────────────────┘    └─────────────────────────┘ │
│                                                                 │
│  CUSTOMER CONFIGURES BOTH:                                      │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Security Groups:                                         │   │
│  │ • Define inbound/outbound rules                          │   │
│  │ • Specify allowed protocols, ports, sources              │   │
│  │ • Reference other security groups                        │   │
│  │                                                          │   │
│  │ Network ACLs:                                            │   │
│  │ • Define numbered rules                                  │   │
│  │ • Specify allow/deny actions                             │   │
│  │ • Configure for inbound AND outbound                     │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### VPC Security Configuration

| Component | Customer Responsibility |
|-----------|------------------------|
| **Subnets** | Public vs private placement |
| **Route Tables** | Traffic routing decisions |
| **Internet Gateway** | Expose resources appropriately |
| **NAT Gateway** | Private subnet internet access |
| **VPC Endpoints** | Private AWS service access |
| **VPC Peering** | Cross-VPC connectivity |
| **Transit Gateway** | Network architecture |
| **VPN/Direct Connect** | Hybrid connectivity security |

## Customer Security Tools

AWS provides tools to help customers fulfill their responsibilities:

```
┌─────────────────────────────────────────────────────────────────┐
│                   AWS SECURITY TOOLS                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  IDENTITY & ACCESS              DETECTION & MONITORING          │
│  ┌─────────────────────┐       ┌─────────────────────┐         │
│  │ • IAM                │       │ • CloudWatch        │         │
│  │ • IAM Identity Center│       │ • CloudTrail        │         │
│  │ • Cognito            │       │ • GuardDuty         │         │
│  │ • Directory Service  │       │ • Security Hub      │         │
│  └─────────────────────┘       │ • Detective         │         │
│                                └─────────────────────┘         │
│  NETWORK SECURITY                                               │
│  ┌─────────────────────┐       DATA PROTECTION                 │
│  │ • Security Groups   │       ┌─────────────────────┐         │
│  │ • NACLs             │       │ • KMS               │         │
│  │ • WAF               │       │ • CloudHSM          │         │
│  │ • Shield            │       │ • Macie             │         │
│  │ • Network Firewall  │       │ • Secrets Manager   │         │
│  └─────────────────────┘       └─────────────────────┘         │
│                                                                 │
│  COMPLIANCE & GOVERNANCE        VULNERABILITY MANAGEMENT        │
│  ┌─────────────────────┐       ┌─────────────────────┐         │
│  │ • AWS Config        │       │ • Inspector         │         │
│  │ • Audit Manager     │       │ • Systems Manager   │         │
│  │ • Organizations     │       │ • Patch Manager     │         │
│  │ • Control Tower     │       │                     │         │
│  └─────────────────────┘       └─────────────────────┘         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 🎯 Exam Tips

> **Tip 1**: Data encryption and classification is ALWAYS customer responsibility - even in managed services

> **Tip 2**: IAM configuration (users, groups, roles, policies) is 100% customer responsibility

> **Tip 3**: For EC2, the customer patches the guest OS; for RDS, AWS patches the database engine

> **Tip 4**: Security Groups and NACLs are customer-configured network security controls

> **Tip 5**: AWS provides security TOOLS, but customers must USE and CONFIGURE them

> **Tip 6**: Application security (code, authentication, API security) is customer responsibility

## Key Exam Scenarios

### Scenario 1: S3 Bucket Breach
**Question**: Customer data is exposed due to a public S3 bucket. Who is responsible?
**Answer**: **Customer** - Bucket permissions and access controls are customer responsibility

### Scenario 2: EC2 Instance Compromised
**Question**: An EC2 instance is hacked due to an unpatched OS vulnerability. Who is responsible?
**Answer**: **Customer** - Guest OS patching is customer responsibility

### Scenario 3: Weak Passwords
**Question**: A user account is compromised due to weak password. Who is responsible?
**Answer**: **Customer** - Password policies and IAM configuration are customer responsibility

### Scenario 4: SQL Injection Attack
**Question**: An application is compromised via SQL injection. Who is responsible?
**Answer**: **Customer** - Application code security is customer responsibility

### Scenario 5: Missing MFA
**Question**: Root account compromised because MFA wasn't enabled. Who is responsible?
**Answer**: **Customer** - MFA configuration is customer responsibility

## 💡 Key Takeaways

1. **Data is ALWAYS customer responsibility** - classification, encryption, backup
2. **IAM is ALWAYS customer responsibility** - users, roles, policies, MFA
3. **Application security is customer responsibility** - code, authentication, APIs
4. **Guest OS patching is customer responsibility** - for EC2 and similar IaaS
5. **Network configuration is customer responsibility** - Security Groups, NACLs, VPC
6. **AWS provides tools** - but customers must enable and configure them
7. **Customer retains control and ownership** - more control = more responsibility

## Quick Reference

```
╔═══════════════════════════════════════════════════════════════╗
║             CUSTOMER RESPONSIBILITIES SUMMARY                  ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║  ALWAYS CUSTOMER RESPONSIBILITY:                              ║
║  ├─ Customer data (encryption, backup, classification)        ║
║  ├─ IAM (users, groups, roles, policies, MFA)                 ║
║  ├─ Application code and security                             ║
║  ├─ Security Groups and NACLs                                 ║
║  ├─ Client-side encryption                                    ║
║  └─ Data in transit encryption                                ║
║                                                               ║
║  FOR IaaS (EC2), ALSO:                                        ║
║  ├─ Guest operating system                                    ║
║  ├─ OS patching and updates                                   ║
║  ├─ Antivirus/antimalware                                     ║
║  └─ Host-based firewall                                       ║
║                                                               ║
║  KEY TOOLS TO USE:                                            ║
║  ├─ IAM for access control                                    ║
║  ├─ KMS for encryption                                        ║
║  ├─ CloudTrail for auditing                                   ║
║  ├─ GuardDuty for threat detection                            ║
║  └─ Inspector for vulnerability scanning                      ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

## Next Steps

Continue to the next section to learn about **Shared Responsibilities** - areas where both AWS and customers have security responsibilities.

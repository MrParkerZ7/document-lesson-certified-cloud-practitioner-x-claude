# Shared Responsibilities - Areas of Joint Accountability

## Overview

While the Shared Responsibility Model clearly divides most responsibilities between AWS and customers, there are certain areas where **both parties share accountability**. These areas require cooperation and complementary efforts from AWS and customers to achieve complete security.

## Shared Responsibility Areas

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      SHARED RESPONSIBILITY AREAS                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│                        ┌─────────────────────────┐                          │
│                        │   PATCH MANAGEMENT      │                          │
│                        └─────────────────────────┘                          │
│                     AWS patches │ Customer patches                          │
│                     infrastructure │ their systems                          │
│                                                                             │
│                        ┌─────────────────────────┐                          │
│                        │ CONFIGURATION MGMT      │                          │
│                        └─────────────────────────┘                          │
│                     AWS configures │ Customer configures                    │
│                     infrastructure │ their resources                        │
│                                                                             │
│                        ┌─────────────────────────┐                          │
│                        │ AWARENESS & TRAINING    │                          │
│                        └─────────────────────────┘                          │
│                     AWS trains │ Customer trains                            │
│                     AWS staff │ their staff                                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

## 1. Patch Management

Patch management is a critical shared responsibility where both AWS and customers must maintain their respective systems.

### Patch Management Division

```
┌─────────────────────────────────────────────────────────────────┐
│                    PATCH MANAGEMENT                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────────────┐  ┌──────────────────────────┐    │
│  │     AWS PATCHES          │  │   CUSTOMER PATCHES       │    │
│  ├──────────────────────────┤  ├──────────────────────────┤    │
│  │ • Hypervisor updates     │  │ • EC2 Guest OS patches   │    │
│  │ • Host OS patches        │  │ • Application patches    │    │
│  │ • Infrastructure firmware│  │ • Container images       │    │
│  │ • Network equipment      │  │ • AMI updates            │    │
│  │ • RDS DB engine patches  │  │ • Database on EC2        │    │
│  │ • Lambda runtime updates │  │ • Lambda custom runtimes │    │
│  │ • EKS control plane      │  │ • EKS worker nodes       │    │
│  │ • Managed service engines│  │ • Self-managed services  │    │
│  └──────────────────────────┘  └──────────────────────────┘    │
│                                                                 │
│                     VARIES BY SERVICE                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                                                          │   │
│  │  EC2 (IaaS):  AWS patches host → Customer patches guest │   │
│  │  RDS (PaaS):  AWS patches DB engine → Customer patches  │   │
│  │               data/schema                                │   │
│  │  Lambda:      AWS patches runtime → Customer patches    │   │
│  │               function code                              │   │
│  │  S3 (SaaS):   AWS handles all infrastructure patching   │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Patching Scenarios by Service Type

| Service | AWS Patches | Customer Patches |
|---------|------------|------------------|
| **EC2** | Hypervisor, host OS, hardware firmware | Guest OS, applications, middleware |
| **RDS** | Database engine, underlying OS | Nothing (but must schedule maintenance) |
| **Lambda** | Runtime environment, execution environment | Function code, dependencies |
| **EKS** | Control plane, managed add-ons | Worker nodes, custom add-ons |
| **ECS on EC2** | ECS agent updates | EC2 instances, container images |
| **ECS Fargate** | Underlying infrastructure | Container images |
| **ElasticBeanstalk** | Platform updates (if managed) | Application code |

### Customer Patching Best Practices

```
┌─────────────────────────────────────────────────────────────────┐
│              CUSTOMER PATCHING BEST PRACTICES                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. ESTABLISH PATCHING SCHEDULE                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Define maintenance windows                             │   │
│  │ • Prioritize critical security patches                   │   │
│  │ • Balance security vs. availability                      │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  2. TEST BEFORE DEPLOYING                                       │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Test patches in staging environment                    │   │
│  │ • Verify application compatibility                       │   │
│  │ • Plan rollback procedures                               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  3. AUTOMATE WHERE POSSIBLE                                     │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Use AWS Systems Manager Patch Manager                  │   │
│  │ • Implement CI/CD for container image updates            │   │
│  │ • Use Auto Scaling for rolling deployments               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  4. DOCUMENT AND AUDIT                                          │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Track patching status                                  │   │
│  │ • Maintain compliance reports                            │   │
│  │ • Use AWS Config for compliance monitoring               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 2. Configuration Management

Both AWS and customers have configuration management responsibilities.

### Configuration Management Division

```
┌─────────────────────────────────────────────────────────────────┐
│                 CONFIGURATION MANAGEMENT                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────────────┐  ┌──────────────────────────┐    │
│  │   AWS CONFIGURES         │  │  CUSTOMER CONFIGURES     │    │
│  ├──────────────────────────┤  ├──────────────────────────┤    │
│  │ • Infrastructure defaults│  │ • Security Groups        │    │
│  │ • Service configurations │  │ • NACLs                  │    │
│  │ • Default security       │  │ • IAM policies           │    │
│  │ • Service limits         │  │ • Encryption settings    │    │
│  │ • API endpoints          │  │ • Logging configuration  │    │
│  │ • Region setup           │  │ • VPC design             │    │
│  │ • Availability zones     │  │ • Resource settings      │    │
│  │ • Network backbone       │  │ • Application config     │    │
│  └──────────────────────────┘  └──────────────────────────┘    │
│                                                                 │
│                                                                 │
│  AWS PROVIDES:                  CUSTOMER MUST:                  │
│  ┌──────────────────────────┐  ┌──────────────────────────┐    │
│  │ • Secure default configs │  │ • Review defaults        │    │
│  │ • Configuration options  │  │ • Customize settings     │    │
│  │ • Best practice guides   │  │ • Follow best practices  │    │
│  │ • Compliance frameworks  │  │ • Maintain compliance    │    │
│  │ • Config validation      │  │ • Monitor drift          │    │
│  └──────────────────────────┘  └──────────────────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Configuration Management Tools

| Tool | Purpose | Owner |
|------|---------|-------|
| **AWS Config** | Track resource configurations | Customer enables & configures |
| **AWS Config Rules** | Compliance checking | Customer defines rules |
| **CloudFormation** | Infrastructure as Code | Customer creates templates |
| **Systems Manager** | Instance configuration | Customer configures |
| **Service Control Policies** | Org-wide guardrails | Customer creates policies |

### Configuration Drift Prevention

```
┌─────────────────────────────────────────────────────────────────┐
│              PREVENTING CONFIGURATION DRIFT                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐       │
│    │   Define    │───▶│   Deploy    │───▶│  Monitor    │       │
│    │   Baseline  │    │    IaC      │    │   Drift     │       │
│    └─────────────┘    └─────────────┘    └─────────────┘       │
│          │                                      │               │
│          │         ┌─────────────┐              │               │
│          └────────▶│  Remediate  │◀─────────────┘               │
│                    │   Changes   │                              │
│                    └─────────────┘                              │
│                                                                 │
│  TOOLS FOR CONFIGURATION MANAGEMENT:                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • AWS Config - Detect configuration changes             │   │
│  │ • CloudFormation Drift Detection                        │   │
│  │ • AWS Systems Manager State Manager                     │   │
│  │ • AWS Control Tower - Guardrails                        │   │
│  │ • AWS Organizations - SCPs                              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 3. Awareness and Training

Security awareness is a shared responsibility that requires both parties to educate their respective personnel.

### Training Responsibilities

```
┌─────────────────────────────────────────────────────────────────┐
│                   AWARENESS & TRAINING                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────────────┐  ┌──────────────────────────┐    │
│  │   AWS TRAINS             │  │  CUSTOMER TRAINS         │    │
│  ├──────────────────────────┤  ├──────────────────────────┤    │
│  │ • AWS employees on       │  │ • Employees on AWS       │    │
│  │   security protocols     │  │   security best practices│    │
│  │ • Data center staff      │  │ • Developers on secure   │    │
│  │ • Support engineers      │  │   coding practices       │    │
│  │ • Service teams          │  │ • Ops teams on security  │    │
│  │                          │  │   tools                  │    │
│  │                          │  │ • End users on security  │    │
│  │                          │  │   policies               │    │
│  └──────────────────────────┘  └──────────────────────────┘    │
│                                                                 │
│  AWS PROVIDES TRAINING RESOURCES:                               │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • AWS Training and Certification                         │   │
│  │ • Security Learning Path                                 │   │
│  │ • AWS Well-Architected Training                          │   │
│  │ • AWS Security Best Practices whitepapers               │   │
│  │ • AWS re:Invent security sessions                        │   │
│  │ • AWS Skill Builder                                      │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  CUSTOMER IMPLEMENTS:                                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Security awareness programs                            │   │
│  │ • Phishing simulation exercises                          │   │
│  │ • Incident response training                             │   │
│  │ • Compliance training requirements                       │   │
│  │ • Role-based security training                           │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Security Awareness Topics

| Topic | AWS Responsibility | Customer Responsibility |
|-------|-------------------|------------------------|
| **Physical Security** | Train data center staff | Not applicable |
| **Social Engineering** | Train AWS employees | Train customer employees |
| **Secure Development** | Train service teams | Train developers |
| **Incident Response** | Train support teams | Train security teams |
| **Compliance** | Train for AWS compliance | Train for customer compliance |

## Additional Shared Areas

### Encryption

```
┌─────────────────────────────────────────────────────────────────┐
│                      ENCRYPTION (Shared)                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  AWS PROVIDES:                  CUSTOMER MANAGES:               │
│  ┌──────────────────────────┐  ┌──────────────────────────┐    │
│  │ • KMS infrastructure     │  │ • Key policies           │    │
│  │ • HSM hardware (CloudHSM)│  │ • Key rotation           │    │
│  │ • Encryption algorithms  │  │ • Who can use keys       │    │
│  │ • TLS for AWS endpoints  │  │ • Enabling encryption    │    │
│  │ • S3 encryption options  │  │ • Client-side encryption │    │
│  │ • EBS encryption feature │  │ • Certificate management │    │
│  └──────────────────────────┘  └──────────────────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Logging and Monitoring

```
┌─────────────────────────────────────────────────────────────────┐
│                 LOGGING & MONITORING (Shared)                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  AWS PROVIDES:                  CUSTOMER CONFIGURES:            │
│  ┌──────────────────────────┐  ┌──────────────────────────┐    │
│  │ • CloudWatch service     │  │ • What to log            │    │
│  │ • CloudTrail service     │  │ • Log retention periods  │    │
│  │ • VPC Flow Logs feature  │  │ • Alarms and alerts      │    │
│  │ • Access logging options │  │ • Dashboards             │    │
│  │ • GuardDuty service      │  │ • Response procedures    │    │
│  │ • Security Hub service   │  │ • Integration with SIEM  │    │
│  └──────────────────────────┘  └──────────────────────────┘    │
│                                                                 │
│  AWS logs their internal operations (available via artifacts)   │
│  Customers log their resource activities (they must enable it)  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Incident Response

```
┌─────────────────────────────────────────────────────────────────┐
│                  INCIDENT RESPONSE (Shared)                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  AWS HANDLES:                   CUSTOMER HANDLES:               │
│  ┌──────────────────────────┐  ┌──────────────────────────┐    │
│  │ • Infrastructure attacks │  │ • Application attacks    │    │
│  │ • Service availability   │  │ • Data breaches          │    │
│  │ • DDoS at infra level    │  │ • Account compromises    │    │
│  │ • Physical security      │  │ • Configuration issues   │    │
│  │   incidents              │  │ • Application-level DDoS │    │
│  │ • Notify via Health      │  │ • Forensics on instances │    │
│  │   Dashboard              │  │ • Incident documentation │    │
│  └──────────────────────────┘  └──────────────────────────┘    │
│                                                                 │
│  COMMUNICATION:                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • AWS notifies customers of infrastructure issues       │   │
│  │ • Customers notify AWS if they suspect AWS-side issues  │   │
│  │ • AWS Support available for incident assistance         │   │
│  │ • AWS provides forensic data upon legal request         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## The Collaboration Model

```
┌─────────────────────────────────────────────────────────────────┐
│                  AWS + CUSTOMER COLLABORATION                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│        ┌─────────────────┐     ┌─────────────────┐             │
│        │       AWS       │     │    CUSTOMER     │             │
│        │                 │     │                 │             │
│        │  Infrastructure │     │  Applications   │             │
│        │     Security    │     │     Security    │             │
│        │                 │     │                 │             │
│        └────────┬────────┘     └────────┬────────┘             │
│                 │                       │                       │
│                 ▼                       ▼                       │
│        ┌─────────────────────────────────────────┐             │
│        │          SHARED RESPONSIBILITIES        │             │
│        │                                         │             │
│        │    ┌─────────────────────────────┐     │             │
│        │    │    Patch Management         │     │             │
│        │    └─────────────────────────────┘     │             │
│        │    ┌─────────────────────────────┐     │             │
│        │    │  Configuration Management   │     │             │
│        │    └─────────────────────────────┘     │             │
│        │    ┌─────────────────────────────┐     │             │
│        │    │   Awareness & Training      │     │             │
│        │    └─────────────────────────────┘     │             │
│        │    ┌─────────────────────────────┐     │             │
│        │    │       Encryption            │     │             │
│        │    └─────────────────────────────┘     │             │
│        │    ┌─────────────────────────────┐     │             │
│        │    │   Logging & Monitoring      │     │             │
│        │    └─────────────────────────────┘     │             │
│        │    ┌─────────────────────────────┐     │             │
│        │    │    Incident Response        │     │             │
│        │    └─────────────────────────────┘     │             │
│        │                                         │             │
│        └─────────────────────────────────────────┘             │
│                         │                                       │
│                         ▼                                       │
│               ┌─────────────────┐                              │
│               │ COMPLETE        │                              │
│               │ SECURITY        │                              │
│               │ POSTURE         │                              │
│               └─────────────────┘                              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Exam Tips

> **Tip 1**: Patch management is shared - AWS patches infrastructure, customer patches their systems

> **Tip 2**: Configuration management is shared - AWS provides options, customer makes choices

> **Tip 3**: Training is shared - AWS trains their staff, customer trains their staff

> **Tip 4**: AWS provides security TOOLS and FEATURES, customers must ENABLE and CONFIGURE them

> **Tip 5**: For RDS, AWS patches the database engine but customer chooses the maintenance window

> **Tip 6**: Logging services exist but customer must enable and configure what to log

## Key Exam Scenarios

### Scenario 1: RDS Patching
**Question**: Who is responsible for patching the RDS database engine?
**Answer**: **AWS** patches the engine, but **Customer** must define maintenance windows

### Scenario 2: Security Group Configuration
**Question**: AWS provides Security Groups. Who configures the rules?
**Answer**: **Customer** - AWS provides the feature, customer configures the rules

### Scenario 3: CloudTrail Logging
**Question**: Who enables CloudTrail for API logging?
**Answer**: **Customer** - AWS provides CloudTrail, customer enables and configures it

### Scenario 4: Employee Security Training
**Question**: Who trains customer developers on AWS security best practices?
**Answer**: **Customer** (AWS provides training resources, customer implements training programs)

## Key Takeaways

1. **Patch management is shared** - AWS patches infrastructure, customers patch their systems
2. **Configuration is shared** - AWS provides options, customers make configuration choices
3. **Training is shared** - Both parties train their respective personnel
4. **AWS provides tools** - Customers must enable, configure, and use them
5. **Encryption is shared** - AWS provides mechanisms, customers manage keys and enable encryption
6. **Logging is shared** - AWS provides services, customers configure what to log
7. **Incident response is shared** - Both parties handle incidents in their domains

## Quick Reference

```
╔═══════════════════════════════════════════════════════════════╗
║              SHARED RESPONSIBILITIES SUMMARY                   ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║  PATCH MANAGEMENT:                                            ║
║  ├─ AWS: Infrastructure, hypervisor, managed service engines  ║
║  └─ Customer: Guest OS, applications, container images        ║
║                                                               ║
║  CONFIGURATION MANAGEMENT:                                    ║
║  ├─ AWS: Service defaults, infrastructure config              ║
║  └─ Customer: Security Groups, NACLs, IAM, encryption        ║
║                                                               ║
║  AWARENESS & TRAINING:                                        ║
║  ├─ AWS: Train AWS employees on security                      ║
║  └─ Customer: Train customer employees on security            ║
║                                                               ║
║  ENCRYPTION:                                                  ║
║  ├─ AWS: Provide KMS, HSM, encryption features                ║
║  └─ Customer: Enable encryption, manage keys                  ║
║                                                               ║
║  LOGGING & MONITORING:                                        ║
║  ├─ AWS: Provide CloudWatch, CloudTrail, GuardDuty            ║
║  └─ Customer: Enable logging, configure alerts                ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

## Next Steps

Continue to the next section to learn about **Responsibility Shifts by Service Type** - understanding how responsibilities change between IaaS, PaaS, and SaaS services.

# Responsibility Shifts by Service Type

## Overview

One of the most important concepts in the AWS Shared Responsibility Model is understanding how security responsibilities **shift** based on the type of service used. As you move from Infrastructure as a Service (IaaS) to Platform as a Service (PaaS) to Software as a Service (SaaS), AWS assumes more responsibility and customers have less to manage.

## The Service Model Spectrum

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    RESPONSIBILITY SPECTRUM BY SERVICE TYPE                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   CUSTOMER RESPONSIBILITY ──────────────────────────────────────────────▶   │
│   ◀────────────────────────────────────────────── MORE ──────── LESS ────   │
│                                                                             │
│   ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐         │
│   │                  │  │                  │  │                  │         │
│   │       IaaS       │  │       PaaS       │  │       SaaS       │         │
│   │                  │  │                  │  │                  │         │
│   │   Infrastructure │  │     Platform     │  │     Software     │         │
│   │    as a Service  │  │    as a Service  │  │    as a Service  │         │
│   │                  │  │                  │  │                  │         │
│   │    Examples:     │  │    Examples:     │  │    Examples:     │         │
│   │    • EC2         │  │    • RDS         │  │    • S3          │         │
│   │    • EBS         │  │    • Lambda      │  │    • DynamoDB    │         │
│   │                  │  │    • Elastic     │  │    • SQS/SNS     │         │
│   │                  │  │      Beanstalk   │  │    • Rekognition │         │
│   │                  │  │    • Aurora      │  │                  │         │
│   └──────────────────┘  └──────────────────┘  └──────────────────┘         │
│                                                                             │
│   ◀──────────────────────────────────────────────────── AWS RESPONSIBILITY │
│   ──────── LESS ──────── MORE ────────────────────────────────────────────▶ │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

## Detailed Service Type Comparison

### Responsibility Matrix by Service Type

| Responsibility Layer | IaaS (EC2) | PaaS (RDS/Lambda) | SaaS (S3/DynamoDB) |
|---------------------|------------|-------------------|-------------------|
| **Customer Data** | Customer | Customer | Customer |
| **Data Encryption** | Customer | Customer | Customer |
| **Network Traffic Protection** | Customer | Customer | Customer |
| **Firewall Configuration** | Customer | Customer | Customer |
| **Application Code** | Customer | Customer | N/A |
| **Identity & Access** | Customer | Customer | Customer |
| **Operating System** | Customer | **AWS** | **AWS** |
| **Network Configuration** | Customer | Shared | **AWS** |
| **Platform/Engine** | Customer | **AWS** | **AWS** |
| **Compute** | **AWS** | **AWS** | **AWS** |
| **Storage** | **AWS** | **AWS** | **AWS** |
| **Physical Infrastructure** | **AWS** | **AWS** | **AWS** |

## 1. IaaS - Infrastructure as a Service (EC2)

With IaaS, customers have the **most responsibility** because they control the entire software stack above the virtualization layer.

### EC2 Responsibility Model

```
┌─────────────────────────────────────────────────────────────────┐
│                    EC2 (IaaS) RESPONSIBILITIES                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                 CUSTOMER MANAGES                         │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Customer Data                        │   │
│  │  ├──────────────┤  Application Code                     │   │
│  │  ├──────────────┤  Runtime & Middleware                 │   │
│  │  ├──────────────┤  Operating System                     │   │
│  │  ├──────────────┤  Security Groups                      │   │
│  │  └──────────────┘  Network Configuration                │   │
│  │                                                          │   │
│  │  Customer must:                                          │   │
│  │  • Patch guest OS                                        │   │
│  │  • Install & update applications                         │   │
│  │  • Configure security groups                             │   │
│  │  • Manage user access                                    │   │
│  │  • Enable & configure encryption                         │   │
│  │  • Install antivirus/monitoring                          │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    AWS MANAGES                           │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Hypervisor (Nitro)                   │   │
│  │  ├──────────────┤  Host Operating System                │   │
│  │  ├──────────────┤  Physical Servers                     │   │
│  │  ├──────────────┤  Network Infrastructure               │   │
│  │  ├──────────────┤  Storage Infrastructure               │   │
│  │  └──────────────┘  Data Center Security                 │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### EC2 Customer Responsibilities Checklist

| Task | Frequency | Tools |
|------|-----------|-------|
| OS Patching | Weekly/Monthly | Systems Manager Patch Manager |
| Security Group Review | Ongoing | AWS Config |
| Access Key Rotation | 90 days | IAM |
| AMI Updates | Monthly | EC2 Image Builder |
| Vulnerability Scanning | Weekly | Amazon Inspector |
| Log Monitoring | Continuous | CloudWatch |
| Backup | Daily/Weekly | AWS Backup |

## 2. PaaS - Platform as a Service (RDS, Lambda)

With PaaS, AWS manages more of the stack, allowing customers to focus on their data and applications.

### RDS Responsibility Model

```
┌─────────────────────────────────────────────────────────────────┐
│                   RDS (PaaS) RESPONSIBILITIES                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                 CUSTOMER MANAGES                         │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Customer Data                        │   │
│  │  ├──────────────┤  Database Schema                      │   │
│  │  ├──────────────┤  Data Encryption (enable)             │   │
│  │  ├──────────────┤  Security Groups                      │   │
│  │  ├──────────────┤  IAM DB Authentication                │   │
│  │  └──────────────┘  Backup Retention (configure)         │   │
│  │                                                          │   │
│  │  Customer must:                                          │   │
│  │  • Design database schema                                │   │
│  │  • Enable encryption at rest                             │   │
│  │  • Configure security groups                             │   │
│  │  • Set maintenance windows                               │   │
│  │  • Configure backups                                     │   │
│  │  • Manage database users                                 │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    AWS MANAGES                           │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Database Engine Patching             │   │
│  │  ├──────────────┤  Operating System                     │   │
│  │  ├──────────────┤  High Availability (Multi-AZ)         │   │
│  │  ├──────────────┤  Automated Backups                    │   │
│  │  ├──────────────┤  Hardware & Infrastructure            │   │
│  │  └──────────────┘  Physical Security                    │   │
│  │                                                          │   │
│  │  AWS automatically:                                      │   │
│  │  • Patches database engine                               │   │
│  │  • Manages OS updates                                    │   │
│  │  • Handles failover                                      │   │
│  │  • Performs automated backups                            │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Lambda Responsibility Model

```
┌─────────────────────────────────────────────────────────────────┐
│                 LAMBDA (PaaS) RESPONSIBILITIES                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                 CUSTOMER MANAGES                         │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Function Code                        │   │
│  │  ├──────────────┤  Dependencies/Libraries               │   │
│  │  ├──────────────┤  IAM Execution Role                   │   │
│  │  ├──────────────┤  Environment Variables                │   │
│  │  ├──────────────┤  VPC Configuration                    │   │
│  │  └──────────────┘  Resource Policies                    │   │
│  │                                                          │   │
│  │  Customer must:                                          │   │
│  │  • Write secure function code                            │   │
│  │  • Manage dependencies                                   │   │
│  │  • Configure IAM roles                                   │   │
│  │  • Secure environment variables                          │   │
│  │  • Configure VPC if needed                               │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    AWS MANAGES                           │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Runtime Environment                  │   │
│  │  ├──────────────┤  Execution Environment                │   │
│  │  ├──────────────┤  Operating System                     │   │
│  │  ├──────────────┤  Scaling & Availability               │   │
│  │  ├──────────────┤  Compute & Memory                     │   │
│  │  └──────────────┘  Infrastructure                       │   │
│  │                                                          │   │
│  │  AWS automatically:                                      │   │
│  │  • Patches runtime                                       │   │
│  │  • Manages execution environment                         │   │
│  │  • Handles scaling                                       │   │
│  │  • Provides fault tolerance                              │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 3. SaaS - Software as a Service (S3, DynamoDB)

With SaaS/Fully Managed services, AWS handles almost everything except customer data and access control.

### S3 Responsibility Model

```
┌─────────────────────────────────────────────────────────────────┐
│                    S3 (SaaS) RESPONSIBILITIES                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                 CUSTOMER MANAGES                         │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Data (Objects)                       │   │
│  │  ├──────────────┤  Bucket Policies                      │   │
│  │  ├──────────────┤  Access Control Lists (ACLs)          │   │
│  │  ├──────────────┤  Encryption Settings                  │   │
│  │  ├──────────────┤  Versioning Configuration             │   │
│  │  └──────────────┘  Lifecycle Policies                   │   │
│  │                                                          │   │
│  │  Customer must:                                          │   │
│  │  • Secure bucket permissions                             │   │
│  │  • Enable encryption                                     │   │
│  │  • Block public access (when needed)                     │   │
│  │  • Configure logging                                     │   │
│  │  • Manage data lifecycle                                 │   │
│  │  • Enable versioning if required                         │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    AWS MANAGES                           │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Storage Infrastructure               │   │
│  │  ├──────────────┤  Data Durability (11 9s)              │   │
│  │  ├──────────────┤  Availability                         │   │
│  │  ├──────────────┤  Replication                          │   │
│  │  ├──────────────┤  Platform Security                    │   │
│  │  └──────────────┘  Physical Infrastructure              │   │
│  │                                                          │   │
│  │  AWS provides:                                           │   │
│  │  • 99.999999999% durability                              │   │
│  │  • 99.99% availability                                   │   │
│  │  • Automatic data replication                            │   │
│  │  • Encryption options                                    │   │
│  │  • S3 Block Public Access feature                        │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### DynamoDB Responsibility Model

```
┌─────────────────────────────────────────────────────────────────┐
│                 DYNAMODB (SaaS) RESPONSIBILITIES                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                 CUSTOMER MANAGES                         │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Data                                 │   │
│  │  ├──────────────┤  Table Design                         │   │
│  │  ├──────────────┤  IAM Policies                         │   │
│  │  ├──────────────┤  Encryption Settings                  │   │
│  │  ├──────────────┤  Backup Configuration                 │   │
│  │  └──────────────┘  VPC Endpoints (optional)             │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    AWS MANAGES                           │   │
│  ├─────────────────────────────────────────────────────────┤   │
│  │                                                          │   │
│  │  ┌──────────────┐  Database Engine                      │   │
│  │  ├──────────────┤  Scaling                              │   │
│  │  ├──────────────┤  Replication                          │   │
│  │  ├──────────────┤  Patching                             │   │
│  │  ├──────────────┤  Hardware                             │   │
│  │  └──────────────┘  All Infrastructure                   │   │
│  │                                                          │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Visual Comparison: The Stack by Service Type

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    RESPONSIBILITY STACK COMPARISON                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│        IaaS (EC2)           PaaS (RDS)           SaaS (S3)                  │
│                                                                             │
│   ┌────────────────┐   ┌────────────────┐   ┌────────────────┐             │
│   │    Customer    │   │    Customer    │   │    Customer    │             │
│   │      Data      │   │      Data      │   │      Data      │             │
│   ├────────────────┤   ├────────────────┤   ├────────────────┤             │
│   │    Customer    │   │    Customer    │   │    Customer    │             │
│   │  Application   │   │     Schema     │   │   Permissions  │             │
│   ├────────────────┤   ├────────────────┤   ├────────────────┤             │
│   │    Customer    │   │                │   │                │             │
│   │    Runtime     │   │                │   │                │             │
│   ├────────────────┤   │                │   │                │             │
│   │    Customer    │   │      AWS       │   │      AWS       │             │
│   │   Guest OS     │   │    Manages     │   │    Manages     │             │
│   ├────────────────┤   │   Everything   │   │   Everything   │             │
│   │    Customer    │   │     Below      │   │     Below      │             │
│   │ Security Group │   │                │   │                │             │
│   ╠════════════════╣   ╠════════════════╣   ╠════════════════╣             │
│   │      AWS       │   │      AWS       │   │      AWS       │             │
│   │   Hypervisor   │   │   DB Engine    │   │    Storage     │             │
│   ├────────────────┤   ├────────────────┤   ├────────────────┤             │
│   │      AWS       │   │      AWS       │   │      AWS       │             │
│   │    Host OS     │   │      OS        │   │   Platform     │             │
│   ├────────────────┤   ├────────────────┤   ├────────────────┤             │
│   │      AWS       │   │      AWS       │   │      AWS       │             │
│   │   Hardware     │   │   Hardware     │   │   Hardware     │             │
│   └────────────────┘   └────────────────┘   └────────────────┘             │
│                                                                             │
│   █ Customer Responsibility    █ AWS Responsibility                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

## Key Service Examples by Category

### Infrastructure as a Service (IaaS)

| Service | Customer Manages | AWS Manages |
|---------|-----------------|-------------|
| **EC2** | Guest OS, applications, security groups | Hypervisor, host OS, hardware |
| **EBS** | Data, encryption key choice | Storage infrastructure |
| **VPC** | Subnets, routes, security | Network infrastructure |

### Platform as a Service (PaaS)

| Service | Customer Manages | AWS Manages |
|---------|-----------------|-------------|
| **RDS** | Data, schema, security groups | DB engine, OS, patching |
| **Lambda** | Code, dependencies, IAM | Runtime, scaling, infrastructure |
| **Elastic Beanstalk** | Application code | Platform, deployment |
| **ECS/EKS (Fargate)** | Container images, tasks | Infrastructure, orchestration |
| **Aurora** | Data, schema, settings | Engine, replication, failover |

### Software as a Service (SaaS) / Fully Managed

| Service | Customer Manages | AWS Manages |
|---------|-----------------|-------------|
| **S3** | Data, bucket policies | Storage, durability |
| **DynamoDB** | Data, IAM policies | Everything else |
| **SQS/SNS** | Queue/topic policies | Messaging infrastructure |
| **API Gateway** | API definitions, auth | Platform, scaling |
| **Rekognition** | Images/videos sent | ML models, processing |

## Decision Framework: Choosing the Right Service Model

```
┌─────────────────────────────────────────────────────────────────┐
│              SERVICE MODEL DECISION FRAMEWORK                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  CHOOSE IaaS (EC2) WHEN:                                        │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Need full OS control                                   │   │
│  │ • Running legacy applications                            │   │
│  │ • Custom software requirements                           │   │
│  │ • Specific compliance needs requiring OS access          │   │
│  │ • Willing to manage patching and updates                 │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  CHOOSE PaaS (RDS/Lambda) WHEN:                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Want reduced operational burden                        │   │
│  │ • Standard database engines are sufficient               │   │
│  │ • Don't need OS-level access                             │   │
│  │ • Prefer managed patching                                │   │
│  │ • Want automatic scaling (Lambda)                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  CHOOSE SaaS (S3/DynamoDB) WHEN:                                │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ • Want minimal operational responsibility                │   │
│  │ • Need unlimited scale                                   │   │
│  │ • Focus only on data and access control                  │   │
│  │ • Want maximum AWS management                            │   │
│  │ • Building serverless architectures                      │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Exam Tips

> **Tip 1**: Moving from IaaS → PaaS → SaaS means LESS customer responsibility and MORE AWS responsibility

> **Tip 2**: Customer data and IAM are ALWAYS customer responsibility regardless of service type

> **Tip 3**: For EC2 (IaaS): Customer patches Guest OS. For RDS (PaaS): AWS patches DB engine

> **Tip 4**: Lambda is PaaS - AWS manages runtime, customer manages code

> **Tip 5**: S3 is SaaS/Fully Managed - customer only manages data and access policies

> **Tip 6**: The more "managed" the service, the more AWS handles, but data security is still yours

## Key Exam Scenarios

### Scenario 1: Database Patching
**Question**: A company uses RDS MySQL. Who patches the MySQL database engine?
**Answer**: **AWS** - RDS is PaaS, AWS manages the database engine

### Scenario 2: Operating System Updates
**Question**: Who is responsible for OS patches on an EC2 instance running Linux?
**Answer**: **Customer** - EC2 is IaaS, customer manages the guest OS

### Scenario 3: Lambda Security
**Question**: A Lambda function has a vulnerability in its code. Who is responsible?
**Answer**: **Customer** - Function code is always customer responsibility

### Scenario 4: S3 Data Breach
**Question**: Data is exposed from an S3 bucket with public access. Who is responsible?
**Answer**: **Customer** - Bucket permissions are customer responsibility

### Scenario 5: DynamoDB Scaling
**Question**: Who is responsible for scaling DynamoDB tables?
**Answer**: **AWS** (if using on-demand mode) - DynamoDB is fully managed

## Key Takeaways

1. **IaaS = Most customer responsibility** - You manage OS, applications, patching
2. **PaaS = Shared responsibility** - AWS manages platform, you manage data/config
3. **SaaS = Least customer responsibility** - You only manage data and access
4. **Data is ALWAYS customer responsibility** - Regardless of service type
5. **IAM is ALWAYS customer responsibility** - You control who accesses what
6. **Service type determines the dividing line** - Know where the line is for each
7. **More managed = less operational burden** - But still responsible for data security

## Quick Reference

```
╔═══════════════════════════════════════════════════════════════════════════╗
║                 RESPONSIBILITY BY SERVICE TYPE SUMMARY                     ║
╠═══════════════════════════════════════════════════════════════════════════╣
║                                                                           ║
║                     IaaS            PaaS            SaaS                  ║
║                    (EC2)           (RDS)            (S3)                  ║
║  ─────────────────────────────────────────────────────────────────────   ║
║  Data             Customer        Customer        Customer                ║
║  IAM              Customer        Customer        Customer                ║
║  Encryption       Customer        Customer        Customer                ║
║  Application      Customer        Customer        N/A                     ║
║  Guest OS         Customer        AWS             AWS                     ║
║  Platform         Customer        AWS             AWS                     ║
║  Infrastructure   AWS             AWS             AWS                     ║
║  Physical         AWS             AWS             AWS                     ║
║                                                                           ║
║  CUSTOMER CONTROL: ████████████   ████████        ████                   ║
║  AWS CONTROL:      ████           ████████        ████████████           ║
║                                                                           ║
╚═══════════════════════════════════════════════════════════════════════════╝
```

## Summary: The Key Principle

**The more AWS manages, the less you manage - but your data is ALWAYS your responsibility.**

Choose your service model based on:
- How much control you need
- How much operational burden you can handle
- Your team's expertise
- Compliance requirements
- Cost considerations

Remember: Using managed services reduces your security responsibility but never eliminates it entirely. Data classification, encryption decisions, and access control always remain with the customer.

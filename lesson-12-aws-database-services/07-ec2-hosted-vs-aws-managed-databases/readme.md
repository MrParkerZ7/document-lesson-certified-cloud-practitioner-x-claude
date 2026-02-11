# ⚖️ EC2-Hosted vs AWS-Managed Databases

## Introduction

When running databases on AWS, you have two main options: self-managing databases on EC2 instances or using AWS-managed database services like RDS. Understanding the trade-offs between these approaches is important for the Cloud Practitioner exam.

## Overview Comparison

```
+------------------------------------------------------------------+
|            EC2-HOSTED vs AWS-MANAGED DATABASES                    |
+------------------------------------------------------------------+
|                                                                   |
|   EC2-HOSTED (Self-Managed)           AWS-MANAGED (RDS/Aurora)    |
|   +------------------------+          +------------------------+  |
|   |  YOU MANAGE:           |          |  AWS MANAGES:          |  |
|   |  - OS patching         |          |  - OS patching         |  |
|   |  - DB installation     |          |  - DB installation     |  |
|   |  - DB patching         |          |  - DB patching         |  |
|   |  - Backups             |          |  - Backups             |  |
|   |  - High availability   |          |  - High availability   |  |
|   |  - Scaling             |          |  - Scaling             |  |
|   |  - Security config     |          |  - Hardware maintenance|  |
|   +------------------------+          +------------------------+  |
|                                                                   |
|   More control                        Less operational burden     |
|   More responsibility                 Focus on your application   |
|                                                                   |
+------------------------------------------------------------------+
```

## Detailed Responsibility Comparison

| Task | EC2-Hosted | AWS-Managed (RDS) |
|------|------------|-------------------|
| Hardware provisioning | AWS | AWS |
| Hardware maintenance | AWS | AWS |
| Network infrastructure | AWS | AWS |
| OS installation | Customer | AWS |
| OS patching | Customer | AWS |
| Database installation | Customer | AWS |
| Database patching | Customer | AWS |
| Database backups | Customer | AWS |
| High availability setup | Customer | AWS |
| Scaling configuration | Customer | AWS |
| Performance tuning | Customer | Customer |
| Schema design | Customer | Customer |
| Query optimization | Customer | Customer |
| Data management | Customer | Customer |

## EC2-Hosted Databases

### When to Use EC2-Hosted

```
+------------------------------------------------------------------+
|                EC2-HOSTED DATABASE USE CASES                      |
+------------------------------------------------------------------+
|                                                                   |
|   +-----------------------------------------------------------+  |
|   |  CHOOSE EC2-HOSTED WHEN:                                   |  |
|   |                                                            |  |
|   |  [✓] Need full control over DB configuration               |  |
|   |  [✓] Using unsupported database engine                     |  |
|   |  [✓] Need OS-level access                                  |  |
|   |  [✓] Specific version requirements                         |  |
|   |  [✓] Third-party software integration                      |  |
|   |  [✓] Custom extensions/plugins                             |  |
|   |  [✓] Regulatory requirements for self-management           |  |
|   +-----------------------------------------------------------+  |
|                                                                   |
+------------------------------------------------------------------+
```

### EC2-Hosted Architecture

```
+------------------------------------------------------------------+
|                 EC2-HOSTED DATABASE SETUP                         |
+------------------------------------------------------------------+
|                                                                   |
|   VPC                                                             |
|   +----------------------------------------------------------+   |
|   |                                                           |   |
|   |   AZ-A                           AZ-B                     |   |
|   |   +------------------+           +------------------+     |   |
|   |   |  EC2 Instance    |           |  EC2 Instance    |     |   |
|   |   |  +------------+  |           |  +------------+  |     |   |
|   |   |  | Database   |  |           |  | Database   |  |     |   |
|   |   |  | (Primary)  |  |           |  | (Standby)  |  |     |   |
|   |   |  +------------+  |           |  +------------+  |     |   |
|   |   |  +------------+  |           |  +------------+  |     |   |
|   |   |  | EBS Volume |  |           |  | EBS Volume |  |     |   |
|   |   |  +------------+  |  Replication +------------+  |     |   |
|   |   +--------+---------+  <------->+------------------+     |   |
|   |            |                                              |   |
|   |   YOU CONFIGURE: Replication, Failover, Backups           |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

### EC2-Hosted Advantages

| Advantage | Description |
|-----------|-------------|
| Full Control | Complete access to OS and database |
| Any Database | Run any database engine |
| Custom Configuration | Any settings, extensions, plugins |
| Version Flexibility | Run any version you need |
| Licensing | BYOL for any software |

### EC2-Hosted Disadvantages

| Disadvantage | Description |
|--------------|-------------|
| Operational Burden | You manage everything |
| Patching | Manual OS and DB patching |
| Backups | Configure and manage yourself |
| High Availability | Build and maintain yourself |
| Scaling | Manual scaling procedures |
| Expertise Required | Need DBA skills |

## AWS-Managed Databases (RDS/Aurora)

### When to Use AWS-Managed

```
+------------------------------------------------------------------+
|                AWS-MANAGED DATABASE USE CASES                     |
+------------------------------------------------------------------+
|                                                                   |
|   +-----------------------------------------------------------+  |
|   |  CHOOSE AWS-MANAGED WHEN:                                  |  |
|   |                                                            |  |
|   |  [✓] Want to reduce operational burden                     |  |
|   |  [✓] Need built-in high availability                       |  |
|   |  [✓] Want automated backups and patching                   |  |
|   |  [✓] Using supported database engine                       |  |
|   |  [✓] Want push-button scaling                              |  |
|   |  [✓] Limited DBA expertise                                 |  |
|   |  [✓] Focus on application, not infrastructure              |  |
|   +-----------------------------------------------------------+  |
|                                                                   |
+------------------------------------------------------------------+
```

### AWS-Managed Architecture

```
+------------------------------------------------------------------+
|                  RDS MANAGED ARCHITECTURE                         |
+------------------------------------------------------------------+
|                                                                   |
|   VPC                                                             |
|   +----------------------------------------------------------+   |
|   |                                                           |   |
|   |   AZ-A                           AZ-B                     |   |
|   |   +------------------+           +------------------+     |   |
|   |   |  RDS Instance    |  Auto     |  RDS Instance    |     |   |
|   |   |  (Primary)       |  Sync     |  (Standby)       |     |   |
|   |   |                  |<--------->|                  |     |   |
|   |   +------------------+           +------------------+     |   |
|   |            |                                              |   |
|   |   AWS MANAGES: Replication, Failover, Backups, Patching   |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |  AUTOMATED:                                               |   |
|   |  - Daily backups to S3                                    |   |
|   |  - Point-in-time recovery                                 |   |
|   |  - Automatic failover (Multi-AZ)                          |   |
|   |  - Automated patching windows                             |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

### AWS-Managed Advantages

| Advantage | Description |
|-----------|-------------|
| Reduced Operations | AWS handles infrastructure |
| Automated Backups | Daily backups, point-in-time recovery |
| High Availability | Multi-AZ with automatic failover |
| Automated Patching | OS and DB patches applied automatically |
| Easy Scaling | Resize with a few clicks |
| Monitoring | Built-in CloudWatch integration |
| Security | Encryption, security groups, IAM |

### AWS-Managed Disadvantages

| Disadvantage | Description |
|--------------|-------------|
| Less Control | Limited OS access |
| Engine Limits | Only supported engines |
| Version Constraints | Limited version options |
| Feature Limits | Some DB features unavailable |
| Cost | May be higher for simple workloads |

## Cost Comparison

```
+------------------------------------------------------------------+
|                      COST COMPARISON                              |
+------------------------------------------------------------------+
|                                                                   |
|   EC2-HOSTED                          AWS-MANAGED (RDS)           |
|   +------------------------+          +------------------------+  |
|   | Direct Costs:          |          | Direct Costs:          |  |
|   | - EC2 instance         |          | - RDS instance         |  |
|   | - EBS storage          |          | - Storage              |  |
|   | - Data transfer        |          | - Data transfer        |  |
|   |                        |          | - Backups (beyond free)|  |
|   | Hidden Costs:          |          |                        |  |
|   | - DBA time             |          | Hidden Costs:          |  |
|   | - Patching effort      |          | - Potentially higher   |  |
|   | - Backup management    |          |   hourly rate          |  |
|   | - HA configuration     |          |                        |  |
|   | - Monitoring setup     |          |                        |  |
|   +------------------------+          +------------------------+  |
|                                                                   |
|   Often more expensive                Often more cost-effective   |
|   when considering time               when considering TCO        |
|                                                                   |
+------------------------------------------------------------------+
```

### Total Cost of Ownership (TCO)

| Cost Factor | EC2-Hosted | AWS-Managed |
|-------------|------------|-------------|
| Instance/Service | EC2 pricing | RDS pricing (slightly higher) |
| Storage | EBS pricing | RDS storage pricing |
| Operational Labor | High (DBA time) | Low (automated) |
| Downtime Risk | Higher (manual recovery) | Lower (auto failover) |
| Backup Infrastructure | Additional cost | Included |

## Decision Framework

```
+------------------------------------------------------------------+
|                    DECISION FRAMEWORK                             |
+------------------------------------------------------------------+
|                                                                   |
|   START                                                           |
|     |                                                             |
|     v                                                             |
|   Is your database engine supported by RDS?                       |
|     |                                                             |
|     +--NO--> Use EC2-Hosted                                       |
|     |                                                             |
|     YES                                                           |
|     |                                                             |
|     v                                                             |
|   Do you need OS-level access or custom extensions?               |
|     |                                                             |
|     +--YES--> Use EC2-Hosted                                      |
|     |                                                             |
|     NO                                                            |
|     |                                                             |
|     v                                                             |
|   Do you want to minimize operational burden?                     |
|     |                                                             |
|     +--YES--> Use AWS-Managed (RDS/Aurora)                        |
|     |                                                             |
|     NO                                                            |
|     |                                                             |
|     v                                                             |
|   Do you have strong DBA expertise?                               |
|     |                                                             |
|     +--YES--> Consider EC2-Hosted for maximum control             |
|     |                                                             |
|     +--NO---> Use AWS-Managed (RDS/Aurora)                        |
|                                                                   |
+------------------------------------------------------------------+
```

## Quick Reference

| Criteria | Recommendation |
|----------|---------------|
| Minimize operations | AWS-Managed |
| Maximum control | EC2-Hosted |
| Unsupported engine | EC2-Hosted |
| Automated HA | AWS-Managed |
| Custom configurations | EC2-Hosted |
| Standard workloads | AWS-Managed |
| Specific version needed | EC2-Hosted |
| Limited DBA resources | AWS-Managed |

## 🎯 Exam Tips

- **EC2-hosted** = full control, full responsibility (OS, patching, backups)
- **AWS-managed (RDS)** = AWS handles operations (patching, backups, HA)
- Choose **EC2-hosted** when you need unsupported engines or full OS access
- Choose **RDS/Aurora** to reduce operational burden and focus on your app
- **RDS** handles: hardware, OS patching, DB patching, backups, HA, scaling
- **Customer** handles (both options): schema design, query optimization, data
- AWS-managed services follow the **shared responsibility model**
- Consider **total cost of ownership**, not just instance pricing

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Self-Managed | Customer manages all database operations |
| Fully Managed | Cloud provider handles infrastructure operations |
| DBA | Database Administrator |
| TCO | Total Cost of Ownership |
| BYOL | Bring Your Own License |
| Operational Burden | Time and effort to manage infrastructure |
| Undifferentiated Heavy Lifting | Commodity work that doesn't add business value |

## 💡 Key Takeaways

1. EC2-hosted databases give you full control but require full management
2. AWS-managed databases reduce operational burden significantly
3. Choose EC2-hosted for unsupported engines or when you need OS access
4. Choose RDS/Aurora for supported engines when you want automated operations
5. Consider total cost of ownership, including operational labor
6. Both options require customer management of schema and queries
7. AWS-managed services let you focus on your application, not infrastructure

---

*Previous: [06 - Database Migration](../06-database-migration/readme.md)*

---

## Lesson Navigation

- [01 - Database Types Overview](../01-database-types-overview/readme.md)
- [02 - Relational Databases](../02-relational-databases/readme.md)
- [03 - NoSQL Databases](../03-nosql-databases/readme.md)
- [04 - In-Memory Databases](../04-in-memory-databases/readme.md)
- [05 - Other Database Services](../05-other-database-services/readme.md)
- [06 - Database Migration](../06-database-migration/readme.md)
- [07 - EC2-Hosted vs AWS-Managed Databases](../07-ec2-hosted-vs-aws-managed-databases/readme.md) (Current)

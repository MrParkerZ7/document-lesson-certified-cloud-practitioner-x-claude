# Backup and Recovery

## File Structure

```
lesson-14-aws-storage-services/
└── 05-backup-and-recovery/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides comprehensive backup and disaster recovery solutions to protect your data and ensure business continuity. AWS Backup offers centralized, policy-driven backup management, while various replication and DR strategies help organizations meet their recovery objectives. Understanding these services is essential for the AWS CCP exam.

## Backup and Recovery Concepts

```
+------------------------------------------------------------------+
|                 BACKUP AND RECOVERY CONCEPTS                      |
+------------------------------------------------------------------+
|                                                                   |
|   RPO (Recovery Point Objective)                                  |
|   = Maximum acceptable data loss (time)                           |
|                                                                   |
|   RTO (Recovery Time Objective)                                   |
|   = Maximum acceptable downtime                                   |
|                                                                   |
|      Last Backup            Disaster           Recovery           |
|          |                     |                  |               |
|   -------|---------------------|------------------|-------->      |
|          |<------- RPO ------->|<----- RTO ------>|               |
|          |    (Data Loss)      |    (Downtime)    |               |
|                                                                   |
+------------------------------------------------------------------+
```

## RPO and RTO

| Term | Definition | Question It Answers |
|------|------------|---------------------|
| RPO | Recovery Point Objective | How much data can we afford to lose? |
| RTO | Recovery Time Objective | How long can we be down? |

| RPO Example | Meaning |
|-------------|---------|
| RPO = 1 hour | Backups every hour, max 1 hour of data loss |
| RPO = 24 hours | Daily backups, max 1 day of data loss |
| RPO = 0 | No data loss acceptable (continuous replication) |

| RTO Example | Meaning |
|-------------|---------|
| RTO = 4 hours | System must be restored within 4 hours |
| RTO = 24 hours | Can tolerate 1 day of downtime |
| RTO = minutes | Near-zero downtime required |

## AWS Backup

| Feature | Description |
|---------|-------------|
| Type | Centralized backup management service |
| Supported Services | EC2, EBS, RDS, DynamoDB, EFS, FSx, S3, and more |
| Policy-Driven | Backup plans with schedules and retention |
| Cross-Region | Copy backups to other regions |
| Cross-Account | Backup to different AWS accounts |
| Compliance | Audit and reporting capabilities |

## AWS Backup Architecture

```
+------------------------------------------------------------------+
|                       AWS BACKUP                                  |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                    BACKUP PLAN                            |   |
|   |  Schedule: Daily at 2:00 AM                               |   |
|   |  Retention: 30 days                                       |   |
|   |  Cross-Region: us-west-2                                  |   |
|   +----------------------------------------------------------+   |
|                              |                                    |
|         +--------------------+--------------------+               |
|         |                    |                    |               |
|   +-----v-----+        +-----v-----+        +-----v-----+         |
|   |   EC2     |        |    RDS    |        |    EFS    |         |
|   | Instances |        | Databases |        |   File    |         |
|   +-----------+        +-----------+        |  Systems  |         |
|         |                    |              +-----------+         |
|         v                    v                    |               |
|   +-----------+        +-----------+              v               |
|   | Snapshots |        | Snapshots |        +-----------+         |
|   +-----------+        +-----------+        | Backups   |         |
|                                             +-----------+         |
|                              |                                    |
|                              v                                    |
|                    +------------------+                           |
|                    |   BACKUP VAULT   |                           |
|                    | (Encrypted, IAM) |                           |
|                    +------------------+                           |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Backup Components

| Component | Description |
|-----------|-------------|
| Backup Plan | Rules defining when and how to backup |
| Backup Vault | Storage container for backups |
| Recovery Point | Individual backup (snapshot, backup) |
| Resource Assignment | Which resources to backup |

## Backup Plan Settings

| Setting | Description |
|---------|-------------|
| Backup Frequency | How often (hourly, daily, weekly, monthly) |
| Backup Window | Time window for backup execution |
| Retention Period | How long to keep backups |
| Lifecycle Rules | Transition to cold storage |
| Copy to Region | Cross-region backup copy |

## Cross-Region Replication

| Service | Replication Feature | Use Case |
|---------|---------------------|----------|
| S3 | Cross-Region Replication (CRR) | DR, latency |
| RDS | Read Replicas, Automated Backups | DR, scaling |
| DynamoDB | Global Tables | Multi-region active |
| EBS | Snapshot Copy | DR, migration |
| EFS | Replication | DR |

## S3 Replication

```
+------------------------------------------------------------------+
|                    S3 CROSS-REGION REPLICATION                    |
+------------------------------------------------------------------+
|                                                                   |
|   SOURCE REGION (us-east-1)         DESTINATION REGION (eu-west-1)|
|   +------------------+              +------------------+          |
|   |   S3 Bucket      |   Async      |   S3 Bucket      |          |
|   |                  | -----------> |                  |          |
|   |  +-----------+   |  Replicate   |  +-----------+   |          |
|   |  | Object A  |   |              |  | Object A  |   |          |
|   |  +-----------+   |              |  +-----------+   |          |
|   |  | Object B  |   |              |  | Object B  |   |          |
|   |  +-----------+   |              |  +-----------+   |          |
|   +------------------+              +------------------+          |
|                                                                   |
|   Requirements:                                                   |
|   - Versioning enabled on both buckets                           |
|   - IAM permissions configured                                    |
|   - Different destination region (CRR) or same region (SRR)      |
|                                                                   |
+------------------------------------------------------------------+
```

## Replication Types

| Type | Description | Use Case |
|------|-------------|----------|
| CRR | Cross-Region Replication | Disaster recovery, compliance |
| SRR | Same-Region Replication | Log aggregation, compliance |

## Disaster Recovery Strategies

| Strategy | RTO/RPO | Cost | Description |
|----------|---------|------|-------------|
| Backup & Restore | Hours | Lowest | Restore from backups |
| Pilot Light | 10s of minutes | Low | Minimal core running |
| Warm Standby | Minutes | Medium | Scaled-down version running |
| Multi-Site Active-Active | Real-time | Highest | Full deployment in multiple regions |

## DR Strategies Diagram

```
+------------------------------------------------------------------+
|              DISASTER RECOVERY STRATEGIES                         |
+------------------------------------------------------------------+
|                                                                   |
|   COST                        RTO/RPO                             |
|   Low  |                                                          |
|        |  +------------------+                                    |
|        |  | BACKUP & RESTORE |  Hours RTO, Hours RPO              |
|        |  | - Backups in S3  |  - Restore from snapshots          |
|        |  +------------------+  - Lowest cost, longest RTO        |
|        |                                                          |
|        |  +------------------+                                    |
|        |  | PILOT LIGHT      |  10s min RTO, Minutes RPO          |
|        |  | - Core running   |  - Database replicated             |
|        |  +------------------+  - Scale up when needed            |
|        |                                                          |
|        |  +------------------+                                    |
|        |  | WARM STANDBY     |  Minutes RTO, Seconds RPO          |
|        |  | - Scaled-down    |  - Functional, smaller scale       |
|        |  +------------------+  - Quick scale up                  |
|        |                                                          |
|   High |  +------------------+                                    |
|        |  | MULTI-SITE       |  Near-zero RTO/RPO                 |
|        |  | ACTIVE-ACTIVE    |  - Full scale in both regions      |
|        |  +------------------+  - Highest availability            |
|        +---------------------------------------------------->     |
|                            RECOVERY TIME (Faster --->)            |
|                                                                   |
+------------------------------------------------------------------+
```

## Backup and Restore

| Feature | Description |
|---------|-------------|
| How It Works | Backup data to S3, restore when needed |
| RTO | Hours (time to restore) |
| RPO | Hours (last backup point) |
| Cost | Lowest |
| Use Case | Non-critical workloads |

## Pilot Light

| Feature | Description |
|---------|-------------|
| How It Works | Core components running (e.g., database) |
| RTO | 10s of minutes |
| RPO | Minutes (near real-time replication) |
| Cost | Low |
| Use Case | Critical databases, apps that can scale |

## Warm Standby

| Feature | Description |
|---------|-------------|
| How It Works | Scaled-down but fully functional copy |
| RTO | Minutes |
| RPO | Seconds (continuous replication) |
| Cost | Medium |
| Use Case | Business-critical applications |

## Multi-Site Active-Active

| Feature | Description |
|---------|-------------|
| How It Works | Full production in multiple regions |
| RTO | Near zero |
| RPO | Near zero |
| Cost | Highest |
| Use Case | Mission-critical, zero downtime |

## AWS Services for DR

| Service | DR Capability |
|---------|---------------|
| Route 53 | Health checks, DNS failover |
| S3 | Cross-region replication |
| RDS | Multi-AZ, read replicas, automated backups |
| DynamoDB | Global tables, point-in-time recovery |
| Aurora | Global databases, automated backups |
| EBS | Snapshots, cross-region copy |
| AWS Backup | Centralized backup management |

## Data Protection Features

| Feature | Service | Description |
|---------|---------|-------------|
| Point-in-Time Recovery | RDS, DynamoDB | Restore to any second within retention |
| Automated Backups | RDS, DynamoDB, EBS | Scheduled automatic backups |
| Snapshots | EBS, RDS | Manual point-in-time copies |
| Versioning | S3 | Keep multiple object versions |
| MFA Delete | S3 | Require MFA to delete objects |
| Vault Lock | S3 Glacier, Backup | WORM (Write Once Read Many) |

## AWS Backup Vault Lock

| Feature | Description |
|---------|-------------|
| Purpose | WORM compliance for backups |
| Immutability | Backups cannot be deleted |
| Compliance | SEC, FINRA, other regulations |
| Governance Mode | Soft lock, admin can remove |
| Compliance Mode | Hard lock, cannot be removed |

## Exam Tips

- **RPO** = how much data loss is acceptable (time between backups)
- **RTO** = how long recovery can take (downtime tolerance)
- **AWS Backup** = centralized backup for EC2, RDS, EBS, EFS, DynamoDB, S3
- **Backup & Restore** = lowest cost, highest RTO
- **Pilot Light** = core components running, quick scale-up
- **Warm Standby** = scaled-down functional copy
- **Active-Active** = full deployment in multiple regions, highest cost
- **S3 CRR** = cross-region replication requires versioning
- **Vault Lock** = WORM compliance, immutable backups
- **Point-in-Time Recovery** = restore to any second (RDS, DynamoDB)
- Know DR strategy trade-offs between cost and recovery time

## Key Terms

| Term | Definition |
|------|------------|
| RPO | Recovery Point Objective - max acceptable data loss |
| RTO | Recovery Time Objective - max acceptable downtime |
| Backup Plan | Policy defining backup schedule and retention |
| Backup Vault | Container for storing backups |
| Cross-Region Replication | Copying data to another AWS region |
| Pilot Light | DR with minimal core components running |
| Warm Standby | DR with scaled-down functional copy |
| Active-Active | Full production running in multiple regions |
| WORM | Write Once Read Many - immutable storage |

## Key Takeaways

1. RPO defines acceptable data loss; RTO defines acceptable downtime
2. AWS Backup provides centralized, policy-driven backup management
3. DR strategies range from Backup & Restore (cheapest) to Active-Active (most resilient)
4. Lower RTO/RPO requirements increase cost and complexity
5. Cross-region replication enables DR and compliance requirements
6. Backup Vault Lock provides WORM compliance for regulatory needs
7. Point-in-Time Recovery enables granular restore for databases
8. Choose DR strategy based on business requirements for cost vs. recovery time

---

*Previous: [04 - Hybrid and Edge Storage](../04-hybrid-and-edge-storage/readme.md)*

---

*Return to: [Lesson 14 - AWS Storage Services](../readme.md)*

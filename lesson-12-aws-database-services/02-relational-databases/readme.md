# 🗄️ Relational Databases (Amazon RDS and Aurora)

## File Structure

```
lesson-12-aws-database-services/
└── 02-relational-databases/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Amazon Relational Database Service (RDS) makes it easy to set up, operate, and scale relational databases in the cloud. Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud with performance and availability of commercial databases at a fraction of the cost.

## Amazon RDS Overview

```
+------------------------------------------------------------------+
|                        AMAZON RDS                                 |
+------------------------------------------------------------------+
|                                                                   |
|   Managed Relational Database Service                             |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                  AWS MANAGES                              |   |
|   |  - Provisioning       - Patching                          |   |
|   |  - Backups            - Monitoring                        |   |
|   |  - Scaling            - Hardware maintenance              |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                  YOU MANAGE                               |   |
|   |  - Schema design      - Query optimization                |   |
|   |  - Data               - Application code                  |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Supported Database Engines

Amazon RDS supports six popular database engines:

| Engine | Description | License |
|--------|-------------|---------|
| **MySQL** | Most popular open-source database | Open source |
| **PostgreSQL** | Advanced open-source database | Open source |
| **MariaDB** | MySQL fork with enhanced features | Open source |
| **Oracle** | Enterprise commercial database | License included or BYOL |
| **SQL Server** | Microsoft's enterprise database | License included or BYOL |
| **Amazon Aurora** | AWS cloud-native database | Proprietary |

### Engine Selection Guide

```
+------------------------------------------------------------------+
|                   RDS ENGINE SELECTION                            |
+------------------------------------------------------------------+
|                                                                   |
|   Open Source (No licensing costs)                                |
|   +------------------+  +------------------+  +------------------+ |
|   |     MySQL        |  |   PostgreSQL     |  |    MariaDB       | |
|   |  Most popular    |  |  Advanced SQL    |  |  MySQL fork      | |
|   |  Web apps        |  |  GIS, analytics  |  |  Enhanced perf   | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
|   Commercial (License required)                                   |
|   +------------------+  +------------------+                      |
|   |    Oracle        |  |   SQL Server     |                      |
|   |  Enterprise apps |  |  .NET apps       |                      |
|   |  BYOL or included|  |  Windows stack   |                      |
|   +------------------+  +------------------+                      |
|                                                                   |
|   AWS Native                                                      |
|   +------------------------------------------+                    |
|   |              Amazon Aurora               |                    |
|   |  MySQL/PostgreSQL compatible, 5x faster  |                    |
|   +------------------------------------------+                    |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon RDS Features

| Feature | Description |
|---------|-------------|
| Automated Backups | Point-in-time recovery, up to 35-day retention |
| Manual Snapshots | User-initiated, persist until deleted |
| Multi-AZ Deployment | Synchronous standby replica for high availability |
| Read Replicas | Asynchronous copies for read scaling |
| Auto Scaling | Automatically adjust storage capacity |
| Encryption | At-rest (KMS) and in-transit (SSL/TLS) |
| Monitoring | CloudWatch metrics, Enhanced Monitoring |

## Multi-AZ Deployments

Multi-AZ provides high availability and automatic failover.

```
+------------------------------------------------------------------+
|                    MULTI-AZ DEPLOYMENT                            |
+------------------------------------------------------------------+
|                                                                   |
|   Region                                                          |
|   +----------------------------------------------------------+   |
|   |                                                           |   |
|   |   AZ-A                           AZ-B                     |   |
|   |   +------------------+           +------------------+     |   |
|   |   |   PRIMARY        |           |   STANDBY        |     |   |
|   |   |   (Active)       |  Sync     |   (Passive)      |     |   |
|   |   |                  |<--------->|                  |     |   |
|   |   |   Read/Write     | Replication   Read/Write     |     |   |
|   |   +------------------+           +------------------+     |   |
|   |          ^                              ^                 |   |
|   |          |                              |                 |   |
|   |          |     Automatic Failover       |                 |   |
|   |          +----------(DNS)---------------+                 |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

| Multi-AZ Feature | Description |
|------------------|-------------|
| Purpose | High availability, not read scaling |
| Replication | Synchronous |
| Failover | Automatic, 60-120 seconds |
| Endpoint | Single DNS endpoint |
| Cost | 2x the cost (two instances) |

## Read Replicas

Read Replicas provide horizontal read scaling.

```
+------------------------------------------------------------------+
|                      READ REPLICAS                                |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+                                            |
|   |     PRIMARY      |                                            |
|   |   (Read/Write)   |                                            |
|   +--------+---------+                                            |
|            | Async Replication                                    |
|   +--------+---------+---------+                                  |
|   |        |         |         |                                  |
|   v        v         v         v                                  |
| +----+   +----+   +----+   +----+                                 |
| | RR |   | RR |   | RR |   | RR |  Up to 15 replicas (Aurora)     |
| +----+   +----+   +----+   +----+  Up to 5 replicas (RDS)         |
|                                                                   |
|   Read traffic distributed across replicas                        |
|                                                                   |
+------------------------------------------------------------------+
```

| Read Replica Feature | Description |
|----------------------|-------------|
| Purpose | Scale read traffic, reporting |
| Replication | Asynchronous |
| Can be promoted | Yes, to standalone database |
| Cross-Region | Supported |
| Same endpoint | No, separate endpoints |

## Amazon Aurora

Amazon Aurora is a fully managed, MySQL and PostgreSQL-compatible relational database.

```
+------------------------------------------------------------------+
|                       AMAZON AURORA                               |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                   Aurora Cluster                          |   |
|   |                                                           |   |
|   |   +------------------+    +------------------+            |   |
|   |   |  Primary Instance|    | Aurora Replica   |  x15 max   |   |
|   |   |   (Read/Write)   |    |   (Read Only)    |            |   |
|   |   +--------+---------+    +--------+---------+            |   |
|   |            |                       |                      |   |
|   |            +-----------+-----------+                      |   |
|   |                        |                                  |   |
|   |            +-----------+-----------+                      |   |
|   |            |   Shared Storage      |                      |   |
|   |            |   (Auto-scaling)      |                      |   |
|   |            |   6 copies, 3 AZs     |                      |   |
|   |            +-----------------------+                      |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

### Aurora Key Features

| Feature | Description |
|---------|-------------|
| Performance | 5x faster than MySQL, 3x faster than PostgreSQL |
| Storage | Auto-scales from 10GB to 128TB |
| Availability | 6 copies of data across 3 AZs |
| Replicas | Up to 15 Aurora Replicas |
| Failover | Automatic, typically under 30 seconds |
| Backtrack | Rewind database to specific point in time |
| Global Database | Cross-region replication under 1 second |

### Aurora Serverless

| Feature | Description |
|---------|-------------|
| Type | On-demand, auto-scaling configuration |
| Scaling | Automatically adjusts capacity |
| Billing | Pay per second for capacity used |
| Use Cases | Infrequent, intermittent, unpredictable workloads |
| Cold Start | May have connection delay when scaling from zero |

## RDS vs Aurora Comparison

| Feature | Amazon RDS | Amazon Aurora |
|---------|------------|---------------|
| Engines | MySQL, PostgreSQL, MariaDB, Oracle, SQL Server | MySQL, PostgreSQL compatible |
| Performance | Standard | 5x MySQL, 3x PostgreSQL |
| Storage | Up to 64TB | Up to 128TB, auto-scaling |
| Replicas | Up to 5 | Up to 15 |
| Availability | Multi-AZ (2 copies) | 6 copies across 3 AZs |
| Failover Time | 60-120 seconds | Typically under 30 seconds |
| Cost | Lower for small workloads | Higher but better performance |
| Serverless | No | Yes (Aurora Serverless) |

## Backup and Recovery

| Backup Type | RDS | Aurora |
|-------------|-----|--------|
| Automated Backups | Daily, up to 35 days | Continuous, up to 35 days |
| Manual Snapshots | Yes, persist until deleted | Yes, persist until deleted |
| Point-in-Time Recovery | Within retention period | Within retention period |
| Cross-Region Copy | Yes | Yes |
| Backtrack | No | Yes (Aurora only) |

## RDS Pricing Components

| Component | Description |
|-----------|-------------|
| Instance Hours | Based on instance class and engine |
| Storage | Per GB-month |
| I/O Requests | For Aurora, per million requests |
| Backup Storage | Beyond free allocation |
| Data Transfer | Outbound data transfer |

## 🎯 Exam Tips

- **RDS** = managed relational database, supports 6 engines
- **Aurora** = MySQL/PostgreSQL compatible, 5x faster than MySQL, 3x faster than PostgreSQL
- **Multi-AZ** = high availability (sync replication), automatic failover
- **Read Replicas** = read scaling (async replication), can be cross-region
- **Aurora stores 6 copies** of data across 3 AZs automatically
- **Aurora Serverless** = auto-scaling, pay-per-use, good for unpredictable workloads
- RDS handles patching, backups, and hardware maintenance (you manage schema and data)
- **BYOL** = Bring Your Own License (Oracle, SQL Server)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| RDS | Amazon Relational Database Service |
| Aurora | AWS cloud-native relational database |
| Multi-AZ | Deployment with synchronous standby in different AZ |
| Read Replica | Asynchronous copy for read scaling |
| Aurora Serverless | Auto-scaling Aurora configuration |
| BYOL | Bring Your Own License |
| Point-in-Time Recovery | Restore database to any second within retention |
| Backtrack | Aurora feature to rewind database state |

## 💡 Key Takeaways

1. Amazon RDS is a managed service supporting MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Aurora
2. RDS handles administrative tasks: backups, patching, scaling, and monitoring
3. Multi-AZ provides high availability with automatic failover (not for read scaling)
4. Read Replicas enable horizontal read scaling and can be promoted to standalone databases
5. Aurora offers 5x MySQL and 3x PostgreSQL performance with automatic storage scaling
6. Aurora stores 6 copies of data across 3 AZs for high durability
7. Aurora Serverless automatically scales capacity based on demand

---

*Previous: [01 - Database Types Overview](../01-database-types-overview/readme.md) | Next: [03 - NoSQL Databases](../03-nosql-databases/readme.md)*

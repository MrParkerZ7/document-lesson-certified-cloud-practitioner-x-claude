# 🔄 Database Migration (AWS DMS and SCT)

## File Structure

```
lesson-12-aws-database-services/
└── 06-database-migration/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides powerful tools for migrating databases to the cloud. AWS Database Migration Service (DMS) and AWS Schema Conversion Tool (SCT) enable you to migrate databases quickly and securely while minimizing downtime.

## Database Migration Overview

```
+------------------------------------------------------------------+
|                   DATABASE MIGRATION PATH                         |
+------------------------------------------------------------------+
|                                                                   |
|   SOURCE                                           TARGET         |
|   +------------------+                     +------------------+   |
|   |  On-Premises     |                     |    AWS Cloud     |   |
|   |  - Oracle        |                     |    - RDS         |   |
|   |  - SQL Server    |     AWS DMS         |    - Aurora      |   |
|   |  - MySQL         |==================>  |    - DynamoDB    |   |
|   |  - PostgreSQL    |                     |    - Redshift    |   |
|   |  - Other DBs     |                     |    - S3          |   |
|   +------------------+                     +------------------+   |
|                                                                   |
|   Also supports:                                                  |
|   - Cloud to Cloud (other cloud -> AWS)                           |
|   - AWS to AWS (RDS -> Aurora)                                    |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Database Migration Service (DMS)

AWS DMS helps you migrate databases to AWS quickly and securely with minimal downtime.

### DMS Architecture

```
+------------------------------------------------------------------+
|                      AWS DMS ARCHITECTURE                         |
+------------------------------------------------------------------+
|                                                                   |
|   SOURCE              REPLICATION              TARGET             |
|   DATABASE            INSTANCE                 DATABASE           |
|   +--------+         +----------+              +--------+         |
|   |        |         |          |              |        |         |
|   | Oracle |-------->|   DMS    |------------->| Aurora |         |
|   |        |  Read   | Instance |    Write     |        |         |
|   +--------+         +----------+              +--------+         |
|                           |                                       |
|                      Runs in VPC                                  |
|                      - Compute resources                          |
|                      - Storage for tasks                          |
|                                                                   |
+------------------------------------------------------------------+
```

### DMS Key Features

| Feature | Description |
|---------|-------------|
| Minimal Downtime | Source database remains operational during migration |
| Homogeneous Migration | Same engine (e.g., MySQL to MySQL) |
| Heterogeneous Migration | Different engines (e.g., Oracle to PostgreSQL) |
| Continuous Replication | Keep source and target in sync |
| Pre-configured Instance | Replication instance handles migration |

### DMS Migration Types

| Type | Description | Use Case |
|------|-------------|----------|
| Full Load | Migrate all existing data | One-time migration |
| CDC (Change Data Capture) | Replicate ongoing changes | Continuous sync |
| Full Load + CDC | Initial load then ongoing changes | Migration with minimal downtime |

### How DMS Works

```
+------------------------------------------------------------------+
|                    DMS MIGRATION PROCESS                          |
+------------------------------------------------------------------+
|                                                                   |
|   1. FULL LOAD                                                    |
|   +------------------+                     +------------------+   |
|   | Source Database  |===================>| Target Database  |   |
|   | (All data)       |  Initial load      | (Copy of data)   |   |
|   +------------------+                     +------------------+   |
|                                                                   |
|   2. CHANGE DATA CAPTURE (CDC)                                    |
|   +------------------+                     +------------------+   |
|   | Source Database  |------[Changes]---->| Target Database  |   |
|   | (Ongoing writes) |  Continuous sync   | (Stays updated)  |   |
|   +------------------+                     +------------------+   |
|                                                                   |
|   3. CUTOVER                                                      |
|   +------------------+                     +------------------+   |
|   | Source Database  |        X           | Target Database  |   |
|   | (Decommissioned) |  Switch apps       | (Now primary)    |   |
|   +------------------+                     +------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

### Supported Migration Paths

| Source | Target |
|--------|--------|
| On-premises databases | Amazon RDS |
| EC2-hosted databases | Amazon Aurora |
| Amazon RDS | Amazon Redshift |
| Amazon S3 | Amazon DynamoDB |
| Other cloud providers | Any supported target |

### DMS Use Cases

| Use Case | Description |
|----------|-------------|
| Cloud Migration | Move on-premises DBs to AWS |
| Database Consolidation | Combine multiple databases |
| Continuous Replication | Keep dev/test in sync with production |
| Data Warehouse Loading | Stream data to Redshift |
| Disaster Recovery | Maintain replica in different region |

## AWS Schema Conversion Tool (SCT)

AWS SCT converts database schemas from one engine to another when performing heterogeneous migrations.

```
+------------------------------------------------------------------+
|                  SCHEMA CONVERSION TOOL                           |
+------------------------------------------------------------------+
|                                                                   |
|   HETEROGENEOUS MIGRATION (Different engines)                     |
|                                                                   |
|   SOURCE SCHEMA         SCT CONVERSION         TARGET SCHEMA      |
|   +-------------+       +-------------+        +-------------+    |
|   |  Oracle     |       |             |        |  PostgreSQL |    |
|   |  - Tables   |------>|   AWS SCT   |------->|  - Tables   |    |
|   |  - Views    |       |             |        |  - Views    |    |
|   |  - Procs    |       |  Converts:  |        |  - Functions|    |
|   |  - Triggers |       |  - Schema   |        |  - Triggers |    |
|   +-------------+       |  - Code     |        +-------------+    |
|                         |  - Objects  |                           |
|                         +-------------+                           |
|                                                                   |
|   Note: Some objects may need manual conversion                   |
|                                                                   |
+------------------------------------------------------------------+
```

### SCT Features

| Feature | Description |
|---------|-------------|
| Schema Conversion | Converts tables, views, indexes |
| Code Conversion | Converts stored procedures, functions |
| Assessment Report | Identifies conversion complexity |
| Data Type Mapping | Maps source types to target types |
| Manual Conversion Help | Flags objects needing manual work |

### When to Use SCT

| Scenario | SCT Needed? |
|----------|-------------|
| Oracle to PostgreSQL | Yes |
| SQL Server to MySQL | Yes |
| MySQL to MySQL | No (homogeneous) |
| PostgreSQL to Aurora PostgreSQL | No (compatible) |
| Oracle to Aurora PostgreSQL | Yes |

### SCT Assessment Report

```
+------------------------------------------------------------------+
|                 SCT ASSESSMENT REPORT                             |
+------------------------------------------------------------------+
|                                                                   |
|   Migration Complexity Analysis                                   |
|                                                                   |
|   +--------------------+------------------+------------------+    |
|   |  Object Type       |  Auto-Convert    |  Manual Work     |    |
|   |--------------------|------------------|------------------|    |
|   |  Tables            |  95%             |  5%              |    |
|   |  Views             |  85%             |  15%             |    |
|   |  Stored Procedures |  70%             |  30%             |    |
|   |  Triggers          |  80%             |  20%             |    |
|   +--------------------+------------------+------------------+    |
|                                                                   |
|   Total Estimated Effort: 120 hours manual work                   |
|                                                                   |
+------------------------------------------------------------------+
```

## DMS + SCT Together

For heterogeneous migrations, use both tools together.

```
+------------------------------------------------------------------+
|                 HETEROGENEOUS MIGRATION FLOW                      |
+------------------------------------------------------------------+
|                                                                   |
|   STEP 1: Convert Schema (SCT)                                    |
|   +------------------+           +------------------+             |
|   | Oracle Schema    |  SCT      | PostgreSQL       |             |
|   | (Tables, Procs)  |========>  | Schema           |             |
|   +------------------+           +------------------+             |
|                                                                   |
|   STEP 2: Migrate Data (DMS)                                      |
|   +------------------+           +------------------+             |
|   | Oracle Data      |  DMS      | PostgreSQL       |             |
|   | (Rows)           |========>  | Data             |             |
|   +------------------+           +------------------+             |
|                                                                   |
|   STEP 3: Continuous Sync (DMS CDC)                               |
|   +------------------+           +------------------+             |
|   | Oracle Changes   |  DMS      | PostgreSQL       |             |
|   | (New/Updated)    |------->   | (Synced)         |             |
|   +------------------+           +------------------+             |
|                                                                   |
+------------------------------------------------------------------+
```

## Migration Scenarios

### Homogeneous Migration

| Source | Target | Tools Needed |
|--------|--------|--------------|
| MySQL (on-prem) | RDS MySQL | DMS only |
| PostgreSQL (on-prem) | Aurora PostgreSQL | DMS only |
| SQL Server (on-prem) | RDS SQL Server | DMS only |

### Heterogeneous Migration

| Source | Target | Tools Needed |
|--------|--------|--------------|
| Oracle | Aurora PostgreSQL | SCT + DMS |
| SQL Server | Aurora MySQL | SCT + DMS |
| Oracle | Redshift | SCT + DMS |

## DMS Pricing

| Component | Pricing Model |
|-----------|---------------|
| Replication Instance | Per hour (based on instance type) |
| Storage | Per GB-month |
| Data Transfer | Standard AWS data transfer rates |

## Best Practices

| Practice | Description |
|----------|-------------|
| Test First | Use DMS assessment to understand scope |
| Size Correctly | Choose appropriate replication instance |
| Use Multi-AZ | For production migrations |
| Monitor Progress | Use CloudWatch metrics |
| Plan Cutover | Schedule during low-traffic periods |

## 🎯 Exam Tips

- **DMS** = migrate databases with minimal downtime
- **SCT** = convert schemas between different database engines
- **Homogeneous migration** (same engine) = DMS only
- **Heterogeneous migration** (different engine) = SCT + DMS
- DMS supports **continuous replication** (CDC) for ongoing sync
- Source database remains **fully operational** during migration
- DMS runs on a **replication instance** in your VPC
- SCT generates an **assessment report** showing conversion complexity

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| DMS | AWS Database Migration Service |
| SCT | AWS Schema Conversion Tool |
| Homogeneous Migration | Same database engine source and target |
| Heterogeneous Migration | Different database engines |
| CDC | Change Data Capture - continuous replication |
| Full Load | One-time migration of all existing data |
| Replication Instance | EC2 instance running DMS tasks |
| Assessment Report | SCT report showing conversion complexity |

## 💡 Key Takeaways

1. AWS DMS migrates databases with minimal downtime
2. DMS keeps source database operational during migration
3. SCT converts schemas between different database engines
4. Use DMS alone for homogeneous migrations (same engine)
5. Use SCT + DMS for heterogeneous migrations (different engines)
6. CDC enables continuous replication after initial load
7. SCT assessment reports help estimate migration effort

---

*Previous: [05 - Other Database Services](../05-other-database-services/readme.md) | Next: [07 - EC2-Hosted vs AWS-Managed Databases](../07-ec2-hosted-vs-aws-managed-databases/readme.md)*

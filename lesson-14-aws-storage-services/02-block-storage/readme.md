# Amazon EBS (Elastic Block Store)

## File Structure

```
lesson-14-aws-storage-services/
└── 02-block-storage/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Amazon EBS provides persistent block storage volumes for use with Amazon EC2 instances. Block storage is essential for databases, file systems, and applications requiring low-latency access to data. Understanding EBS volume types and their use cases is crucial for the AWS CCP exam.

## Block Storage vs Object Storage

```
+------------------------------------------------------------------+
|              BLOCK STORAGE vs OBJECT STORAGE                      |
+------------------------------------------------------------------+
|                                                                   |
|   BLOCK STORAGE (EBS)              OBJECT STORAGE (S3)            |
|   +------------------+             +------------------+           |
|   | Block | Block |  |             |     Object 1     |           |
|   |-------+-------|  |             |   (Complete File) |           |
|   | Block | Block |  |             +------------------+           |
|   |-------+-------|  |             |     Object 2     |           |
|   | Block | Block |  |             |   (Complete File) |           |
|   +------------------+             +------------------+           |
|                                                                   |
|   - OS sees as disk               - Accessed via API              |
|   - Can be partitioned            - No file system needed         |
|   - Low latency I/O               - Unlimited scalability         |
|   - Attached to one EC2           - Accessible from anywhere      |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon EBS Overview

| Feature | Description |
|---------|-------------|
| Type | Network-attached block storage |
| Persistence | Data persists independently of EC2 instance |
| Attachment | Attached to one EC2 instance at a time (most types) |
| AZ Scope | Volumes are AZ-specific |
| Resizing | Can increase size without downtime |
| Encryption | Supports encryption at rest |

## EBS Volume Types

| Volume Type | Category | Use Case | Max IOPS | Max Throughput |
|-------------|----------|----------|----------|----------------|
| gp3 | General Purpose SSD | Most workloads | 16,000 | 1,000 MB/s |
| gp2 | General Purpose SSD | Boot volumes, dev/test | 16,000 | 250 MB/s |
| io2 Block Express | Provisioned IOPS SSD | Highest performance | 256,000 | 4,000 MB/s |
| io2/io1 | Provisioned IOPS SSD | Databases, critical apps | 64,000 | 1,000 MB/s |
| st1 | Throughput Optimized HDD | Big data, data warehouses | 500 | 500 MB/s |
| sc1 | Cold HDD | Infrequently accessed | 250 | 250 MB/s |

## EBS Volume Types Comparison

```
+------------------------------------------------------------------+
|                      EBS VOLUME TYPES                             |
+------------------------------------------------------------------+
|                                                                   |
|   PERFORMANCE (IOPS)                                              |
|   High  |  [io2 Block Express] - Mission-critical (256K IOPS)    |
|         |  [io2/io1]           - Databases (64K IOPS)            |
|         |  [gp3/gp2]           - General purpose (16K IOPS)      |
|         |  [st1]               - Throughput (500 IOPS)           |
|   Low   |  [sc1]               - Cold storage (250 IOPS)         |
|         +---------------------------------------------------->    |
|                               COST (Lower --->)                   |
|                                                                   |
|   SSD = IOPS-intensive     HDD = Throughput-intensive             |
|   (Databases, boot)        (Big data, sequential)                 |
|                                                                   |
+------------------------------------------------------------------+
```

## General Purpose SSD (gp3 vs gp2)

| Feature | gp3 | gp2 |
|---------|-----|-----|
| Baseline IOPS | 3,000 | 3 IOPS/GB (burst) |
| Max IOPS | 16,000 | 16,000 |
| Baseline Throughput | 125 MB/s | Varies with size |
| Max Throughput | 1,000 MB/s | 250 MB/s |
| IOPS/Throughput | Independently adjustable | Tied to volume size |
| Cost | 20% lower than gp2 | Higher |
| Recommendation | Preferred for new workloads | Legacy |

## Provisioned IOPS SSD (io1/io2)

| Feature | Description |
|---------|-------------|
| Use Case | Databases requiring sustained IOPS |
| IOPS | Provision exact IOPS needed |
| Durability | io2 provides 99.999% durability |
| Multi-Attach | io1/io2 can attach to multiple EC2 instances |
| Cost | Most expensive EBS option |

## Throughput Optimized HDD (st1)

| Feature | Description |
|---------|-------------|
| Use Case | Big data, data warehousing, log processing |
| Performance | Optimized for large, sequential I/O |
| Boot Volume | Cannot be used as boot volume |
| Cost | Lower than SSD options |

## Cold HDD (sc1)

| Feature | Description |
|---------|-------------|
| Use Case | Infrequently accessed data |
| Performance | Lowest cost HDD option |
| Boot Volume | Cannot be used as boot volume |
| Best For | Large volumes with minimal access |

## EBS Snapshots

| Feature | Description |
|---------|-------------|
| Definition | Point-in-time backup of EBS volume |
| Storage | Stored in S3 (managed by AWS) |
| Incremental | Only changed blocks are saved |
| Cross-Region | Can copy snapshots to other regions |
| Restore | Create new volume from snapshot |

```
+------------------------------------------------------------------+
|                       EBS SNAPSHOTS                               |
+------------------------------------------------------------------+
|                                                                   |
|   Initial Snapshot:          Incremental Snapshots:               |
|   +----------------+         +------+  +------+  +------+         |
|   | Full Volume    |         | Only |  | Only |  | Only |         |
|   | 100 GB         |         |Changed|  |Changed|  |Changed|        |
|   +----------------+         | 5 GB |  | 2 GB |  | 10 GB|         |
|                              +------+  +------+  +------+         |
|                              Snap 2    Snap 3    Snap 4           |
|                                                                   |
|   Benefits: Faster backups, Lower storage costs, Cross-region     |
|                                                                   |
+------------------------------------------------------------------+
```

## EBS Snapshot Features

| Feature | Description |
|---------|-------------|
| Fast Snapshot Restore | Immediately access restored volume at full performance |
| Snapshot Archive | Move snapshots to lower-cost archive tier |
| Recycle Bin | Protect against accidental deletion |
| Data Lifecycle Manager | Automate snapshot creation and retention |

## Instance Store (Ephemeral Storage)

| Feature | Description |
|---------|-------------|
| Type | Physically attached to host computer |
| Performance | Very high IOPS and throughput |
| Persistence | Data lost when instance stops/terminates |
| Cost | Included in instance price |
| Use Case | Temporary data, caches, buffers |

## EBS vs Instance Store

| Feature | EBS | Instance Store |
|---------|-----|----------------|
| Persistence | Persistent | Ephemeral |
| Connection | Network-attached | Physically attached |
| Performance | Good | Highest |
| Availability | Can detach/reattach | Tied to instance |
| Snapshots | Supported | Not supported |
| Data on Stop | Preserved | Lost |
| Data on Terminate | Optionally preserved | Lost |

```
+------------------------------------------------------------------+
|                  EBS vs INSTANCE STORE                            |
+------------------------------------------------------------------+
|                                                                   |
|   +----------+                          +----------+              |
|   |   EC2    |----Network--->           |   EC2    |              |
|   | Instance |                          | Instance |              |
|   +----------+                          +-----+----+              |
|        |                                      |                   |
|   +----v-----+                          +-----v----+              |
|   |   EBS    |                          | Instance |              |
|   |  Volume  |                          |   Store  |              |
|   +----------+                          +----------+              |
|   Network-attached                      Physically attached       |
|   Persistent                            Ephemeral                 |
|   Survives stop/start                   Lost on stop              |
|                                                                   |
+------------------------------------------------------------------+
```

## EBS Multi-Attach

| Feature | Description |
|---------|-------------|
| Volume Types | io1 and io2 only |
| Attachment | Same volume to multiple EC2 instances |
| Constraint | All instances must be in same AZ |
| Use Case | Clustered applications, high availability |

## EBS Encryption

| Feature | Description |
|---------|-------------|
| Method | AES-256 encryption |
| Key Management | AWS KMS (default or custom CMK) |
| At Rest | Data encrypted on volume |
| In Transit | Data encrypted between EC2 and EBS |
| Snapshots | Encrypted volumes produce encrypted snapshots |

## Exam Tips

- **gp3** = recommended general purpose SSD (independent IOPS/throughput)
- **gp2** = legacy general purpose SSD (IOPS scales with size)
- **io1/io2** = highest performance, provision IOPS, for databases
- **st1** = throughput optimized HDD, big data, sequential reads
- **sc1** = cold HDD, lowest cost, infrequent access
- **HDD volumes (st1, sc1)** = cannot be boot volumes
- **EBS volumes** = AZ-specific, can only attach to instances in same AZ
- **Snapshots** = stored in S3, incremental, cross-region copy supported
- **Instance Store** = highest performance, ephemeral (data lost on stop)
- **Multi-Attach** = io1/io2 volumes can attach to multiple instances
- **Encryption** = uses AWS KMS, encrypts data at rest and in transit

## Key Terms

| Term | Definition |
|------|------------|
| Block Storage | Storage accessed as fixed-size blocks (like a hard drive) |
| EBS Volume | Network-attached persistent block storage |
| IOPS | Input/Output Operations Per Second |
| Throughput | Data transfer rate (MB/s) |
| Snapshot | Point-in-time incremental backup of a volume |
| Instance Store | Ephemeral storage physically attached to EC2 host |
| Provisioned IOPS | Pre-allocated performance level for consistent I/O |
| Multi-Attach | Ability to attach one volume to multiple instances |

## Key Takeaways

1. EBS provides persistent, network-attached block storage for EC2
2. Volume types range from high-performance SSD (io2) to low-cost HDD (sc1)
3. gp3 is the recommended general purpose SSD with independent IOPS/throughput settings
4. io1/io2 volumes are for databases requiring consistent, high IOPS
5. HDD volumes (st1, sc1) are for throughput-intensive, sequential workloads
6. Snapshots are incremental, stored in S3, and can be copied cross-region
7. Instance Store provides highest performance but data is ephemeral
8. EBS volumes are AZ-specific and typically attach to one instance

---

*Previous: [01 - Object Storage](../01-object-storage/readme.md) | Next: [03 - File Storage](../03-file-storage/readme.md)*

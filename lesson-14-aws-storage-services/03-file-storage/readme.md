# Amazon EFS and FSx (File Storage)

## File Structure

```
lesson-14-aws-storage-services/
└── 03-file-storage/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides managed file storage services that allow multiple compute instances to access shared file systems simultaneously. Amazon EFS offers scalable NFS storage for Linux workloads, while Amazon FSx provides fully managed file systems for various use cases including Windows and high-performance computing.

## File Storage Overview

```
+------------------------------------------------------------------+
|                        FILE STORAGE                               |
+------------------------------------------------------------------+
|                                                                   |
|              +------------------+                                 |
|              |   File System    |                                 |
|              | /home/data/      |                                 |
|              | /logs/           |                                 |
|              | /shared/         |                                 |
|              +--------+---------+                                 |
|                       |                                           |
|         +-------------+-------------+                             |
|         |             |             |                             |
|   +-----v-----+ +-----v-----+ +-----v-----+                       |
|   |   EC2-1   | |   EC2-2   | |   EC2-3   |                       |
|   | (Web Svr) | | (App Svr) | | (Worker)  |                       |
|   +-----------+ +-----------+ +-----------+                       |
|                                                                   |
|   Multiple instances access the SAME file system concurrently    |
|                                                                   |
+------------------------------------------------------------------+
```

## Storage Types Comparison

| Type | How It Works | Access | Use Case |
|------|--------------|--------|----------|
| Block (EBS) | Raw storage blocks | Single instance | Databases, OS |
| Object (S3) | Complete objects via API | Unlimited via HTTP | Media, backups |
| File (EFS/FSx) | Hierarchical file system | Multiple instances | Shared data |

## Amazon EFS (Elastic File System)

| Feature | Description |
|---------|-------------|
| Type | Fully managed NFS file system |
| Protocol | NFSv4 |
| Scalability | Automatically grows/shrinks |
| Availability | Multi-AZ by default (Regional) |
| Compatibility | Linux-based instances only |
| Access | Thousands of concurrent connections |

## EFS Architecture

```
+------------------------------------------------------------------+
|                      AMAZON EFS                                   |
+------------------------------------------------------------------+
|                                                                   |
|                    +-------------------+                          |
|                    |    EFS File       |                          |
|                    |    System         |                          |
|                    +-------------------+                          |
|                            |                                      |
|         +------------------+------------------+                   |
|         |                  |                  |                   |
|   +-----v-----+      +-----v-----+      +-----v-----+             |
|   | Mount     |      | Mount     |      | Mount     |             |
|   | Target    |      | Target    |      | Target    |             |
|   | (AZ-1)    |      | (AZ-2)    |      | (AZ-3)    |             |
|   +-----+-----+      +-----+-----+      +-----+-----+             |
|         |                  |                  |                   |
|   +-----v-----+      +-----v-----+      +-----v-----+             |
|   | EC2       |      | EC2       |      | EC2       |             |
|   | Instances |      | Instances |      | Instances |             |
|   +-----------+      +-----------+      +-----------+             |
|                                                                   |
|   Mount targets in each AZ provide high availability             |
|                                                                   |
+------------------------------------------------------------------+
```

## EFS Storage Classes

| Storage Class | Description | Use Case |
|---------------|-------------|----------|
| Standard | Frequently accessed data | Active workloads |
| Standard-IA | Infrequent Access | Older files, archives |
| One Zone | Single AZ storage | Dev/test, cost savings |
| One Zone-IA | Single AZ + Infrequent Access | Lowest cost option |

## EFS Performance Modes

| Mode | Description | Use Case |
|------|-------------|----------|
| General Purpose | Default, low latency | Web servers, CMS |
| Max I/O | Higher latency, higher throughput | Big data, media processing |

## EFS Throughput Modes

| Mode | Description | Use Case |
|------|-------------|----------|
| Bursting | Throughput scales with size | Variable workloads |
| Provisioned | Set throughput independently | Consistent throughput needs |
| Elastic | Automatically scales throughput | Unpredictable workloads |

## EFS Lifecycle Management

| Feature | Description |
|---------|-------------|
| Purpose | Automatically move files to IA storage |
| Trigger | Based on last access time |
| Options | 7, 14, 30, 60, or 90 days |
| Cost Savings | Up to 92% lower cost for IA storage |

## Amazon FSx Overview

| FSx Option | Description | Use Case |
|------------|-------------|----------|
| FSx for Windows File Server | Windows native SMB file system | Windows apps, AD integration |
| FSx for Lustre | High-performance parallel file system | HPC, ML training, media |
| FSx for NetApp ONTAP | NetApp ONTAP file system | Enterprise apps, hybrid |
| FSx for OpenZFS | OpenZFS file system | Linux workloads, migration |

## FSx Comparison

```
+------------------------------------------------------------------+
|                      AMAZON FSx OPTIONS                           |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------------+    +------------------------+        |
|   | FSx for Windows        |    | FSx for Lustre         |        |
|   | File Server            |    |                        |        |
|   |------------------------|    |------------------------|        |
|   | - SMB protocol         |    | - POSIX-compliant      |        |
|   | - Active Directory     |    | - Sub-millisecond      |        |
|   | - Windows NTFS         |    |   latency              |        |
|   | - Quotas, shadow       |    | - Hundreds of GB/s     |        |
|   |   copies               |    |   throughput           |        |
|   | - DFS namespaces       |    | - S3 integration       |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
|   +------------------------+    +------------------------+        |
|   | FSx for NetApp ONTAP   |    | FSx for OpenZFS        |        |
|   |------------------------|    |------------------------|        |
|   | - Multi-protocol       |    | - ZFS features         |        |
|   |   (NFS, SMB, iSCSI)    |    | - Snapshots, clones    |        |
|   | - SnapMirror, FlexClone|    | - Data compression     |        |
|   | - Data tiering         |    | - Linux migration      |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## FSx for Windows File Server

| Feature | Description |
|---------|-------------|
| Protocol | SMB (Server Message Block) |
| Integration | Active Directory (AWS or self-managed) |
| Features | Shadow copies, quotas, DFS |
| Access | Windows and Linux clients |
| Availability | Single-AZ or Multi-AZ |

## FSx for Lustre

| Feature | Description |
|---------|-------------|
| Performance | Sub-millisecond latency |
| Throughput | Up to hundreds of GB/s |
| IOPS | Millions of IOPS |
| S3 Integration | Read from and write to S3 |
| Use Cases | HPC, ML training, video processing |

## Deployment Options

| Option | Description |
|--------|-------------|
| Scratch | Temporary storage, highest performance |
| Persistent | Long-term storage, data replicated |

## EFS vs FSx Comparison

| Feature | EFS | FSx for Windows | FSx for Lustre |
|---------|-----|-----------------|----------------|
| Protocol | NFS | SMB | POSIX |
| OS Support | Linux | Windows & Linux | Linux |
| Use Case | Linux shared storage | Windows apps | HPC/ML |
| Performance | Good | Good | Highest |
| AD Integration | No | Yes | No |

## When to Use Each File Storage

```
+------------------------------------------------------------------+
|                  CHOOSING FILE STORAGE                            |
+------------------------------------------------------------------+
|                                                                   |
|   Need shared Linux file storage?                                 |
|   ---> Amazon EFS                                                 |
|                                                                   |
|   Need Windows file shares with AD?                               |
|   ---> FSx for Windows File Server                                |
|                                                                   |
|   Need high-performance computing (HPC)?                          |
|   ---> FSx for Lustre                                             |
|                                                                   |
|   Migrating from on-premises NetApp?                              |
|   ---> FSx for NetApp ONTAP                                       |
|                                                                   |
|   Migrating Linux ZFS workloads?                                  |
|   ---> FSx for OpenZFS                                            |
|                                                                   |
+------------------------------------------------------------------+
```

## Exam Tips

- **EFS** = managed NFS for Linux, automatically scales, multi-AZ
- **EFS Standard** = frequently accessed files, higher cost
- **EFS IA** = infrequently accessed, lower cost with retrieval fees
- **EFS** = only works with Linux (NFSv4), NOT Windows
- **FSx for Windows** = SMB protocol, Active Directory integration
- **FSx for Lustre** = HPC, ML training, sub-millisecond latency
- **FSx for Lustre + S3** = can present S3 data as a file system
- **EFS vs EBS** = EFS is shared (multi-instance), EBS is single instance
- **Mount targets** = EFS needs mount target in each AZ for access
- **Lifecycle policies** = automatically move EFS files to IA storage

## Key Terms

| Term | Definition |
|------|------------|
| File Storage | Hierarchical storage accessed via file system protocols |
| NFS | Network File System, standard Linux file sharing protocol |
| SMB | Server Message Block, Windows file sharing protocol |
| Mount Target | Network endpoint for EFS access in an AZ |
| Lustre | High-performance parallel file system for HPC |
| Active Directory | Microsoft directory service for user/resource management |
| POSIX | Portable Operating System Interface, Unix standard |
| Throughput | Rate of data transfer (measured in MB/s or GB/s) |

## Key Takeaways

1. EFS provides scalable, managed NFS storage for Linux workloads
2. EFS supports thousands of concurrent connections across multiple AZs
3. EFS lifecycle management automatically moves files to lower-cost IA storage
4. FSx for Windows File Server provides native SMB with AD integration
5. FSx for Lustre delivers sub-millisecond latency for HPC and ML workloads
6. FSx for Lustre can integrate directly with S3 for data processing
7. EFS automatically grows and shrinks based on usage
8. Choose file storage when multiple instances need concurrent access to the same data

---

*Previous: [02 - Block Storage](../02-block-storage/readme.md) | Next: [04 - Hybrid and Edge Storage](../04-hybrid-and-edge-storage/readme.md)*

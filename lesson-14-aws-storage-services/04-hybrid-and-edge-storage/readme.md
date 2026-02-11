# Hybrid and Edge Storage

## Introduction

AWS provides solutions for extending cloud storage capabilities to on-premises environments and edge locations. AWS Storage Gateway enables hybrid cloud storage, while the AWS Snow Family provides physical devices for edge computing and massive data transfers. These services are essential for migrations, hybrid architectures, and disconnected environments.

## Hybrid Storage Architecture

```
+------------------------------------------------------------------+
|                    HYBRID STORAGE                                 |
+------------------------------------------------------------------+
|                                                                   |
|   ON-PREMISES                              AWS CLOUD              |
|   +-----------------+                  +-------------------+      |
|   |  Data Center    |                  |                   |      |
|   |  +----------+   |                  |  +-------------+  |      |
|   |  | Servers  |   |                  |  |     S3      |  |      |
|   |  +----+-----+   |     Internet     |  +-------------+  |      |
|   |       |         |    or Direct     |                   |      |
|   |  +----v------+  |     Connect      |  +-------------+  |      |
|   |  | Storage   |<--------------------->|    EBS      |  |      |
|   |  | Gateway   |  |                  |  +-------------+  |      |
|   |  +-----------+  |                  |                   |      |
|   +-----------------+                  |  +-------------+  |      |
|                                        |  |   Glacier   |  |      |
|                                        |  +-------------+  |      |
|                                        +-------------------+      |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Storage Gateway

| Feature | Description |
|---------|-------------|
| Purpose | Hybrid cloud storage integration |
| Function | Connects on-premises to AWS storage |
| Deployment | VM or hardware appliance |
| Caching | Local cache for low-latency access |
| Protocols | NFS, SMB, iSCSI, iSCSI-VTL |

## Storage Gateway Types

| Type | Protocol | Backend | Use Case |
|------|----------|---------|----------|
| S3 File Gateway | NFS, SMB | S3 | File shares backed by S3 |
| FSx File Gateway | SMB | FSx for Windows | Windows file shares |
| Volume Gateway | iSCSI | S3, EBS | Block storage, backups |
| Tape Gateway | iSCSI-VTL | S3 Glacier | Tape backup replacement |

## Storage Gateway Types Diagram

```
+------------------------------------------------------------------+
|                   STORAGE GATEWAY TYPES                           |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------------+    +------------------------+        |
|   | S3 FILE GATEWAY        |    | FSx FILE GATEWAY       |        |
|   |------------------------|    |------------------------|        |
|   | NFS/SMB --> S3         |    | SMB --> FSx Windows    |        |
|   | - File shares          |    | - Windows file shares  |        |
|   | - Data lakes           |    | - Active Directory     |        |
|   | - Backups              |    | - Low-latency cache    |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
|   +------------------------+    +------------------------+        |
|   | VOLUME GATEWAY         |    | TAPE GATEWAY           |        |
|   |------------------------|    |------------------------|        |
|   | iSCSI --> S3/EBS       |    | VTL --> S3 Glacier     |        |
|   | - Stored Volumes       |    | - Replace tape backup  |        |
|   |   (full local copy)    |    | - Virtual tapes        |        |
|   | - Cached Volumes       |    | - Archive to Glacier   |        |
|   |   (primary in cloud)   |    |                        |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## S3 File Gateway

| Feature | Description |
|---------|-------------|
| Protocol | NFS v3/v4.1, SMB |
| Storage | Objects in S3 |
| Cache | Local cache for recently accessed data |
| Use Case | File shares, data lakes, backups |
| S3 Classes | All S3 storage classes supported |

## FSx File Gateway

| Feature | Description |
|---------|-------------|
| Protocol | SMB |
| Storage | FSx for Windows File Server |
| Cache | Local cache for frequently accessed data |
| Use Case | Windows workloads needing low-latency access |
| Integration | Active Directory |

## Volume Gateway

| Mode | Description | Data Location |
|------|-------------|---------------|
| Cached Volumes | Primary data in S3, cache locally | Cloud (S3) |
| Stored Volumes | Primary data local, async backup to S3 | On-premises |

| Feature | Description |
|---------|-------------|
| Protocol | iSCSI |
| Snapshots | EBS snapshots stored in S3 |
| Recovery | Create EBS volumes from snapshots |

## Tape Gateway

| Feature | Description |
|---------|-------------|
| Purpose | Replace physical tape backup infrastructure |
| Protocol | iSCSI VTL (Virtual Tape Library) |
| Storage | Virtual tapes stored in S3 |
| Archive | Tapes archived to S3 Glacier |
| Compatibility | Works with existing backup software |

## AWS Snow Family

| Device | Storage | Compute | Use Case |
|--------|---------|---------|----------|
| Snowcone | 8-14 TB | Optional | Edge computing, small transfers |
| Snowball Edge Storage | 80 TB | Optional | Large data transfers |
| Snowball Edge Compute | 42 TB | Yes | Edge computing + storage |
| Snowmobile | 100 PB | No | Exabyte-scale migration |

## Snow Family Comparison

```
+------------------------------------------------------------------+
|                      AWS SNOW FAMILY                              |
+------------------------------------------------------------------+
|                                                                   |
|   STORAGE CAPACITY                                                |
|                                                                   |
|   +----------+   Snowcone (8-14 TB)                               |
|   |  Small   |   - Portable, rugged                               |
|   |  Device  |   - Edge computing optional                        |
|   +----------+   - Fits in a backpack                             |
|                                                                   |
|   +--------------+   Snowball Edge (42-80 TB)                     |
|   |    Medium    |   - Storage Optimized (80 TB)                  |
|   |    Device    |   - Compute Optimized (42 TB)                  |
|   +--------------+   - Edge computing capabilities                |
|                                                                   |
|   +------------------+   Snowmobile (100 PB)                      |
|   |     Shipping     |   - Semi-trailer truck                     |
|   |     Container    |   - Exabyte-scale transfers                |
|   +------------------+   - AWS personnel operated                 |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Snowcone

| Feature | Description |
|---------|-------------|
| Size | Smallest Snow device, 4.5 lbs |
| Storage | 8 TB HDD or 14 TB SSD |
| Compute | Optional EC2 instances |
| Connectivity | WiFi, ethernet |
| Transfer | DataSync agent pre-installed |
| Use Case | Edge locations, tactical edge |

## AWS Snowball Edge

| Variant | Storage | Compute | Use Case |
|---------|---------|---------|----------|
| Storage Optimized | 80 TB | 40 vCPUs | Large data transfers |
| Compute Optimized | 42 TB | 52 vCPUs, GPU optional | Edge ML, processing |

| Feature | Description |
|---------|-------------|
| Clustering | Up to 15 devices for increased capacity |
| Services | Run EC2 and Lambda at the edge |
| Use Case | Data migration, edge computing, disaster recovery |

## AWS Snowmobile

| Feature | Description |
|---------|-------------|
| Capacity | Up to 100 PB per Snowmobile |
| Size | 45-foot shipping container |
| Security | GPS, alarm, 24/7 video, escort |
| Transfer | Multi-petabyte migrations |
| Use Case | Data center migration, exabyte-scale |

## Snow Family Data Transfer Process

```
+------------------------------------------------------------------+
|                 SNOW FAMILY DATA TRANSFER                         |
+------------------------------------------------------------------+
|                                                                   |
|   1. Order          2. Load Data       3. Ship to AWS             |
|   +----------+      +----------+       +----------+               |
|   | Request  |----->| Copy to  |------>| Return   |               |
|   | Device   |      | Device   |       | Device   |               |
|   +----------+      +----------+       +----------+               |
|                                               |                   |
|                                               v                   |
|                     4. AWS Imports      +----------+              |
|                        to S3            |   S3     |              |
|                                         | Bucket   |              |
|                                         +----------+              |
|                                                                   |
|   Device is securely erased after import                         |
|                                                                   |
+------------------------------------------------------------------+
```

## Edge Computing with Snow

| Feature | Description |
|---------|-------------|
| Purpose | Process data at edge before transfer |
| Services | EC2, Lambda, IoT Greengrass |
| Benefits | Reduce data transfer, real-time processing |
| Use Cases | ML inference, data preprocessing, IoT |

## When to Use Snow Family

| Scenario | Recommended Solution |
|----------|---------------------|
| < 10 TB | Use internet or Direct Connect |
| 10 TB - 80 TB | Snowball Edge |
| 80 TB - 500 TB | Multiple Snowball Edge |
| > 500 TB | Snowmobile |
| Edge computing needed | Snowball Edge Compute |
| Remote/tactical locations | Snowcone |

## AWS DataSync

| Feature | Description |
|---------|-------------|
| Purpose | Online data transfer service |
| Speed | Up to 10x faster than open-source tools |
| Sources | NFS, SMB, HDFS, self-managed storage |
| Destinations | S3, EFS, FSx |
| Scheduling | Automated, scheduled transfers |

## Storage Gateway vs DataSync

| Feature | Storage Gateway | DataSync |
|---------|----------------|----------|
| Type | Hybrid cloud storage | Data transfer service |
| Use | Ongoing hybrid access | One-time or scheduled migrations |
| Protocol | File, block, tape | NFS, SMB |
| Destination | S3, Glacier, EBS | S3, EFS, FSx |

## Exam Tips

- **Storage Gateway** = connects on-premises to AWS storage
- **S3 File Gateway** = NFS/SMB file shares backed by S3
- **FSx File Gateway** = SMB shares for FSx for Windows
- **Volume Gateway** = iSCSI block storage (cached or stored)
- **Tape Gateway** = replace physical tape with virtual tapes in S3/Glacier
- **Snowcone** = smallest (8-14 TB), edge computing, portable
- **Snowball Edge** = medium (42-80 TB), storage or compute optimized
- **Snowmobile** = largest (100 PB), for exabyte-scale migrations
- **Snow devices** = physical data transfer when network is too slow
- **DataSync** = fast online transfer between on-premises and AWS
- **Snowball Edge Compute** = run EC2 and Lambda at the edge

## Key Terms

| Term | Definition |
|------|------------|
| Hybrid Cloud | Architecture using both on-premises and cloud resources |
| Storage Gateway | Service connecting on-premises storage to AWS |
| Virtual Tape Library (VTL) | Virtualized tape backup infrastructure |
| Snow Family | Physical devices for data transfer and edge computing |
| Edge Computing | Processing data at the network edge |
| DataSync | Service for automated online data transfer |
| Cached Volumes | Block storage with primary data in cloud |
| Stored Volumes | Block storage with primary data on-premises |

## Key Takeaways

1. Storage Gateway provides hybrid cloud storage with local caching
2. S3 File Gateway exposes S3 objects as NFS/SMB file shares
3. Tape Gateway replaces physical tape infrastructure with virtual tapes
4. Snow Family enables physical data transfer for large datasets
5. Snowcone is portable (8-14 TB), Snowball Edge is medium (42-80 TB), Snowmobile is massive (100 PB)
6. Snowball Edge supports edge computing with EC2 and Lambda
7. Use Snow devices when network transfer would take weeks/months
8. DataSync provides fast online transfer for migrations

---

*Previous: [03 - File Storage](../03-file-storage/readme.md) | Next: [05 - Backup and Recovery](../05-backup-and-recovery/readme.md)*

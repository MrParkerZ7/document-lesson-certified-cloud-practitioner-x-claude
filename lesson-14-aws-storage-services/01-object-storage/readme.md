# Amazon S3 (Simple Storage Service)

## File Structure

```
lesson-14-aws-storage-services/
└── 01-object-storage/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Amazon S3 is AWS's flagship object storage service, designed for unlimited scalability, high durability (99.999999999% - 11 nines), and availability. S3 stores data as objects within buckets and is ideal for storing any amount of data from anywhere on the web. Understanding S3 storage classes and features is essential for the AWS CCP exam.

## What is Object Storage?

```
+------------------------------------------------------------------+
|                        OBJECT STORAGE                             |
+------------------------------------------------------------------+
|                                                                   |
|   Object = Data + Metadata + Unique Identifier                    |
|                                                                   |
|   +---------------------------------------------------------+    |
|   |                      S3 BUCKET                          |    |
|   |  +------------+  +------------+  +------------+         |    |
|   |  | Object 1   |  | Object 2   |  | Object 3   |         |    |
|   |  | image.png  |  | video.mp4  |  | data.csv   |         |    |
|   |  | 2.5 MB     |  | 500 MB     |  | 100 KB     |         |    |
|   |  | Metadata   |  | Metadata   |  | Metadata   |         |    |
|   |  +------------+  +------------+  +------------+         |    |
|   +---------------------------------------------------------+    |
|                                                                   |
|   Flat structure (no folders - uses prefixes for organization)   |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon S3 Core Concepts

| Concept | Description |
|---------|-------------|
| Bucket | Container for objects, globally unique name |
| Object | File + metadata stored in a bucket |
| Key | Unique identifier for an object within a bucket |
| Region | Buckets are created in a specific AWS region |
| Object Size | 0 bytes to 5 TB per object |
| Storage | Unlimited total storage |

## S3 Storage Classes

| Storage Class | Use Case | Availability | Min Storage Duration |
|---------------|----------|--------------|---------------------|
| S3 Standard | Frequently accessed data | 99.99% | None |
| S3 Intelligent-Tiering | Unknown/changing access patterns | 99.9% | None |
| S3 Standard-IA | Infrequently accessed, rapid access needed | 99.9% | 30 days |
| S3 One Zone-IA | Infrequent access, single AZ, recreatable data | 99.5% | 30 days |
| S3 Glacier Instant Retrieval | Archive with millisecond retrieval | 99.9% | 90 days |
| S3 Glacier Flexible Retrieval | Archive with minutes to hours retrieval | 99.99% | 90 days |
| S3 Glacier Deep Archive | Long-term archive, lowest cost | 99.99% | 180 days |

## Storage Classes Comparison

```
+------------------------------------------------------------------+
|                    S3 STORAGE CLASSES                             |
+------------------------------------------------------------------+
|                                                                   |
|   ACCESS FREQUENCY                                                |
|   High  |  [S3 Standard]         - Frequently accessed            |
|         |                                                         |
|         |  [Intelligent-Tiering] - Auto-moves between tiers       |
|         |                                                         |
|         |  [Standard-IA]         - Infrequent, quick retrieval    |
|         |                                                         |
|         |  [One Zone-IA]         - Infrequent, single AZ          |
|         |                                                         |
|         |  [Glacier Instant]     - Archive, instant access        |
|         |                                                         |
|         |  [Glacier Flexible]    - Archive, mins-hours retrieval  |
|         |                                                         |
|   Low   |  [Glacier Deep Archive]- Long-term, lowest cost         |
|         +---------------------------------------------------->    |
|                               COST (Lower --->)                   |
|                                                                   |
+------------------------------------------------------------------+
```

## S3 Glacier Retrieval Options

| Retrieval Type | Glacier Flexible | Glacier Deep Archive |
|----------------|------------------|---------------------|
| Expedited | 1-5 minutes | N/A |
| Standard | 3-5 hours | 12 hours |
| Bulk | 5-12 hours | 48 hours |

## S3 Versioning

| Feature | Description |
|---------|-------------|
| Purpose | Keep multiple versions of an object |
| State | Disabled, Enabled, or Suspended |
| Protection | Protects against accidental deletion |
| Delete Marker | Soft delete, can be restored |
| Storage Cost | Each version consumes storage |

```
+------------------------------------------------------------------+
|                      S3 VERSIONING                                |
+------------------------------------------------------------------+
|                                                                   |
|   Without Versioning:          With Versioning:                   |
|   +----------------+           +----------------+                 |
|   | document.pdf   |           | document.pdf   |                 |
|   | (overwritten)  |           | Version ID: v3 | <-- Current     |
|   +----------------+           +----------------+                 |
|                                | document.pdf   |                 |
|                                | Version ID: v2 |                 |
|                                +----------------+                 |
|                                | document.pdf   |                 |
|                                | Version ID: v1 |                 |
|                                +----------------+                 |
|                                                                   |
+------------------------------------------------------------------+
```

## S3 Lifecycle Policies

| Action | Description |
|--------|-------------|
| Transition | Move objects between storage classes |
| Expiration | Delete objects after specified time |
| Abort Incomplete Uploads | Clean up incomplete multipart uploads |
| Noncurrent Version Expiration | Delete old versions |

```
+------------------------------------------------------------------+
|                   S3 LIFECYCLE POLICY                             |
+------------------------------------------------------------------+
|                                                                   |
|   Day 0              Day 30              Day 90        Day 365    |
|   +----------+       +------------+      +----------+  +--------+ |
|   | Standard |  -->  | Standard-IA|  --> | Glacier  |->| Delete | |
|   +----------+       +------------+      +----------+  +--------+ |
|                                                                   |
|   Automatically move data to cheaper storage as it ages          |
|                                                                   |
+------------------------------------------------------------------+
```

## S3 Security Features

| Feature | Description |
|---------|-------------|
| Bucket Policies | JSON-based access policies on buckets |
| ACLs | Legacy access control at object/bucket level |
| Block Public Access | Account/bucket-level settings to prevent public access |
| Encryption | SSE-S3, SSE-KMS, SSE-C, client-side |
| Presigned URLs | Temporary access to private objects |

## S3 Encryption Options

| Type | Key Management | Description |
|------|----------------|-------------|
| SSE-S3 | AWS managed | Default encryption, Amazon manages keys |
| SSE-KMS | AWS KMS | You control keys in KMS, audit trail |
| SSE-C | Customer provided | You provide and manage encryption keys |
| Client-Side | Customer managed | Encrypt before uploading |

## S3 Access Points

| Feature | Description |
|---------|-------------|
| Purpose | Simplify data access at scale |
| Function | Named network endpoints with specific permissions |
| Use Case | Different access policies for different applications |

## S3 Replication

| Type | Description | Use Case |
|------|-------------|----------|
| Same-Region Replication (SRR) | Replicate within same region | Compliance, log aggregation |
| Cross-Region Replication (CRR) | Replicate across regions | DR, latency reduction |

## S3 Event Notifications

| Feature | Description |
|---------|-------------|
| Triggers | Object created, deleted, restored, etc. |
| Destinations | Lambda, SNS, SQS, EventBridge |
| Use Cases | Process uploads, trigger workflows |

## S3 Transfer Acceleration

| Feature | Description |
|---------|-------------|
| Purpose | Fast uploads over long distances |
| How | Uses CloudFront edge locations |
| Use Case | Global users uploading to centralized bucket |

## Exam Tips

- **S3 Standard** = frequently accessed data, highest availability
- **S3 Standard-IA** = infrequent access but needs millisecond retrieval
- **S3 One Zone-IA** = infrequent access, single AZ, lower cost, recreatable data
- **S3 Intelligent-Tiering** = auto-moves objects, no retrieval fees
- **S3 Glacier Instant Retrieval** = archive with millisecond access
- **S3 Glacier Flexible Retrieval** = archive, minutes to hours retrieval
- **S3 Glacier Deep Archive** = lowest cost, 12-48 hour retrieval
- **Versioning** = protect against accidental deletion/overwrite
- **Lifecycle Policies** = automate transitions and deletions
- **S3 durability** = 99.999999999% (11 nines) for all storage classes
- **Object size limit** = 5 TB max per object
- **Bucket names** = globally unique across all AWS accounts

## Key Terms

| Term | Definition |
|------|------------|
| Object Storage | Storage architecture for unstructured data as objects |
| Bucket | Container for S3 objects with globally unique name |
| Storage Class | Different tiers for cost/access optimization |
| Lifecycle Policy | Rules to automatically transition or expire objects |
| Versioning | Keeping multiple versions of objects |
| Durability | Probability that data will not be lost |
| Availability | Percentage of time data is accessible |
| Glacier | Archival storage class for infrequently accessed data |

## Key Takeaways

1. S3 is AWS's unlimited, highly durable object storage service
2. Storage classes range from Standard (frequent access) to Glacier Deep Archive (long-term archive)
3. All storage classes provide 11 nines (99.999999999%) durability
4. Versioning protects against accidental deletion and overwrites
5. Lifecycle policies automate cost optimization by transitioning objects
6. S3 Intelligent-Tiering automatically moves objects between tiers
7. Glacier classes are for archival with varying retrieval times (instant to 48 hours)
8. Cross-Region Replication provides disaster recovery and latency benefits

---

*Next: [02 - Block Storage](../02-block-storage/readme.md)*

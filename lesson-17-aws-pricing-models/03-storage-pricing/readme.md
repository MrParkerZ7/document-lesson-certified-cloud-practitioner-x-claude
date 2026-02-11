# 💰 Storage Pricing

## Introduction

AWS storage pricing varies significantly based on the service, storage class, access patterns, and data retrieval requirements. Understanding these pricing models is essential for optimizing storage costs while meeting performance and availability requirements.

## S3 Storage Classes and Pricing

```
+------------------------------------------------------------------+
|                    S3 STORAGE CLASS TIERS                         |
+------------------------------------------------------------------+
|                                                                   |
|   COST PER GB                    ACCESS FREQUENCY                 |
|   High ^                                                          |
|        |  [S3 Standard]         - Frequent access                 |
|        |                                                          |
|        |  [S3 Standard-IA]      - Infrequent access               |
|        |                                                          |
|        |  [S3 One Zone-IA]      - Infrequent, single AZ           |
|        |                                                          |
|        |  [S3 Glacier Instant]  - Archive, milliseconds retrieval |
|        |                                                          |
|        |  [S3 Glacier Flexible] - Archive, minutes to hours       |
|        |                                                          |
|   Low  |  [S3 Glacier Deep]     - Archive, 12-48 hours            |
|        +----------------------------------------------------->    |
|               Frequent                          Rare              |
|                                                                   |
+------------------------------------------------------------------+
```

## S3 Storage Classes Comparison

| Storage Class | Use Case | Availability | Min Storage | Retrieval Fee |
|---------------|----------|--------------|-------------|---------------|
| S3 Standard | Frequently accessed data | 99.99% | None | None |
| S3 Intelligent-Tiering | Unknown/changing access | 99.9% | None | None (monitoring fee) |
| S3 Standard-IA | Infrequent access, rapid retrieval | 99.9% | 30 days | Per GB retrieved |
| S3 One Zone-IA | Infrequent, reproducible data | 99.5% | 30 days | Per GB retrieved |
| S3 Glacier Instant | Archive, instant access | 99.9% | 90 days | Per GB retrieved |
| S3 Glacier Flexible | Archive, minutes to hours | 99.99% | 90 days | Per GB + request |
| S3 Glacier Deep Archive | Long-term archive | 99.99% | 180 days | Per GB + request |

## S3 Pricing Components

```
+------------------------------------------------------------------+
|                    S3 PRICING COMPONENTS                          |
+------------------------------------------------------------------+
|                                                                   |
|   Your S3 Bill = Storage + Requests + Data Transfer + Features    |
|                                                                   |
|   +---------------+  +---------------+  +---------------+         |
|   | STORAGE       |  | REQUESTS      |  | DATA TRANSFER |         |
|   | - Per GB/month|  | - PUT, COPY   |  | - OUT to      |         |
|   | - Varies by   |  | - GET, SELECT |  |   Internet    |         |
|   |   class       |  | - Lifecycle   |  | - Cross-region|         |
|   +---------------+  +---------------+  +---------------+         |
|                                                                   |
|   +---------------+  +---------------+                            |
|   | RETRIEVAL     |  | FEATURES      |                            |
|   | - From IA/    |  | - Analytics   |                            |
|   |   Glacier     |  | - Inventory   |                            |
|   | - Per GB      |  | - Replication |                            |
|   +---------------+  +---------------+                            |
|                                                                   |
+------------------------------------------------------------------+
```

## S3 Pricing Details

| Component | What You Pay For | Pricing Model |
|-----------|-----------------|---------------|
| Storage | Data stored per month | Per GB-month |
| PUT/COPY/POST/LIST | Write and list requests | Per 1,000 requests |
| GET/SELECT | Read requests | Per 1,000 requests |
| Data Transfer OUT | Data leaving AWS | Per GB (tiered) |
| Data Retrieval | Retrieving from IA/Glacier | Per GB |
| Lifecycle Transitions | Moving between classes | Per 1,000 objects |

## S3 Intelligent-Tiering

Automatically moves data between tiers based on access patterns.

```
+------------------------------------------------------------------+
|                 S3 INTELLIGENT-TIERING                            |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+                                            |
|   | Frequent Access  |  <-- Objects accessed                      |
|   | (Standard cost)  |                                            |
|   +--------+---------+                                            |
|            |                                                      |
|            v  30 days no access                                   |
|   +------------------+                                            |
|   | Infrequent       |  <-- Auto-moved                            |
|   | Access           |                                            |
|   +--------+---------+                                            |
|            |                                                      |
|            v  90 days no access                                   |
|   +------------------+                                            |
|   | Archive Instant  |  <-- Auto-moved (optional)                 |
|   | Access           |                                            |
|   +--------+---------+                                            |
|            |                                                      |
|            v  180 days no access                                  |
|   +------------------+                                            |
|   | Deep Archive     |  <-- Auto-moved (optional)                 |
|   +------------------+                                            |
|                                                                   |
|   Cost: Small monthly monitoring fee per object                   |
|   Benefit: No retrieval fees when accessed                        |
|                                                                   |
+------------------------------------------------------------------+
```

## S3 Glacier Retrieval Options

| Retrieval Option | Glacier Flexible | Glacier Deep Archive | Time |
|------------------|-----------------|---------------------|------|
| Expedited | Available | Not available | 1-5 minutes |
| Standard | Available | Available | 3-5 hours / 12 hours |
| Bulk | Available | Available | 5-12 hours / 48 hours |

**Note:** Faster retrieval = Higher cost

## EBS Volume Pricing

```
+------------------------------------------------------------------+
|                     EBS VOLUME TYPES                              |
+------------------------------------------------------------------+
|                                                                   |
|   PERFORMANCE                                                     |
|   High ^                                                          |
|        |  [io2 Block Express]  - Highest IOPS, mission-critical   |
|        |                                                          |
|        |  [io2/io1]            - High IOPS, databases             |
|        |                                                          |
|        |  [gp3/gp2]            - Balanced price/performance       |
|        |                                                          |
|        |  [st1]                - Throughput optimized HDD         |
|        |                                                          |
|   Low  |  [sc1]                - Cold HDD, infrequent access      |
|        +----------------------------------------------------->    |
|                Low                              High   COST       |
|                                                                   |
+------------------------------------------------------------------+
```

## EBS Pricing Components

| Volume Type | Use Case | Pricing Based On |
|-------------|----------|------------------|
| gp3 | General purpose SSD | GB/month + IOPS + throughput |
| gp2 | General purpose SSD (older) | GB/month (IOPS included) |
| io2/io1 | High-performance SSD | GB/month + provisioned IOPS |
| st1 | Throughput optimized HDD | GB/month |
| sc1 | Cold HDD | GB/month |

## EBS Additional Costs

| Feature | Description | Pricing |
|---------|-------------|---------|
| Snapshots | Point-in-time backups | Per GB-month stored |
| Snapshot Archive | Long-term snapshot storage | Lower storage, retrieval fee |
| Fast Snapshot Restore | Instant snapshot access | Per AZ per snapshot hour |
| Data Transfer | Cross-AZ EBS data | Per GB transferred |

## EFS Pricing

```
+------------------------------------------------------------------+
|                    EFS PRICING MODEL                              |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+         +------------------+               |
|   | EFS Standard     |         | EFS One Zone     |               |
|   | - Multi-AZ       |         | - Single AZ      |               |
|   | - Higher cost    |         | - 47% lower cost |               |
|   +------------------+         +------------------+               |
|           |                            |                          |
|           v                            v                          |
|   +------------------+         +------------------+               |
|   | Standard Storage |         | One Zone Storage |               |
|   | Standard-IA      |         | One Zone-IA      |               |
|   +------------------+         +------------------+               |
|                                                                   |
|   Pricing: Per GB-month (storage) + throughput charges            |
|   IA classes: Lower storage cost + retrieval fee                  |
|                                                                   |
+------------------------------------------------------------------+
```

## EFS Throughput Modes

| Mode | Description | Best For |
|------|-------------|----------|
| Bursting | Throughput scales with storage size | Most workloads |
| Provisioned | Set throughput independent of size | High throughput, small storage |
| Elastic | Auto-scales throughput | Unpredictable workloads |

## Storage Cost Optimization Strategies

```
+------------------------------------------------------------------+
|               STORAGE COST OPTIMIZATION                           |
+------------------------------------------------------------------+
|                                                                   |
|   1. RIGHT-SIZE STORAGE                                           |
|      - Use appropriate storage class for access patterns          |
|      - Enable S3 Intelligent-Tiering for unknown patterns         |
|                                                                   |
|   2. LIFECYCLE POLICIES                                           |
|      - Automatically transition to cheaper storage classes        |
|      - Delete incomplete multipart uploads                        |
|      - Expire old object versions                                 |
|                                                                   |
|   3. ANALYZE ACCESS PATTERNS                                      |
|      - Use S3 Storage Class Analysis                              |
|      - Use S3 Storage Lens for insights                           |
|                                                                   |
|   4. COMPRESSION & DEDUPLICATION                                  |
|      - Compress data before storing                               |
|      - Use S3 Object Lambda for dynamic compression               |
|                                                                   |
+------------------------------------------------------------------+
```

## Minimum Storage Duration Charges

| Storage Class | Minimum Duration | Charged If Deleted Early |
|---------------|------------------|-------------------------|
| S3 Standard | None | No |
| S3 Standard-IA | 30 days | Yes |
| S3 One Zone-IA | 30 days | Yes |
| S3 Glacier Instant | 90 days | Yes |
| S3 Glacier Flexible | 90 days | Yes |
| S3 Glacier Deep Archive | 180 days | Yes |

## 🎯 Exam Tips

- **S3 Standard** = Frequently accessed, no retrieval fee, highest storage cost
- **S3 Standard-IA** = Infrequent access, lower storage cost, retrieval fee applies
- **S3 One Zone-IA** = Single AZ storage, cheapest IA option, less durable
- **S3 Glacier** classes = Archive storage, very low cost, retrieval takes time
- **S3 Intelligent-Tiering** = Best for unknown access patterns, auto-tiers data
- **EBS gp3** = General purpose SSD with separate IOPS/throughput pricing
- **EBS io2** = Highest performance SSD for databases
- Know that **retrieval costs** apply to IA and Glacier classes
- **Minimum storage duration** charges apply to IA and Glacier classes

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Storage Class | S3 tier that determines cost, durability, and access speed |
| Infrequent Access (IA) | Storage tier for data accessed less than once per month |
| Glacier | Archive storage with very low cost but retrieval delays |
| Retrieval Fee | Cost charged when accessing data from IA or Glacier |
| Lifecycle Policy | Rules to automatically transition or expire objects |
| Provisioned IOPS | Pre-configured I/O operations per second for EBS |
| Throughput | Rate of data transfer measured in MB/s |

## 💡 Key Takeaways

1. S3 pricing includes storage, requests, data transfer, and retrieval costs
2. Choose storage class based on access frequency and retrieval requirements
3. S3 Intelligent-Tiering automatically optimizes costs for unknown access patterns
4. Glacier classes offer lowest storage costs but have retrieval delays and fees
5. EBS pricing varies by volume type and includes IOPS/throughput charges
6. Lifecycle policies automate cost optimization by transitioning data
7. Minimum storage duration charges apply to IA and Glacier classes
8. Always consider total cost: storage + requests + retrieval + transfer

---

*Previous: [02 - Reserved Instance Flexibility](../02-reserved-instance-flexibility/readme.md) | Next: [04 - Data Transfer Costs](../04-data-transfer-costs/readme.md)*

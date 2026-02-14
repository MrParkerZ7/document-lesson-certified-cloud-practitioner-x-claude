# 💰 Data Transfer Costs

## File Structure

```
lesson-17-aws-pricing-models/
└── 04-data-transfer-costs/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Data transfer costs are often overlooked but can become a significant portion of your AWS bill. Understanding when data transfer is free, when it's charged, and how to minimize these costs is essential for optimizing your AWS spending.

## Data Transfer Pricing Overview

```
+------------------------------------------------------------------+
|                  DATA TRANSFER PRICING RULES                      |
+------------------------------------------------------------------+
|                                                                   |
|                         AWS CLOUD                                 |
|   +-----------------------------------------------------------+   |
|   |                                                           |   |
|   |   INBOUND (to AWS)                                        |   |
|   |   +-------------------+                                   |   |
|   |   |     FREE          |  <---- Data INTO AWS              |   |
|   |   +-------------------+        (from Internet)            |   |
|   |                                                           |   |
|   |   OUTBOUND (from AWS)                                     |   |
|   |   +-------------------+                                   |   |
|   |   |     CHARGED       |  ----> Data OUT of AWS            |   |
|   |   +-------------------+        (to Internet)              |   |
|   |                                                           |   |
|   +-----------------------------------------------------------+   |
|                                                                   |
|   Key Rule: Data IN is free, Data OUT is charged                  |
|                                                                   |
+------------------------------------------------------------------+
```

## Data Transfer Cost Categories

| Transfer Type | Cost |
|--------------|------|
| Data IN to AWS from Internet | FREE |
| Data OUT to Internet | Charged per GB (tiered pricing) |
| Data transfer between AZs | Charged per GB |
| Data transfer between Regions | Charged per GB |
| Data transfer within same AZ | FREE (using private IP) |
| Data transfer to CloudFront | Reduced rate |

## Inbound vs Outbound Data Transfer

```
+------------------------------------------------------------------+
|              INBOUND vs OUTBOUND DATA TRANSFER                    |
+------------------------------------------------------------------+
|                                                                   |
|        INTERNET                    AWS REGION                     |
|   +-----------------+        +-------------------------+          |
|   |                 |        |                         |          |
|   |    Users        |  FREE  |      EC2 Instance       |          |
|   |    Uploads      | =====> |      S3 Bucket          |          |
|   |                 |        |      (INBOUND)          |          |
|   |                 |        |                         |          |
|   |    Users        | $$$$$  |      EC2 Instance       |          |
|   |    Downloads    | <===== |      S3 Bucket          |          |
|   |                 |        |      (OUTBOUND)         |          |
|   |                 |        |                         |          |
|   +-----------------+        +-------------------------+          |
|                                                                   |
+------------------------------------------------------------------+
```

## Cross-AZ Data Transfer

```
+------------------------------------------------------------------+
|                  CROSS-AZ DATA TRANSFER                           |
+------------------------------------------------------------------+
|                                                                   |
|                        AWS REGION                                 |
|   +-----------------------------------------------------------+   |
|   |                                                           |   |
|   |   +------------------+         +------------------+       |   |
|   |   |    AZ-1a         |         |    AZ-1b         |       |   |
|   |   |                  |         |                  |       |   |
|   |   |   [Instance A]   | ~~~~~~> |   [Instance B]   |       |   |
|   |   |                  |  $$$    |                  |       |   |
|   |   |                  | <~~~~~~ |                  |       |   |
|   |   |                  |  $$$    |                  |       |   |
|   |   +------------------+         +------------------+       |   |
|   |                                                           |   |
|   |   Note: Cross-AZ traffic is charged in BOTH directions    |   |
|   |                                                           |   |
|   +-----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Cross-Region Data Transfer

```
+------------------------------------------------------------------+
|                 CROSS-REGION DATA TRANSFER                        |
+------------------------------------------------------------------+
|                                                                   |
|   +-------------------------+     +-------------------------+     |
|   |    US-EAST-1            |     |    EU-WEST-1            |     |
|   |                         |     |                         |     |
|   |   [EC2 Instance]        |     |   [EC2 Instance]        |     |
|   |   [S3 Bucket]           |     |   [S3 Bucket]           |     |
|   |                         |     |                         |     |
|   +------------+------------+     +------------+------------+     |
|                |                               ^                  |
|                |                               |                  |
|                +===============================+                  |
|                    Cross-Region Transfer                          |
|                    (Charged per GB)                               |
|                                                                   |
|   Examples: S3 Replication, RDS Read Replicas, VPC Peering        |
|                                                                   |
+------------------------------------------------------------------+
```

## VPC Endpoints and Data Transfer

VPC Endpoints can significantly reduce data transfer costs by keeping traffic within AWS.

```
+------------------------------------------------------------------+
|                    VPC ENDPOINT BENEFITS                          |
+------------------------------------------------------------------+
|                                                                   |
|   WITHOUT VPC ENDPOINT:                                           |
|   +------------------+     +----------+     +------------------+  |
|   |  EC2 Instance    | --> | Internet | --> |    S3 Bucket     |  |
|   |  (in VPC)        |     | Gateway  |     |                  |  |
|   +------------------+     +----------+     +------------------+  |
|   Data goes through Internet = Potential data transfer charges    |
|                                                                   |
|   WITH VPC ENDPOINT (Gateway):                                    |
|   +------------------+     +----------+     +------------------+  |
|   |  EC2 Instance    | --> | Gateway  | --> |    S3 Bucket     |  |
|   |  (in VPC)        |     | Endpoint |     |                  |  |
|   +------------------+     +----------+     +------------------+  |
|   Data stays within AWS = FREE data transfer (Gateway Endpoints)  |
|                                                                   |
+------------------------------------------------------------------+
```

## Types of VPC Endpoints

| Type | Supported Services | Cost |
|------|-------------------|------|
| Gateway Endpoint | S3, DynamoDB | FREE |
| Interface Endpoint | 100+ AWS services | Hourly + per GB |

## Data Transfer Pricing Tiers (Outbound)

| Tier | Data Amount | Price Trend |
|------|-------------|-------------|
| First 10 TB/month | Per GB price | Highest |
| Next 40 TB/month | Per GB price | Lower |
| Next 100 TB/month | Per GB price | Lower |
| Over 150 TB/month | Per GB price | Lowest |

**Note:** The more data you transfer, the lower the per-GB cost.

## CloudFront Data Transfer Benefits

```
+------------------------------------------------------------------+
|               CLOUDFRONT DATA TRANSFER SAVINGS                    |
+------------------------------------------------------------------+
|                                                                   |
|   DIRECT FROM S3:                                                 |
|   +----------+                      +----------+                  |
|   |    S3    | ===================> |   User   |                  |
|   +----------+   Higher cost        +----------+                  |
|                  per GB                                           |
|                                                                   |
|   VIA CLOUDFRONT:                                                 |
|   +----------+     +------------+     +----------+                |
|   |    S3    | --> | CloudFront | --> |   User   |                |
|   +----------+     +------------+     +----------+                |
|                  Lower cost + cached content                      |
|                                                                   |
|   Benefits:                                                       |
|   - Lower data transfer rates from origin to edge                 |
|   - Cached content = Less origin requests                         |
|   - Often cheaper than direct from S3 for global distribution     |
|                                                                   |
+------------------------------------------------------------------+
```

## Private Connectivity Options

| Option | Description | Data Transfer Cost |
|--------|-------------|-------------------|
| VPC Peering | Connect VPCs within/across regions | Cross-AZ/Region rates apply |
| AWS Transit Gateway | Hub for connecting VPCs | Per GB + hourly |
| AWS Direct Connect | Dedicated connection to AWS | Lower than Internet |
| AWS PrivateLink | Private access to services | Per GB + hourly |

## Data Transfer Cost Optimization Strategies

```
+------------------------------------------------------------------+
|            DATA TRANSFER OPTIMIZATION STRATEGIES                  |
+------------------------------------------------------------------+
|                                                                   |
|   1. USE VPC GATEWAY ENDPOINTS                                    |
|      +-------------------------------------------+                |
|      | S3 and DynamoDB: FREE with Gateway        |                |
|      | Endpoints vs Internet Gateway charges     |                |
|      +-------------------------------------------+                |
|                                                                   |
|   2. KEEP RESOURCES IN SAME AZ                                    |
|      +-------------------------------------------+                |
|      | Same AZ + Private IP = FREE data transfer |                |
|      | Cross-AZ = Charged both directions        |                |
|      +-------------------------------------------+                |
|                                                                   |
|   3. USE CLOUDFRONT FOR DISTRIBUTION                              |
|      +-------------------------------------------+                |
|      | Lower transfer rates to edge locations    |                |
|      | Caching reduces origin requests           |                |
|      +-------------------------------------------+                |
|                                                                   |
|   4. COMPRESS DATA BEFORE TRANSFER                                |
|      +-------------------------------------------+                |
|      | Less data = Lower transfer costs          |                |
|      | Use gzip, Snappy, or other compression    |                |
|      +-------------------------------------------+                |
|                                                                   |
|   5. USE AWS DIRECT CONNECT                                       |
|      +-------------------------------------------+                |
|      | Lower per-GB rates than Internet          |                |
|      | Consistent network performance            |                |
|      +-------------------------------------------+                |
|                                                                   |
+------------------------------------------------------------------+
```

## Common Data Transfer Scenarios

| Scenario | Cost |
|----------|------|
| Upload files to S3 from Internet | FREE |
| Download files from S3 to Internet | Charged per GB |
| EC2 to S3 in same region | FREE (via Gateway Endpoint) |
| EC2 to RDS in same AZ | FREE (private IP) |
| EC2 to RDS in different AZ | Charged per GB |
| S3 Cross-Region Replication | Charged per GB |
| CloudFront to users | Charged (lower rate) |
| S3 Transfer Acceleration | Charged (premium) |

## AWS Data Transfer Calculator Considerations

When estimating data transfer costs, consider:

1. **Inbound data** - Usually free
2. **Outbound to Internet** - Per GB, tiered pricing
3. **Cross-AZ traffic** - Often overlooked, adds up quickly
4. **Cross-Region traffic** - Higher cost, consider architecture
5. **Private vs Public IPs** - Private IPs within same AZ are free

## 🎯 Exam Tips

- **Data IN to AWS** from the Internet is always **FREE**
- **Data OUT to Internet** is charged per GB (tiered pricing)
- **Same AZ + Private IP** = FREE data transfer
- **Cross-AZ** = Charged in BOTH directions
- **VPC Gateway Endpoints** for S3 and DynamoDB are FREE
- **VPC Interface Endpoints** have hourly + per GB charges
- **CloudFront** can reduce data transfer costs for global distribution
- **Direct Connect** offers lower data transfer rates than Internet

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Data Transfer IN | Data coming into AWS from the Internet |
| Data Transfer OUT | Data going from AWS to the Internet |
| Cross-AZ Transfer | Data moving between Availability Zones |
| Cross-Region Transfer | Data moving between AWS Regions |
| VPC Endpoint | Private connection to AWS services without using Internet |
| Gateway Endpoint | Free endpoint for S3 and DynamoDB |
| Interface Endpoint | PrivateLink-powered endpoint for other services |
| Direct Connect | Dedicated network connection to AWS |

## 💡 Key Takeaways

1. Data transfer INTO AWS from the Internet is always free
2. Data transfer OUT to the Internet is charged per GB with tiered pricing
3. Same AZ traffic using private IPs is free
4. Cross-AZ traffic is charged in both directions
5. VPC Gateway Endpoints for S3 and DynamoDB are free and reduce costs
6. CloudFront can reduce data transfer costs for content distribution
7. Architect applications to minimize cross-AZ and cross-region traffic
8. Use AWS Direct Connect for lower data transfer rates on large volumes

---

*Previous: [03 - Storage Pricing](../03-storage-pricing/readme.md) | Next: [05 - Free Tier](../05-free-tier/readme.md)*

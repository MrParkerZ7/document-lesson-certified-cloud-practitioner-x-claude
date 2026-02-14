# 🌍 AWS Regions

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 01-aws-regions/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Regions are physical locations around the world where AWS clusters data centers. Each AWS Region is a separate geographic area designed to be completely isolated from other AWS Regions. This design achieves the greatest possible fault tolerance and stability.

## What is an AWS Region?

```
+------------------------------------------------------------------+
|                       AWS REGIONS                                 |
+------------------------------------------------------------------+
|                                                                   |
|   A Region is a geographic area containing multiple              |
|   data center clusters called Availability Zones                  |
|                                                                   |
|   +------------------------------------------------------------+ |
|   |                    AWS REGION (e.g., us-east-1)             | |
|   |  +------------+   +------------+   +------------+           | |
|   |  |    AZ-1a   |   |    AZ-1b   |   |    AZ-1c   |           | |
|   |  | Data Center|   | Data Center|   | Data Center|           | |
|   |  | Cluster    |   | Cluster    |   | Cluster    |           | |
|   |  +------------+   +------------+   +------------+           | |
|   |         |               |               |                    | |
|   |         +-------+-------+-------+-------+                    | |
|   |                 |                                            | |
|   |      High-speed, low-latency connections                     | |
|   +------------------------------------------------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Regions Worldwide

| Geography | Example Regions | Count (approx) |
|-----------|----------------|----------------|
| Americas | N. Virginia, Ohio, Oregon, GovCloud | 8+ |
| Europe | Ireland, Frankfurt, London, Paris | 8+ |
| Asia Pacific | Singapore, Sydney, Tokyo, Mumbai | 10+ |
| Middle East | Bahrain, UAE | 2+ |
| Africa | Cape Town | 1 |
| Total | | 30+ |

## Region Naming Convention

| Code | Name | Location |
|------|------|----------|
| us-east-1 | US East (N. Virginia) | Virginia, USA |
| us-west-2 | US West (Oregon) | Oregon, USA |
| eu-west-1 | Europe (Ireland) | Dublin, Ireland |
| ap-southeast-1 | Asia Pacific (Singapore) | Singapore |
| sa-east-1 | South America (São Paulo) | Brazil |

## Why Regions Matter

| Benefit | Description |
|---------|-------------|
| Data Residency | Keep data in specific geographic location |
| Compliance | Meet regulatory requirements |
| Latency | Reduce latency for local users |
| Disaster Recovery | Deploy across regions for resilience |
| Pricing | Costs vary by region |

## Choosing a Region

| Factor | Consideration |
|--------|---------------|
| Compliance | Data sovereignty, legal requirements |
| Proximity | Closer to users = lower latency |
| Services | Not all services in all regions |
| Pricing | Costs differ between regions |
| Disaster Recovery | Multi-region for resilience |

## Region Independence

Each region is completely independent:

| Aspect | Isolation |
|--------|-----------|
| Data | Data doesn't replicate automatically |
| Services | Each region runs independently |
| Outages | Region outages don't affect others |
| Resources | Resources are region-specific |

## Regional vs Global Services

| Global Services | Regional Services |
|----------------|-------------------|
| IAM | EC2 |
| CloudFront | S3 |
| Route 53 | VPC |
| WAF | RDS |
| | Lambda |

## Cross-Region Features

```
+------------------------------------------------------------------+
|                   CROSS-REGION CAPABILITIES                       |
+------------------------------------------------------------------+
|                                                                   |
|   Region A (us-east-1)              Region B (eu-west-1)          |
|   +------------------+              +------------------+          |
|   |    S3 Bucket     | -----CRR---> |    S3 Bucket     |          |
|   +------------------+              +------------------+          |
|                                                                   |
|   +------------------+              +------------------+          |
|   |    RDS DB        | ---Replica-> |    RDS Read      |          |
|   +------------------+              |    Replica       |          |
|                                     +------------------+          |
|                                                                   |
|   +------------------+              +------------------+          |
|   |    AMI           | ---Copy----> |    AMI Copy      |          |
|   +------------------+              +------------------+          |
|                                                                   |
+------------------------------------------------------------------+
```

## Cross-Region Features

| Feature | Description |
|---------|-------------|
| S3 Cross-Region Replication | Replicate objects to another region |
| RDS Read Replicas | Create read replicas in other regions |
| AMI Copy | Copy AMIs between regions |
| DynamoDB Global Tables | Multi-region, multi-active tables |
| Route 53 | Global DNS routing |

## Region Considerations

### Data Transfer Costs

| Transfer Type | Cost |
|---------------|------|
| Within region | Usually free or minimal |
| Between regions | Higher cost |
| To internet | Egress charges |

### Service Availability

| Consideration | Description |
|---------------|-------------|
| New services | Launch in major regions first |
| GovCloud | Special regions for government |
| China regions | Separate from global regions |

## 🎯 Exam Tips

- **Region** = geographic area with multiple AZs
- Each region is **completely isolated** from others
- Data **does not replicate** automatically between regions
- **IAM, CloudFront, Route 53** = global services
- **EC2, S3, RDS** = regional services
- Choose region based on **compliance, latency, pricing, services**
- Cross-region **data transfer costs money**
- Currently **30+ regions** worldwide

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Region | Geographic area with multiple AZs |
| Regional Service | Service that operates in one region |
| Global Service | Service that operates across all regions |
| Cross-Region Replication | Copying data between regions |
| Data Residency | Keeping data in specific location |

## 💡 Key Takeaways

1. AWS has 30+ regions worldwide
2. Each region contains multiple Availability Zones
3. Regions are completely isolated from each other
4. Data does not automatically replicate between regions
5. Some services are global, most are regional
6. Choose regions based on compliance, latency, and pricing
7. Cross-region features enable multi-region architectures

---

*Next: [02 - Availability Zones](../02-availability-zones/readme.md)*

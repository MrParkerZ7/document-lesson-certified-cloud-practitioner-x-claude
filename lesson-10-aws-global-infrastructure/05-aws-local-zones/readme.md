# 📍 AWS Local Zones

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 05-aws-local-zones/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Local Zones are a type of infrastructure deployment that places compute, storage, and database services closer to large population centers, industries, and IT centers. They enable you to run applications that require single-digit millisecond latency to end users.

## What are Local Zones?

```
+------------------------------------------------------------------+
|                      AWS LOCAL ZONES                              |
+------------------------------------------------------------------+
|                                                                   |
|   Local Zones extend AWS Regions to geographic proximity          |
|   of large population centers for ultra-low latency               |
|                                                                   |
|   +------------------------------------------------------------+ |
|   |                    AWS REGION                               | |
|   |   +------------+   +------------+   +------------+          | |
|   |   |    AZ-1    |   |    AZ-2    |   |    AZ-3    |          | |
|   |   +------------+   +------------+   +------------+          | |
|   +------------------------------------------------------------+ |
|                               |                                   |
|                               | (Connected)                       |
|                               v                                   |
|   +------------------------+     +------------------------+       |
|   |     LOCAL ZONE         |     |     LOCAL ZONE         |       |
|   |     Los Angeles        |     |     Boston             |       |
|   | • Low latency (< 10ms) |     | • Low latency (< 10ms) |       |
|   | • Near end users       |     | • Near end users       |       |
|   +------------------------+     +------------------------+       |
|                                                                   |
+------------------------------------------------------------------+
```

## Local Zone Characteristics

| Characteristic | Description |
|----------------|-------------|
| Location | Near large cities |
| Latency | Single-digit milliseconds |
| Connection | Connected to parent region |
| Services | Subset of AWS services |
| Opt-in | Must enable in console |

## Local Zones vs Regions vs AZs

| Aspect | Region | Availability Zone | Local Zone |
|--------|--------|-------------------|------------|
| Purpose | Full AWS services | High availability | Low latency |
| Location | Geographic area | Within region | Near cities |
| Services | All | All | Subset |
| Latency | Varies | < 1ms in-region | < 10ms to users |
| Opt-in | Available | Available | Must enable |

## Available Services in Local Zones

| Service Category | Examples |
|-----------------|----------|
| Compute | EC2, ECS, EKS |
| Storage | EBS |
| Database | RDS (limited) |
| Networking | VPC, ELB, Direct Connect |

## Local Zone Use Cases

| Use Case | Requirement |
|----------|-------------|
| Media & entertainment | Real-time rendering |
| Gaming | Low-latency multiplayer |
| Live streaming | Quick content delivery |
| Machine learning | Real-time inference |
| AR/VR | Immersive experiences |
| Healthcare | Real-time analysis |

## Local Zone Locations

| Parent Region | Local Zone Cities |
|---------------|-------------------|
| us-west-2 (Oregon) | Los Angeles, Phoenix, Denver |
| us-east-1 (N. Virginia) | Boston, Miami, Chicago, Dallas |
| ap-northeast-1 (Tokyo) | Osaka |
| eu-west-2 (London) | Manchester |

## How Local Zones Work

```
+------------------------------------------------------------------+
|                  LOCAL ZONE ARCHITECTURE                          |
+------------------------------------------------------------------+
|                                                                   |
|   End Users in LA                  AWS Region (us-west-2)         |
|   +----------+                     +------------------+           |
|   |  Users   |                     |   Oregon Region  |           |
|   | (LA Area)|                     |                  |           |
|   +----------+                     |  +------------+  |           |
|        |                           |  | Full AWS   |  |           |
|        | < 10ms                    |  | Services   |  |           |
|        v                           |  +------------+  |           |
|   +------------------+             +------------------+           |
|   | Local Zone LA    |<-------------------|                       |
|   | • EC2            |    (Connected)                             |
|   | • EBS            |                                            |
|   | • VPC subnet     |                                            |
|   +------------------+                                            |
|                                                                   |
+------------------------------------------------------------------+
```

## Setting Up Local Zones

| Step | Action |
|------|--------|
| 1 | Enable Local Zone in console |
| 2 | Create subnet in Local Zone |
| 3 | Launch resources in subnet |
| 4 | Use same VPC as parent region |

## Local Zone Networking

| Component | Description |
|-----------|-------------|
| VPC | Same VPC as parent region |
| Subnets | Specific to Local Zone |
| Internet Gateway | Shared with region |
| Direct Connect | Local connectivity |

## Pricing

| Factor | Pricing |
|--------|---------|
| EC2 | Higher than region (varies) |
| Data transfer | Within zone = free |
| To parent region | Standard transfer rates |
| EBS | Similar to region |

## Benefits of Local Zones

| Benefit | Description |
|---------|-------------|
| Low latency | Single-digit milliseconds |
| Consistent APIs | Same as region |
| Easy deployment | Extend existing VPCs |
| Hybrid options | Connect on-premises |

## Limitations

| Limitation | Description |
|------------|-------------|
| Service availability | Not all services available |
| Capacity | Smaller than regions |
| Opt-in required | Must enable |
| Higher costs | Premium pricing |

## 🎯 Exam Tips

- **Local Zones** = extend regions to cities for low latency
- **Single-digit millisecond** latency to end users
- **Must opt-in** to enable Local Zones
- **Subset of services** available (EC2, EBS, VPC)
- Use cases: **gaming**, **media**, **streaming**, **AR/VR**
- Different from **edge locations** (caching) and **Outposts** (on-premises)
- Connected to **parent region** for full services

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Local Zone | AWS infrastructure near cities |
| Parent Region | Region the Local Zone connects to |
| Opt-in | Must explicitly enable |
| Single-digit ms | < 10 millisecond latency |

## 💡 Key Takeaways

1. Local Zones extend regions to population centers
2. Enable single-digit millisecond latency to end users
3. Must opt-in to enable in your account
4. Connected to parent region for VPC and management
5. Subset of AWS services available
6. Ideal for latency-sensitive applications
7. Different from edge locations and Outposts

---

*Next: [06 - AWS Wavelength](../06-aws-wavelength/readme.md)*

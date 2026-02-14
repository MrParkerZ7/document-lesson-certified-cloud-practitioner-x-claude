# 🏢 Availability Zones

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 02-availability-zones/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Availability Zones (AZs) are distinct locations within an AWS Region that are engineered to be isolated from failures in other Availability Zones. They provide inexpensive, low-latency network connectivity to other Availability Zones in the same Region.

## What is an Availability Zone?

```
+------------------------------------------------------------------+
|                    AVAILABILITY ZONE                              |
+------------------------------------------------------------------+
|                                                                   |
|   An Availability Zone consists of one or more discrete          |
|   data centers with redundant power, networking, and connectivity |
|                                                                   |
|   +------------------------------------------------------------+ |
|   |                  AVAILABILITY ZONE (us-east-1a)             | |
|   |                                                             | |
|   |   +----------------+    +----------------+                  | |
|   |   | Data Center 1  |    | Data Center 2  |    ...           | |
|   |   | - Power        |    | - Power        |                  | |
|   |   | - Cooling      |    | - Cooling      |                  | |
|   |   | - Networking   |    | - Networking   |                  | |
|   |   +----------------+    +----------------+                  | |
|   |                                                             | |
|   |   Redundant power, networking, connectivity                 | |
|   +------------------------------------------------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Availability Zone Characteristics

| Characteristic | Description |
|----------------|-------------|
| Physical separation | Each AZ is in a separate facility |
| Independent infrastructure | Separate power, cooling, networking |
| Low-latency connection | High-speed links between AZs |
| Fault isolation | Failures don't affect other AZs |
| Multiple data centers | Each AZ may have multiple DCs |

## AZs Within a Region

```
+------------------------------------------------------------------+
|                      AWS REGION                                   |
+------------------------------------------------------------------+
|                                                                   |
|   +-------------+     +-------------+     +-------------+         |
|   |    AZ-a     |     |    AZ-b     |     |    AZ-c     |         |
|   |             |     |             |     |             |         |
|   |  Data       |<--->|  Data       |<--->|  Data       |         |
|   |  Centers    |     |  Centers    |     |  Centers    |         |
|   |             |     |             |     |             |         |
|   +-------------+     +-------------+     +-------------+         |
|         ^                   ^                   ^                 |
|         |                   |                   |                 |
|         +----------- High-Speed Links ----------+                 |
|                   (Low latency < 1ms)                             |
|                                                                   |
|   Each AZ: Separate power, cooling, networking                    |
|   Distance: Meaningful separation (miles apart)                   |
|                                                                   |
+------------------------------------------------------------------+
```

## Number of AZs per Region

| Region Type | Typical AZ Count |
|-------------|------------------|
| Major regions | 3-6 AZs |
| Smaller regions | 2-3 AZs |
| Minimum | 2 AZs |

## AZ Naming

| Format | Example | Note |
|--------|---------|------|
| Region + letter | us-east-1a | AZ ID is account-specific |
| Physical mapping | use1-az1 | Actual physical AZ |

Note: us-east-1a in one account may map to a different physical AZ than us-east-1a in another account.

## High Availability with AZs

```
+------------------------------------------------------------------+
|              HIGH AVAILABILITY ARCHITECTURE                       |
+------------------------------------------------------------------+
|                                                                   |
|                       Load Balancer                               |
|                           |                                       |
|            +-----------------------------+                        |
|            |              |              |                        |
|            v              v              v                        |
|       +--------+     +--------+     +--------+                    |
|       |  AZ-a  |     |  AZ-b  |     |  AZ-c  |                    |
|       | EC2 x2 |     | EC2 x2 |     | EC2 x2 |                    |
|       +--------+     +--------+     +--------+                    |
|            |              |              |                        |
|            v              v              v                        |
|       +--------+     +--------+     +--------+                    |
|       | RDS    |<----|  RDS   |---->| (Read  |                    |
|       | Primary|Sync |Standby |Async|Replica)|                    |
|       +--------+     +--------+     +--------+                    |
|                                                                   |
+------------------------------------------------------------------+
```

## Multi-AZ Deployments

| Service | Multi-AZ Feature |
|---------|------------------|
| EC2 | Deploy instances in multiple AZs |
| RDS | Multi-AZ for automatic failover |
| ELB | Distribute traffic across AZs |
| S3 | Automatically stores in multiple AZs |
| DynamoDB | Data replicated across 3 AZs |
| Lambda | Runs in multiple AZs automatically |

## Benefits of Multiple AZs

| Benefit | Description |
|---------|-------------|
| Fault tolerance | Survive AZ failure |
| High availability | Minimize downtime |
| Low latency | AZs connected with fast links |
| Data redundancy | Replicate data across AZs |
| Disaster recovery | Quick recovery from failures |

## AZ Failure Scenarios

| Scenario | Multi-AZ Response |
|----------|-------------------|
| Power failure | Other AZs continue |
| Network issue | Traffic routes to healthy AZs |
| Natural disaster | Separate locations protected |
| Hardware failure | Automatic failover |

## Services and AZ Awareness

| AZ Aware | Not AZ Aware |
|----------|--------------|
| EC2 instances | S3 (regional) |
| EBS volumes | DynamoDB (regional) |
| RDS | CloudFront (global) |
| Subnets | IAM (global) |
| NAT Gateways | Route 53 (global) |

## Best Practices

| Practice | Description |
|----------|-------------|
| Deploy across 2+ AZs | Minimum for high availability |
| Use load balancers | Distribute traffic across AZs |
| Enable Multi-AZ | For databases (RDS) |
| Replicate data | S3, EBS snapshots |
| Automate failover | Use Auto Scaling groups |

## Cost Considerations

| Aspect | Cost Impact |
|--------|-------------|
| Cross-AZ data transfer | Small charge applies |
| Multi-AZ RDS | About 2x single-AZ cost |
| ELB across AZs | Included in ELB pricing |
| S3 | Included in storage pricing |

## AZ vs Region Comparison

| Aspect | Availability Zone | Region |
|--------|-------------------|--------|
| Scope | Part of a region | Geographic area |
| Latency | < 1ms between AZs | Higher between regions |
| Use case | High availability | Disaster recovery |
| Data replication | Synchronous | Asynchronous |
| Cost | Lower data transfer | Higher data transfer |

## 🎯 Exam Tips

- **AZ** = one or more data centers with independent power/cooling
- Each region has **minimum 2 AZs** (typically 3-6)
- AZs are connected with **high-speed, low-latency** links
- **Multi-AZ** = high availability within a region
- **us-east-1a** in one account may be different physical AZ than another account
- Data transfer **between AZs costs money**
- **S3** automatically stores data across multiple AZs
- **EBS volumes** are AZ-specific

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Availability Zone | Isolated data center cluster within region |
| Multi-AZ | Deployment across multiple AZs |
| Fault Isolation | Failures contained within AZ |
| Synchronous Replication | Real-time data copy between AZs |
| AZ-ID | Consistent identifier across accounts |

## 💡 Key Takeaways

1. Availability Zones are isolated infrastructure within a region
2. Each AZ has independent power, cooling, and networking
3. Regions have 2-6 Availability Zones
4. AZs are connected with high-speed, low-latency links
5. Deploy across multiple AZs for high availability
6. Some services are AZ-specific, others are regional
7. Cross-AZ data transfer incurs small charges

---

*Next: [03 - Edge Locations and Points of Presence](../03-edge-locations-and-points-of-presence/readme.md)*

# 🌐 Multi-Region Strategies

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 08-multi-region-strategies/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Multi-region deployment strategies enable organizations to achieve high availability, disaster recovery, and low latency for global users. AWS provides tools and services to implement various multi-region architectures based on business requirements.

## Why Multi-Region?

```
+------------------------------------------------------------------+
|                    MULTI-REGION BENEFITS                          |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |   DISASTER       |  |   GLOBAL         |  |   COMPLIANCE     | |
|   |   RECOVERY       |  |   PERFORMANCE    |  |                  | |
|   +------------------+  +------------------+  +------------------+ |
|   | Survive region   |  | Low latency for  |  | Data residency   | |
|   | failures         |  | worldwide users  |  | requirements     | |
|   | Business         |  | Better user      |  | Regulatory       | |
|   | continuity       |  | experience       |  | compliance       | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Multi-Region Architecture Patterns

| Pattern | Description | Use Case |
|---------|-------------|----------|
| Active-Passive | Primary region active, secondary standby | Disaster recovery |
| Active-Active | Multiple regions serve traffic | High availability |
| Pilot Light | Minimal resources in standby | Cost-effective DR |
| Warm Standby | Scaled-down copy running | Faster recovery |
| Multi-Site | Full deployment in each region | Maximum availability |

## Active-Passive Strategy

```
+------------------------------------------------------------------+
|                    ACTIVE-PASSIVE                                 |
+------------------------------------------------------------------+
|                                                                   |
|   PRIMARY (Active)                 SECONDARY (Passive)            |
|   +-----------------+              +-----------------+            |
|   | Region A        |   Data       | Region B        |            |
|   | (us-east-1)     | --------->   | (eu-west-1)     |            |
|   |                 | Replication  |                 |            |
|   | All traffic     |              | Standby         |            |
|   +-----------------+              +-----------------+            |
|          |                                |                       |
|          v                                v                       |
|   [Route 53 - Failover Routing]                                   |
|                                                                   |
|   Normal: All traffic to Region A                                 |
|   Failover: Traffic redirected to Region B                        |
|                                                                   |
+------------------------------------------------------------------+
```

## Active-Active Strategy

```
+------------------------------------------------------------------+
|                    ACTIVE-ACTIVE                                  |
+------------------------------------------------------------------+
|                                                                   |
|   REGION A                         REGION B                       |
|   +-----------------+              +-----------------+            |
|   | us-east-1       |<------------>| eu-west-1       |            |
|   | Serving users   | Bidirectional| Serving users   |            |
|   | in Americas     | Replication  | in Europe       |            |
|   +-----------------+              +-----------------+            |
|          |                                |                       |
|          +---------+    +--------+--------+                       |
|                    |    |                                         |
|                    v    v                                         |
|              [Route 53 - Latency/Geolocation Routing]             |
|                                                                   |
|   Traffic routed to nearest/fastest region                        |
|                                                                   |
+------------------------------------------------------------------+
```

## DR Strategy Comparison

| Strategy | RTO | RPO | Cost | Complexity |
|----------|-----|-----|------|------------|
| Backup & Restore | Hours | Hours | Low | Low |
| Pilot Light | Minutes-Hours | Minutes | Medium-Low | Medium |
| Warm Standby | Minutes | Seconds-Minutes | Medium | Medium |
| Multi-Site Active-Active | Seconds | Zero-Seconds | High | High |

## AWS Services for Multi-Region

| Service | Multi-Region Feature |
|---------|---------------------|
| Route 53 | Global DNS with failover |
| S3 | Cross-Region Replication |
| RDS | Read Replicas, Aurora Global |
| DynamoDB | Global Tables |
| CloudFront | Global edge delivery |
| Global Accelerator | Static anycast IPs |

## Route 53 Routing Policies

| Policy | Description |
|--------|-------------|
| Simple | Single resource |
| Failover | Active-passive |
| Geolocation | Route by user location |
| Latency | Route to lowest latency |
| Weighted | Distribute by percentage |
| Geoproximity | Route by geographic distance |

## Data Replication Strategies

| Service | Replication Type |
|---------|-----------------|
| S3 CRR | Cross-Region Replication |
| Aurora Global | 1 primary, 5 secondary regions |
| DynamoDB Global Tables | Multi-region, multi-active |
| RDS Read Replicas | Async replication to other regions |

## Disaster Recovery Metrics

| Metric | Definition |
|--------|------------|
| RTO | Recovery Time Objective - max acceptable downtime |
| RPO | Recovery Point Objective - max acceptable data loss |

## Multi-Region Best Practices

| Practice | Description |
|----------|-------------|
| Automate failover | Use Route 53 health checks |
| Regular testing | Test DR procedures |
| Data sync | Keep data replicated |
| Infrastructure as Code | Deploy consistently |
| Monitoring | Multi-region observability |

## Cost Considerations

| Cost Factor | Description |
|-------------|-------------|
| Data transfer | Cross-region transfer costs |
| Duplicate resources | Multiple region deployments |
| Storage replication | Replicated data storage |
| Standby resources | Warm/hot standby costs |

## Global Services

| Service | Description |
|---------|-------------|
| Route 53 | Global DNS |
| CloudFront | Global CDN |
| IAM | Global identity |
| Global Accelerator | Global anycast |
| WAF | Global protection |

## AWS Global Accelerator

| Feature | Description |
|---------|-------------|
| Static IPs | Two anycast IP addresses |
| Performance | Optimized routing via AWS backbone |
| Health checks | Automatic failover |
| Global reach | Route to multiple regions |

## Implementation Steps

| Step | Action |
|------|--------|
| 1 | Choose regions based on users and compliance |
| 2 | Design data replication strategy |
| 3 | Set up networking (VPC peering, TGW) |
| 4 | Configure Route 53 routing |
| 5 | Implement monitoring and alerts |
| 6 | Test failover procedures |
| 7 | Document runbooks |

## 🎯 Exam Tips

- **Active-Passive** = one region active, one standby
- **Active-Active** = multiple regions serving traffic
- **RTO** = how long can you be down
- **RPO** = how much data can you lose
- **Route 53** enables multi-region routing (failover, latency, geolocation)
- **S3 CRR** = Cross-Region Replication
- **Aurora Global** = low-latency global database
- **DynamoDB Global Tables** = multi-region, multi-active
- **Global Accelerator** = static IPs with optimized routing

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Multi-Region | Deployment across AWS regions |
| Active-Passive | Primary/standby configuration |
| Active-Active | All regions serve traffic |
| RTO | Recovery Time Objective |
| RPO | Recovery Point Objective |
| Failover | Switching to backup system |

## 💡 Key Takeaways

1. Multi-region provides disaster recovery and global performance
2. Active-passive is cost-effective, active-active offers higher availability
3. RTO and RPO drive architecture decisions
4. Route 53 enables global traffic routing
5. AWS services support cross-region replication
6. Global Accelerator provides static IPs with optimized routing
7. Regular testing of DR procedures is essential

---

*Next: [Lesson 11 - AWS Compute Services](../../lesson-11-aws-compute-services/01-amazon-ec2-overview/readme.md)*

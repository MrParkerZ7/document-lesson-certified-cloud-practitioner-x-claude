# ⚡ Performance Efficiency Pillar

## File Structure

```
lesson-02-aws-well-architected-framework/
└── 05-performance-efficiency-pillar/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Overview

The **Performance Efficiency** pillar focuses on using computing resources efficiently to meet system requirements, and maintaining that efficiency as demand changes and technologies evolve.

## Definition

> Performance Efficiency is the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.

## Design Principles

| Principle | Description |
|-----------|-------------|
| **Democratize advanced technologies** | Use managed services instead of building yourself |
| **Go global in minutes** | Deploy in multiple regions for lower latency |
| **Use serverless architectures** | Remove operational burden of servers |
| **Experiment more often** | Use automation to test different configurations |
| **Consider mechanical sympathy** | Understand how cloud services work |

## Key Focus Areas

```
┌───────────────────────────────────────────────────────────────────────┐
│                    Performance Efficiency Pillar                       │
├───────────────────────────────────────────────────────────────────────┤
│                                                                        │
│   ┌───────────────┐  ┌───────────────┐  ┌───────────────┐            │
│   │    Selection  │  │    Review     │  │   Monitoring  │            │
│   │               │  │               │  │               │            │
│   │ Choose right  │  │ Continuously  │  │ Monitor and   │            │
│   │ resources for │  │ evaluate new  │  │ identify      │            │
│   │ workload      │  │ services      │  │ improvements  │            │
│   └───────────────┘  └───────────────┘  └───────────────┘            │
│                                                                        │
│   ┌───────────────────────────────────────────────────────────────┐  │
│   │                        Trade-offs                              │  │
│   │   Balance consistency, durability, space vs time, latency     │  │
│   └───────────────────────────────────────────────────────────────┘  │
│                                                                        │
└───────────────────────────────────────────────────────────────────────┘
```

## Best Practices

### 1. Selection
Choose the right resource type and size based on:
- **Compute** - EC2 instances, containers, serverless (Lambda)
- **Storage** - S3, EBS (different types), EFS, FSx
- **Database** - RDS, DynamoDB, Aurora, ElastiCache
- **Networking** - VPC, CloudFront, Route 53

### 2. Review
- Stay current with new AWS services
- Use AWS Well-Architected Tool regularly
- Benchmark and load test

### 3. Monitoring
- Use CloudWatch for metrics
- Implement alarms for performance thresholds
- Use X-Ray for tracing

### 4. Trade-offs
- Consider **caching** for frequently accessed data
- Use **read replicas** to reduce database load
- Balance **cost vs performance**

## Compute Options

| Option | Use Case | Benefits |
|--------|----------|----------|
| **EC2 Instances** | Full control, specific requirements | Flexible, customizable |
| **Containers (ECS/EKS)** | Microservices, portability | Consistent, efficient |
| **Serverless (Lambda)** | Event-driven, variable load | No server management |
| **Batch** | Large-scale batch processing | Cost-effective for batches |

## Storage Performance

```
                    Performance vs Cost Trade-off

    ┌─────────────────────────────────────────────────────────┐
    │  io2 Block Express (EBS)                                │ High IOPS
    ├─────────────────────────────────────────────────────────┤
    │  io1/io2 (EBS)                    Provisioned IOPS     │
    ├─────────────────────────────────────────────────────────┤
    │  gp3 (EBS)                        General Purpose      │
    ├─────────────────────────────────────────────────────────┤
    │  st1 (EBS)                        Throughput Optimized │
    ├─────────────────────────────────────────────────────────┤
    │  sc1 (EBS)                        Cold Storage         │ Low Cost
    └─────────────────────────────────────────────────────────┘
```

## Database Performance

| Scenario | Solution |
|----------|----------|
| **High read traffic** | Read Replicas, ElastiCache |
| **High write traffic** | Provisioned IOPS, DynamoDB |
| **Global users** | Aurora Global, DynamoDB Global Tables |
| **Complex queries** | Amazon Redshift |
| **In-memory caching** | ElastiCache (Redis/Memcached) |

## Caching Strategies

```
                          User Request
                               │
                               ▼
                        ┌──────────────┐
                        │ CloudFront   │  ← Edge Caching
                        │ (CDN)        │
                        └──────┬───────┘
                               │
                        ┌──────▼───────┐
                        │ ElastiCache  │  ← Application Cache
                        │ (Redis)      │
                        └──────┬───────┘
                               │
                        ┌──────▼───────┐
                        │ Database     │  ← Data Store
                        │ (RDS/Dynamo) │
                        └──────────────┘
```

## AWS Services for Performance

| Category | Services |
|----------|----------|
| **Compute** | EC2, Lambda, ECS, EKS, Fargate |
| **Storage** | S3 (Intelligent-Tiering), EBS, EFS |
| **Database** | RDS, DynamoDB, Aurora, ElastiCache |
| **Networking** | CloudFront, Global Accelerator, Route 53 |
| **Monitoring** | CloudWatch, X-Ray |

## Performance Testing

Best practices for performance testing:
1. **Baseline measurement** - Establish current performance
2. **Load testing** - Test under expected load
3. **Stress testing** - Test beyond expected limits
4. **Synthetic monitoring** - Continuous testing from multiple locations

## 🎯 Exam Tips

- Know the different **EC2 instance types** (compute, memory, storage optimized)
- Understand **EBS volume types** and their use cases
- **CloudFront** reduces latency for global users
- **ElastiCache** improves database read performance
- **Read Replicas** offload read traffic from primary database
- **Lambda** is the go-to serverless compute option

## 💡 Key Takeaways

1. **Right-size resources** - Don't over or under provision
2. **Use caching** - CloudFront, ElastiCache reduce latency
3. **Go serverless** - When appropriate, use Lambda
4. **Monitor constantly** - Use CloudWatch metrics
5. **Review regularly** - New AWS services may improve performance
6. **Test thoroughly** - Load test before production

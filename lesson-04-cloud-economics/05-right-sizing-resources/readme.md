# Right-Sizing Resources

## Overview

**Right-sizing** is the process of matching instance types and sizes to workload performance and capacity requirements at the lowest possible cost. It is one of the most effective ways to reduce AWS costs while maintaining optimal performance.

## What is Right-Sizing?

```
┌─────────────────────────────────────────────────────────────────────────┐
│                       Right-Sizing Concept                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Over-Provisioned          Right-Sized            Under-Provisioned    │
│   ─────────────────         ───────────            ──────────────────   │
│                                                                          │
│   ┌─────────────────┐      ┌─────────────┐        ┌─────────────┐       │
│   │                 │      │             │        │█████████████│       │
│   │    Capacity     │      │  Capacity   │        │█████████████│       │
│   │   ─────────     │      │  ─────────  │        │█ Capacity ██│       │
│   │   ████████      │      │  ███████████│        │█████████████│       │
│   │   ██Usage█      │      │  ██Usage████│        │█████████████│       │
│   │   ████████      │      │  ███████████│        │█████████████│       │
│   │                 │      │             │        │  (Overwhelmed)      │
│   └─────────────────┘      └─────────────┘        └─────────────┘       │
│                                                                          │
│   Wasting money            Optimal cost           Poor performance      │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## EC2 Instance Types

### Instance Family Categories

| Category | Instance Families | Use Case |
|----------|------------------|----------|
| **General Purpose** | T3, T3a, M5, M6i | Balanced compute, memory, networking |
| **Compute Optimized** | C5, C6i, C7g | CPU-intensive workloads |
| **Memory Optimized** | R5, R6i, X1, X2 | Memory-intensive workloads |
| **Storage Optimized** | I3, D2, H1 | High sequential read/write |
| **Accelerated Computing** | P4, G4, Inf1 | Machine learning, graphics |

### Instance Naming Convention

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Instance Type Naming                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│                        m5.2xlarge                                        │
│                        │ │  │                                            │
│                        │ │  └── Size (nano, micro, small, medium,       │
│                        │ │      large, xlarge, 2xlarge, etc.)           │
│                        │ │                                               │
│                        │ └───── Generation (higher = newer/better)      │
│                        │                                                 │
│                        └─────── Family (m = general purpose,            │
│                                         c = compute optimized,          │
│                                         r = memory optimized, etc.)     │
│                                                                          │
│   Examples:                                                              │
│   - t3.micro    = General purpose, gen 3, micro size                    │
│   - c5.4xlarge  = Compute optimized, gen 5, 4xlarge size                │
│   - r5.large    = Memory optimized, gen 5, large size                   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Instance Size Scaling

| Size | vCPUs (typical) | Memory (typical) |
|------|-----------------|------------------|
| nano | 1-2 | 0.5 GB |
| micro | 1-2 | 1 GB |
| small | 1-2 | 2 GB |
| medium | 2 | 4 GB |
| large | 2 | 8 GB |
| xlarge | 4 | 16 GB |
| 2xlarge | 8 | 32 GB |
| 4xlarge | 16 | 64 GB |

**Note**: Each size up typically doubles resources and cost.

## AWS Compute Optimizer

### What is Compute Optimizer?

**AWS Compute Optimizer** uses machine learning to analyze historical utilization metrics and provide recommendations for optimal AWS resource configurations.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    AWS Compute Optimizer                                 │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ┌─────────────────┐                                                   │
│   │  CloudWatch     │──────┐                                            │
│   │  Metrics        │      │                                            │
│   └─────────────────┘      │      ┌─────────────────────────────┐      │
│                            │      │                             │      │
│   ┌─────────────────┐      ├─────►│   Compute Optimizer        │      │
│   │  Usage Patterns │──────┤      │   (Machine Learning)       │      │
│   │                 │      │      │                             │      │
│   └─────────────────┘      │      │   Analyzes:                │      │
│                            │      │   - CPU utilization         │      │
│   ┌─────────────────┐      │      │   - Memory utilization      │      │
│   │  Resource       │──────┘      │   - Network throughput      │      │
│   │  Configuration  │             │   - Disk I/O                │      │
│   └─────────────────┘             └──────────────┬──────────────┘      │
│                                                   │                     │
│                                                   ▼                     │
│                                   ┌─────────────────────────────┐      │
│                                   │   Recommendations           │      │
│                                   │   - Optimal instance type   │      │
│                                   │   - Estimated savings       │      │
│                                   │   - Performance risk        │      │
│                                   └─────────────────────────────┘      │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Supported Resources

| Resource Type | What It Analyzes |
|---------------|------------------|
| **EC2 Instances** | Instance type, size optimization |
| **Auto Scaling Groups** | Configuration and instance mix |
| **EBS Volumes** | Volume type, size, IOPS |
| **Lambda Functions** | Memory size allocation |
| **ECS Services (Fargate)** | Task CPU and memory |

### Recommendation Types

```
┌─────────────────────────────────────────────────────────────────────────┐
│                 Compute Optimizer Recommendations                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   1. UNDER-PROVISIONED                                                  │
│      ─────────────────                                                  │
│      Current: m5.large (High CPU/Memory usage)                          │
│      Recommended: m5.xlarge                                              │
│      Action: Scale UP for better performance                            │
│                                                                          │
│   2. OVER-PROVISIONED                                                   │
│      ────────────────                                                   │
│      Current: m5.2xlarge (Low CPU/Memory usage)                         │
│      Recommended: m5.large                                               │
│      Action: Scale DOWN to save costs                                   │
│      Savings: ~$150/month                                                │
│                                                                          │
│   3. OPTIMIZED                                                          │
│      ─────────                                                          │
│      Current: m5.xlarge                                                  │
│      Status: Already optimal                                             │
│      Action: No changes needed                                           │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Cost Explorer Right-Sizing Recommendations

### How It Works

**AWS Cost Explorer** also provides right-sizing recommendations based on historical usage data.

| Feature | Description |
|---------|-------------|
| **Analysis Period** | 14 days of usage data |
| **Recommendation Basis** | CPU and memory utilization |
| **Cost Impact** | Shows estimated monthly savings |
| **RI/SP Awareness** | Considers existing commitments |

### Accessing Recommendations

1. Open **AWS Cost Management Console**
2. Navigate to **Cost Explorer**
3. Select **Right Sizing Recommendations**
4. Review and implement recommendations

## Right-Sizing Best Practices

### Continuous Right-Sizing Process

```
┌─────────────────────────────────────────────────────────────────────────┐
│                   Right-Sizing Process                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│      ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐       │
│      │         │     │         │     │         │     │         │       │
│      │ Monitor │────►│ Analyze │────►│ Resize  │────►│ Validate│       │
│      │         │     │         │     │         │     │         │       │
│      └─────────┘     └─────────┘     └─────────┘     └─────────┘       │
│           │                                               │              │
│           │                                               │              │
│           └───────────────────────────────────────────────┘              │
│                         (Continuous Loop)                                │
│                                                                          │
│   Step 1: Monitor - Collect CloudWatch metrics                          │
│   Step 2: Analyze - Use Compute Optimizer or Cost Explorer              │
│   Step 3: Resize  - Implement recommended changes                       │
│   Step 4: Validate - Verify performance and savings                     │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Key Metrics to Monitor

| Metric | Significance |
|--------|--------------|
| **CPU Utilization** | Low = over-provisioned, High = under-provisioned |
| **Memory Utilization** | Enable CloudWatch agent for detailed metrics |
| **Network I/O** | May indicate need for different instance type |
| **Disk I/O** | Affects storage optimized decisions |
| **GPU Utilization** | For accelerated computing instances |

### Right-Sizing Strategies

1. **Start Small, Scale Up**
   - Begin with smaller instances
   - Scale up based on actual demand
   - Avoid guessing requirements

2. **Use T-Series for Variable Workloads**
   - Burstable instances for inconsistent usage
   - Cost-effective for low average utilization
   - CPU credits accumulate during idle times

3. **Consider Graviton Instances**
   - ARM-based processors (better price/performance)
   - Up to 40% better price/performance vs x86
   - Instance families: M6g, C6g, R6g, T4g

4. **Leverage Spot Instances**
   - For fault-tolerant workloads
   - Up to 90% discount
   - Combine with right-sizing for maximum savings

## Practical Examples

### Example 1: Over-Provisioned Web Server

```
Current State:
┌────────────────────────────────────────┐
│ Instance: m5.4xlarge                   │
│ vCPUs: 16                              │
│ Memory: 64 GB                          │
│ Average CPU: 10%                       │
│ Average Memory: 15%                    │
│ Cost: $560/month                       │
└────────────────────────────────────────┘
                    │
                    ▼ Compute Optimizer Recommendation
                    │
┌────────────────────────────────────────┐
│ Instance: m5.large                     │
│ vCPUs: 2                               │
│ Memory: 8 GB                           │
│ Projected CPU: 80%                     │
│ Projected Memory: 60%                  │
│ Cost: $70/month                        │
│ SAVINGS: $490/month (87%)              │
└────────────────────────────────────────┘
```

### Example 2: Under-Provisioned Database

```
Current State:
┌────────────────────────────────────────┐
│ Instance: r5.large                     │
│ vCPUs: 2                               │
│ Memory: 16 GB                          │
│ Average CPU: 95%                       │
│ Average Memory: 90%                    │
│ Performance: Degraded                  │
└────────────────────────────────────────┘
                    │
                    ▼ Compute Optimizer Recommendation
                    │
┌────────────────────────────────────────┐
│ Instance: r5.xlarge                    │
│ vCPUs: 4                               │
│ Memory: 32 GB                          │
│ Projected CPU: 48%                     │
│ Projected Memory: 45%                  │
│ Performance: Improved                  │
│ Additional Cost: Worth the performance │
└────────────────────────────────────────┘
```

## Comparison Table

| Tool | Focus | Analysis Period | Cost |
|------|-------|-----------------|------|
| **Compute Optimizer** | Resource optimization | 14 days | Free |
| **Cost Explorer Recommendations** | Cost savings | 14 days | Free (with Cost Explorer) |
| **Trusted Advisor** | Idle/underutilized resources | Various | Depends on Support Plan |
| **CloudWatch** | Raw metrics | Customizable | Pay per metric |

## Exam Tips

- **Right-sizing** = matching instance size to workload requirements
- **AWS Compute Optimizer** = ML-based recommendations for optimal sizing
- **Cost Explorer** also provides right-sizing recommendations
- Know the **instance families**: General (M/T), Compute (C), Memory (R), Storage (I/D)
- **Instance naming**: family + generation + size (e.g., m5.xlarge)
- Right-sizing is a **continuous process**, not a one-time activity
- **Graviton** instances offer better price/performance (ARM-based)
- **T-series** instances are burstable and good for variable workloads

## Key Takeaways

1. **Right-sizing** eliminates waste by matching resources to actual needs
2. **AWS Compute Optimizer** uses ML to analyze and recommend optimal configurations
3. **Instance families** are designed for different workload types
4. **Continuous monitoring** is essential for ongoing optimization
5. Right-sizing should happen **before** purchasing Reserved Instances
6. **Multiple tools** available: Compute Optimizer, Cost Explorer, Trusted Advisor
7. Right-sizing can result in **significant cost savings** (often 20-40%+)

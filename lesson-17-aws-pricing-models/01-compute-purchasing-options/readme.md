# 💰 Compute Purchasing Options

## File Structure

```
lesson-17-aws-pricing-models/
└── 01-compute-purchasing-options/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS offers multiple purchasing options for compute services, primarily EC2. Understanding these options is essential for optimizing costs while meeting your workload requirements. Each purchasing option offers different levels of flexibility, commitment, and savings.

## Overview of EC2 Purchasing Options

```
+------------------------------------------------------------------+
|                    EC2 PURCHASING OPTIONS                         |
+------------------------------------------------------------------+
|                                                                   |
|   SAVINGS                          COMMITMENT                     |
|   High ^                                                          |
|        |  [Spot]         - Up to 90% off, can be interrupted     |
|        |                                                          |
|        |  [Reserved/SP]  - Up to 72% off, 1-3 year commitment    |
|        |                                                          |
|        |  [Dedicated]    - Full server control, compliance needs  |
|        |                                                          |
|   None |  [On-Demand]    - Pay as you go, no commitment          |
|        +----------------------------------------------------->    |
|                           Low               High                  |
|                                                                   |
+------------------------------------------------------------------+
```

## On-Demand Instances

Pay for compute capacity by the hour or second with no long-term commitments.

| Feature | Description |
|---------|-------------|
| Billing | Per hour or per second (minimum 60 seconds) |
| Commitment | None required |
| Flexibility | Start/stop anytime |
| Best For | Short-term, unpredictable workloads |
| Discount | None (baseline pricing) |

### When to Use On-Demand

- Applications with unpredictable usage patterns
- Development and testing environments
- Short-term projects
- First-time workloads to establish baseline usage
- Applications that cannot be interrupted

## Reserved Instances (RIs)

Commit to a specific instance type for 1 or 3 years in exchange for significant discounts.

| Feature | Description |
|---------|-------------|
| Term Options | 1 year or 3 years |
| Payment Options | All Upfront, Partial Upfront, No Upfront |
| Discount | Up to 72% compared to On-Demand |
| Scope | Regional or Zonal |
| Types | Standard, Convertible |

### Reserved Instance Payment Options

```
+------------------------------------------------------------------+
|                   RI PAYMENT OPTIONS                              |
+------------------------------------------------------------------+
|                                                                   |
|   Payment Option      Upfront Cost    Monthly Cost    Discount    |
|   ----------------------------------------------------------------|
|   All Upfront         Highest         None            Maximum     |
|   Partial Upfront     Medium          Reduced         Medium      |
|   No Upfront          None            Higher          Lowest      |
|                                                                   |
|   Rule: More upfront payment = Greater discount                   |
|                                                                   |
+------------------------------------------------------------------+
```

## Savings Plans

Flexible pricing model offering lower prices in exchange for consistent usage commitment.

| Type | Description | Flexibility |
|------|-------------|-------------|
| Compute Savings Plans | Applies to EC2, Fargate, Lambda | Most flexible |
| EC2 Instance Savings Plans | Applies to specific instance family in a region | Moderate |
| SageMaker Savings Plans | Applies to SageMaker instances | SageMaker only |

### Savings Plans vs Reserved Instances

| Feature | Savings Plans | Reserved Instances |
|---------|---------------|-------------------|
| Commitment | $/hour usage | Specific instance type |
| Flexibility | Can change instance type/region/OS | Limited (Standard) or Moderate (Convertible) |
| Discount | Up to 72% | Up to 72% |
| Services | EC2, Fargate, Lambda | EC2 only |
| Simplicity | Easier to manage | More complex |

## Spot Instances

Purchase unused EC2 capacity at steep discounts, but instances can be interrupted.

| Feature | Description |
|---------|-------------|
| Discount | Up to 90% off On-Demand pricing |
| Interruption | 2-minute warning before termination |
| Pricing | Based on supply and demand |
| Best For | Fault-tolerant, flexible workloads |

### Spot Instance Use Cases

```
+------------------------------------------------------------------+
|                    SPOT INSTANCE USE CASES                        |
+------------------------------------------------------------------+
|                                                                   |
|   GOOD FOR SPOT:                   NOT GOOD FOR SPOT:             |
|   +--------------------------+     +--------------------------+   |
|   | - Batch processing       |     | - Databases              |   |
|   | - Data analysis          |     | - Critical web servers   |   |
|   | - Image/video rendering  |     | - Real-time applications |   |
|   | - CI/CD pipelines        |     | - Stateful applications  |   |
|   | - Big data workloads     |     | - Applications that      |   |
|   | - Machine learning       |     |   can't handle           |   |
|   |   training               |     |   interruption           |   |
|   +--------------------------+     +--------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Dedicated Hosts

Physical EC2 servers dedicated for your use.

| Feature | Description |
|---------|-------------|
| Control | Full visibility of sockets and physical cores |
| Licensing | Supports BYOL (Bring Your Own License) |
| Compliance | Meets regulatory requirements |
| Pricing | Per-host billing (hourly or reserved) |
| Best For | Server-bound software licenses, compliance needs |

## Dedicated Instances

Instances running on hardware dedicated to a single customer.

| Feature | Dedicated Instances | Dedicated Hosts |
|---------|---------------------|-----------------|
| Billing | Per instance | Per host |
| Socket/Core Visibility | No | Yes |
| Host Affinity | No | Yes |
| BYOL Support | Limited | Full |
| Capacity Sharing | With your account | With your account |

## Purchasing Options Comparison

| Option | Discount | Commitment | Interruption | Best For |
|--------|----------|------------|--------------|----------|
| On-Demand | None | None | No | Unpredictable workloads |
| Reserved | Up to 72% | 1-3 years | No | Steady-state workloads |
| Savings Plans | Up to 72% | 1-3 years | No | Flexible, consistent usage |
| Spot | Up to 90% | None | Yes (2-min notice) | Fault-tolerant workloads |
| Dedicated Hosts | Varies | Optional | No | Licensing, compliance |
| Dedicated Instances | Premium | None | No | Compliance requirements |

## Decision Flow for Choosing Purchasing Option

```
+------------------------------------------------------------------+
|              CHOOSING THE RIGHT PURCHASING OPTION                 |
+------------------------------------------------------------------+
|                                                                   |
|   START: What's your workload like?                               |
|          |                                                        |
|          v                                                        |
|   Is it fault-tolerant and flexible?                              |
|          |                                                        |
|   YES ---+--> Consider SPOT INSTANCES (up to 90% savings)         |
|          |                                                        |
|   NO ----v                                                        |
|   Can you commit to 1-3 years of usage?                           |
|          |                                                        |
|   YES ---+--> Do you need flexibility across services?            |
|          |     |                                                  |
|          |    YES --> SAVINGS PLANS                               |
|          |    NO ---> RESERVED INSTANCES                          |
|          |                                                        |
|   NO ----+--> ON-DEMAND INSTANCES                                 |
|                                                                   |
|   Special Case: Licensing/Compliance --> DEDICATED HOSTS          |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **On-Demand** = No commitment, pay-as-you-go, most flexible but no discount
- **Reserved Instances** = 1-3 year commitment, up to 72% discount, best for steady-state
- **Savings Plans** = Flexible commitment to $/hour, works across EC2/Fargate/Lambda
- **Spot Instances** = Up to 90% discount, can be interrupted with 2-minute notice
- **Dedicated Hosts** = Physical server, use for BYOL licenses (per-socket, per-core)
- **Dedicated Instances** = Hardware isolation without full host visibility
- Know that **3-year terms** provide greater savings than 1-year terms
- **All Upfront payment** provides the maximum discount

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| On-Demand | Pay-as-you-go pricing with no commitment |
| Reserved Instance | Discounted pricing with 1-3 year commitment |
| Savings Plan | Flexible discount model based on hourly spend commitment |
| Spot Instance | Discounted unused EC2 capacity that can be interrupted |
| Dedicated Host | Physical server dedicated to your use |
| BYOL | Bring Your Own License, using existing software licenses |
| Convertible RI | Reserved Instance that can be exchanged for different attributes |

## 💡 Key Takeaways

1. On-Demand provides maximum flexibility with no commitment but at full price
2. Reserved Instances offer up to 72% discount for 1-3 year commitments
3. Savings Plans provide similar discounts with more flexibility across services
4. Spot Instances offer up to 90% discount but can be interrupted with 2-minute notice
5. Dedicated Hosts are ideal for bring-your-own-license scenarios
6. Choose payment options based on cash flow needs (upfront = more savings)
7. Mix purchasing options to optimize costs for different workload types

---

*Next: [02 - Reserved Instance Flexibility](../02-reserved-instance-flexibility/readme.md)*

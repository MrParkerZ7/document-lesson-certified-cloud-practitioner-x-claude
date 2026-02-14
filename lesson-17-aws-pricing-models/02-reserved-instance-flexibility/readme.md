# 💰 Reserved Instance Flexibility

## File Structure

```
lesson-17-aws-pricing-models/
└── 02-reserved-instance-flexibility/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Reserved Instances (RIs) offer significant discounts compared to On-Demand pricing, but they come with different levels of flexibility. Understanding the differences between Standard and Convertible RIs, regional vs zonal scope, and payment options is crucial for optimizing your AWS costs while maintaining the flexibility your workloads require.

## Standard vs Convertible Reserved Instances

```
+------------------------------------------------------------------+
|           STANDARD vs CONVERTIBLE RESERVED INSTANCES              |
+------------------------------------------------------------------+
|                                                                   |
|   STANDARD RI                       CONVERTIBLE RI                |
|   +-------------------------+       +-------------------------+   |
|   | - Higher discount       |       | - Lower discount        |   |
|   |   (up to 72%)           |       |   (up to 66%)           |   |
|   | - Cannot change:        |       | - CAN change:           |   |
|   |   * Instance family     |       |   * Instance family     |   |
|   |   * Instance type       |       |   * Instance type       |   |
|   |   * Platform            |       |   * Platform            |   |
|   |   * Tenancy             |       |   * Tenancy             |   |
|   | - Can sell in           |       | - Cannot sell in        |   |
|   |   Marketplace           |       |   Marketplace           |   |
|   +-------------------------+       +-------------------------+   |
|                                                                   |
|   Choose: Maximum savings    vs     Future flexibility            |
|                                                                   |
+------------------------------------------------------------------+
```

## Detailed Comparison

| Feature | Standard RI | Convertible RI |
|---------|------------|----------------|
| Maximum Discount | Up to 72% | Up to 66% |
| Change Instance Family | No | Yes |
| Change Instance Size | Yes (within family) | Yes |
| Change OS/Platform | No | Yes |
| Change Tenancy | No | Yes |
| Change Scope | Yes | Yes |
| Sell in Marketplace | Yes | No |
| Exchange for New RI | No | Yes (equal or greater value) |

## Instance Size Flexibility

Standard RIs within a region automatically apply to different instance sizes within the same family.

```
+------------------------------------------------------------------+
|                 INSTANCE SIZE FLEXIBILITY                         |
+------------------------------------------------------------------+
|                                                                   |
|   You purchased: 1 x m5.2xlarge Regional RI                       |
|                                                                   |
|   Normalization Factor Conversion:                                |
|   +-------------------+--------------------+                      |
|   | Instance Size     | Normalization      |                      |
|   |                   | Factor             |                      |
|   +-------------------+--------------------+                      |
|   | nano              | 0.25               |                      |
|   | micro             | 0.5                |                      |
|   | small             | 1                  |                      |
|   | medium            | 2                  |                      |
|   | large             | 4                  |                      |
|   | xlarge            | 8                  |                      |
|   | 2xlarge           | 16                 |                      |
|   | 4xlarge           | 32                 |                      |
|   +-------------------+--------------------+                      |
|                                                                   |
|   1 x m5.2xlarge (16) = 2 x m5.xlarge (8+8) = 4 x m5.large        |
|                       = 16 x m5.small = 32 x m5.micro             |
|                                                                   |
+------------------------------------------------------------------+
```

## Regional vs Zonal Reserved Instances

| Feature | Regional RI | Zonal RI |
|---------|-------------|----------|
| Scope | Entire AWS Region | Specific Availability Zone |
| Instance Size Flexibility | Yes | No |
| Capacity Reservation | No | Yes |
| AZ Flexibility | Yes (any AZ in region) | No (specific AZ only) |
| Best For | Flexibility across AZs | Guaranteed capacity in specific AZ |

### Regional RI Benefits

```
+------------------------------------------------------------------+
|                      REGIONAL RI SCOPE                            |
+------------------------------------------------------------------+
|                                                                   |
|                    AWS Region (us-east-1)                         |
|   +-------------------------------------------------------------+ |
|   |                                                              | |
|   |   +-------------+  +-------------+  +-------------+          | |
|   |   |   AZ-1a     |  |   AZ-1b     |  |   AZ-1c     |          | |
|   |   |             |  |             |  |             |          | |
|   |   |  Instance   |  |  Instance   |  |  Instance   |          | |
|   |   |  ~~~~~~~~   |  |  ~~~~~~~~   |  |  ~~~~~~~~   |          | |
|   |   +-------------+  +-------------+  +-------------+          | |
|   |                                                              | |
|   |   Regional RI applies automatically to ANY AZ!               | |
|   |   + Instance size flexibility within family                  | |
|   |                                                              | |
|   +-------------------------------------------------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

### Zonal RI Benefits

```
+------------------------------------------------------------------+
|                       ZONAL RI SCOPE                              |
+------------------------------------------------------------------+
|                                                                   |
|                    AWS Region (us-east-1)                         |
|   +-------------------------------------------------------------+ |
|   |                                                              | |
|   |   +-------------+  +-------------+  +-------------+          | |
|   |   |   AZ-1a     |  |   AZ-1b     |  |   AZ-1c     |          | |
|   |   |             |  |             |  |             |          | |
|   |   |  Instance   |  |             |  |             |          | |
|   |   |  [RESERVED] |  |   -----     |  |   -----     |          | |
|   |   +-------------+  +-------------+  +-------------+          | |
|   |        ^                                                     | |
|   |        |                                                     | |
|   |   Zonal RI only applies here + Capacity Reserved!            | |
|   |                                                              | |
|   +-------------------------------------------------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Payment Options Explained

| Payment Option | Upfront | Monthly | Effective Discount |
|----------------|---------|---------|-------------------|
| All Upfront | 100% | $0 | Maximum (largest discount) |
| Partial Upfront | ~50% | Reduced | Medium |
| No Upfront | $0 | Full monthly | Minimum (smallest discount) |

### Payment Option Decision Guide

```
+------------------------------------------------------------------+
|                PAYMENT OPTION DECISION GUIDE                      |
+------------------------------------------------------------------+
|                                                                   |
|   Question: What's your cash flow situation?                      |
|                                                                   |
|   +---------------------------+                                   |
|   | Have capital available?   |                                   |
|   | Want maximum savings?     |-----> ALL UPFRONT                 |
|   +---------------------------+       (Highest discount)          |
|                                                                   |
|   +---------------------------+                                   |
|   | Some capital available?   |                                   |
|   | Balance savings & cash    |-----> PARTIAL UPFRONT             |
|   | flow?                     |       (Medium discount)           |
|   +---------------------------+                                   |
|                                                                   |
|   +---------------------------+                                   |
|   | Preserve cash flow?       |                                   |
|   | Still want RI savings?    |-----> NO UPFRONT                  |
|   +---------------------------+       (Lower discount, but        |
|                                        still significant)         |
|                                                                   |
+------------------------------------------------------------------+
```

## Term Length Comparison

| Term | Discount Level | Flexibility | Best For |
|------|----------------|-------------|----------|
| 1 Year | Lower | More flexibility to change | Uncertain long-term needs |
| 3 Year | Higher | Less flexibility | Stable, predictable workloads |

```
+------------------------------------------------------------------+
|                    TERM LENGTH COMPARISON                         |
+------------------------------------------------------------------+
|                                                                   |
|   SAVINGS                                                         |
|   High ^                                                          |
|        |    +----------------------------------------+            |
|        |    |              3 YEAR                    |            |
|        |    |         (Maximum Savings)              |            |
|        |    +----------------------------------------+            |
|        |                                                          |
|        |    +---------------------------+                         |
|        |    |         1 YEAR            |                         |
|        |    |     (Moderate Savings)    |                         |
|        |    +---------------------------+                         |
|        |                                                          |
|   Low  +-------------------------------------------------->       |
|                              TIME                                 |
|                                                                   |
|   Note: 3-year RIs save more but lock you in longer               |
|                                                                   |
+------------------------------------------------------------------+
```

## Convertible RI Exchange Rules

When exchanging Convertible RIs, you must follow these rules:

| Rule | Description |
|------|-------------|
| Value | New RI must be equal or greater value |
| Payment | May need to pay difference (true-up) |
| Term | Cannot reduce remaining term |
| Quantity | Can exchange for multiple smaller RIs |
| Frequency | Unlimited exchanges allowed |

## Reserved Instance Marketplace

```
+------------------------------------------------------------------+
|               RESERVED INSTANCE MARKETPLACE                       |
+------------------------------------------------------------------+
|                                                                   |
|   SELLERS                              BUYERS                     |
|   +-------------------------+          +-------------------------+|
|   | - Standard RIs only     |          | - Purchase unused RIs   ||
|   | - No Convertible RIs    |  <---->  | - Shorter terms         ||
|   | - Sell unused capacity  |          | - Potentially lower     ||
|   | - Recover investment    |          |   cost                  ||
|   +-------------------------+          +-------------------------+|
|                                                                   |
|   Note: Only Standard RIs can be sold in the Marketplace          |
|                                                                   |
+------------------------------------------------------------------+
```

## Choosing Between Standard and Convertible

| Choose Standard RI When | Choose Convertible RI When |
|-------------------------|---------------------------|
| Workload is stable and well-understood | Requirements may change |
| Maximum savings is priority | Flexibility is priority |
| Instance type won't change | May need different instance family |
| Might sell unused capacity | Don't plan to use Marketplace |
| Cost optimization is mature | Still learning usage patterns |

## 🎯 Exam Tips

- **Standard RIs** offer higher discounts (up to 72%) but less flexibility
- **Convertible RIs** offer lower discounts (up to 66%) but can exchange for different attributes
- **Regional RIs** provide AZ flexibility and instance size flexibility
- **Zonal RIs** provide capacity reservation in a specific AZ
- **All Upfront** payment provides the maximum discount
- **3-year term** provides more savings than 1-year term
- Only **Standard RIs** can be sold in the Reserved Instance Marketplace
- Instance size flexibility uses **normalization factors** based on instance size

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Standard RI | Reserved Instance with higher discount but limited modification options |
| Convertible RI | Reserved Instance that can be exchanged for different attributes |
| Regional RI | RI that applies to any AZ in a region with size flexibility |
| Zonal RI | RI that applies to a specific AZ with capacity reservation |
| Normalization Factor | Value assigned to instance sizes for size flexibility calculations |
| RI Marketplace | Platform to buy/sell unused Standard Reserved Instances |
| Capacity Reservation | Guarantee of EC2 capacity in a specific Availability Zone |

## 💡 Key Takeaways

1. Standard RIs offer up to 72% discount but cannot change instance family or platform
2. Convertible RIs offer up to 66% discount but allow exchanging for different attributes
3. Regional RIs provide flexibility across AZs and instance sizes within a family
4. Zonal RIs provide capacity reservation but no AZ or size flexibility
5. All Upfront payment provides maximum discount, No Upfront preserves cash flow
6. 3-year terms offer more savings than 1-year terms
7. Only Standard RIs can be sold in the Reserved Instance Marketplace
8. Convertible RIs can be exchanged unlimited times for equal or greater value

---

*Previous: [01 - Compute Purchasing Options](../01-compute-purchasing-options/readme.md) | Next: [03 - Storage Pricing](../03-storage-pricing/readme.md)*

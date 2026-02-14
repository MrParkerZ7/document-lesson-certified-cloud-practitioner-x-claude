# 💰 Fixed Costs vs Variable Costs

## File Structure

```
lesson-04-cloud-economics/
└── 01-fixed-costs-vs-variable-costs/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Overview

Understanding the difference between **fixed costs** and **variable costs** is fundamental to understanding cloud economics. AWS's cloud model fundamentally shifts IT spending from fixed costs to variable costs, providing significant financial flexibility.

## Definitions

| Cost Type | Definition | Characteristics |
|-----------|------------|-----------------|
| **Fixed Costs** | Costs that remain constant regardless of usage | Don't change with output, paid upfront |
| **Variable Costs** | Costs that change based on usage | Scale with consumption, pay-as-you-go |

## Traditional IT: Fixed Costs

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Traditional IT - Fixed Cost Model                     │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Capacity ▲                                                             │
│            │    ┌─────────────────────────────────────────────┐         │
│            │    │                                             │         │
│            │    │     Purchased Capacity (Fixed Cost)         │         │
│            │    │     ─────────────────────────────────       │         │
│            │    │                                             │         │
│            │    │   ╱╲  Actual Usage                          │         │
│            │    │  ╱  ╲     ╱╲                               │         │
│            │    │ ╱    ╲   ╱  ╲    ╱╲                        │         │
│            │    │╱      ╲ ╱    ╲  ╱  ╲                       │ WASTE   │
│            │    └─────────────────────────────────────────────┘         │
│            └────────────────────────────────────────────────────► Time  │
│                                                                          │
│   Problem: You pay for capacity whether you use it or not!              │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Examples of Fixed Costs in Traditional IT
- Server hardware purchases
- Data center leases
- Networking equipment
- Storage arrays
- Software licenses (perpetual)
- IT staff salaries

## AWS Cloud: Variable Costs

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      AWS Cloud - Variable Cost Model                     │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Capacity ▲                                                             │
│            │                                                             │
│            │                       Auto-scaled Capacity                  │
│            │                       matches usage!                        │
│            │       ╱╲                                                    │
│            │      ╱  ╲     ╱╲                                           │
│            │     ╱    ╲   ╱  ╲    ╱╲                                    │
│            │    ╱      ╲ ╱    ╲  ╱  ╲                                   │
│            │   ╱        ╲      ╲╱    ╲                                  │
│            │  ╱                        ╲                                 │
│            └────────────────────────────────────────────────────► Time  │
│                                                                          │
│   Benefit: Pay only for what you actually use!                          │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Examples of Variable Costs in AWS
- EC2 instance hours
- S3 storage used
- Data transfer
- Lambda function invocations
- API calls

## Comparison

| Aspect | Fixed Costs | Variable Costs |
|--------|-------------|----------------|
| **Payment Timing** | Upfront | As you use |
| **Scaling** | Difficult, slow | Easy, instant |
| **Risk** | High (over/under provision) | Low (match demand) |
| **Cash Flow** | Large capital outlays | Operational expense |
| **Flexibility** | Limited | High |
| **Waste** | Common (unused capacity) | Minimal |

## Benefits of Variable Cost Model

### 1. No Upfront Investment
```
Traditional:  💰💰💰💰💰 → Buy servers → Wait months → Use
AWS Cloud:    Start using → 💵 Pay monthly for usage
```

### 2. Scale with Demand
- **Scale up** during peak periods
- **Scale down** during quiet periods
- Only pay for what you use

### 3. Reduced Risk
- No guessing future capacity needs
- No risk of over-provisioning
- No risk of under-provisioning

### 4. Improved Cash Flow
- Convert large capital expenditures to smaller operational expenses
- Better predictability of costs
- Easier budgeting

## AWS Pricing Examples

| Service | Pricing Model | Variable Factor |
|---------|---------------|-----------------|
| **EC2** | Per hour/second | Instance running time |
| **S3** | Per GB stored | Storage amount |
| **Lambda** | Per request + duration | Function calls |
| **DynamoDB** | Per read/write unit | Database operations |
| **Data Transfer** | Per GB transferred | Network usage |

## When Fixed Costs Still Make Sense

AWS offers options that trade variable costs for predictable costs:
- **Reserved Instances** - Commit for 1-3 years for lower rates
- **Savings Plans** - Commit to usage level for discounts
- **Dedicated Hosts** - Fixed price for physical servers

These are still more flexible than traditional IT fixed costs.

## 🎯 Exam Tips

- AWS shifts IT from **fixed costs** to **variable costs**
- **Variable costs** = pay for what you use
- **Fixed costs** = pay regardless of usage
- AWS **Auto Scaling** enables true variable cost model
- Know that **Reserved Instances** trade flexibility for savings

## 💡 Key Takeaways

1. **Traditional IT** = Fixed costs (pay regardless of usage)
2. **AWS Cloud** = Variable costs (pay for what you use)
3. **Variable costs** reduce waste and risk
4. **Auto Scaling** makes variable costs practical
5. AWS offers **hybrid options** (Reserved Instances) for predictability
6. **Cash flow improves** with variable cost model

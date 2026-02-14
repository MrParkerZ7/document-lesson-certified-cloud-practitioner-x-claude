# 💰 CapEx vs OpEx

## File Structure

```
lesson-04-cloud-economics/
└── 03-capex-vs-opex/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Overview

Understanding the difference between **Capital Expenditure (CapEx)** and **Operational Expenditure (OpEx)** is fundamental to understanding how cloud computing changes IT financial management.

## Definitions

| Type | Full Name | Definition |
|------|-----------|------------|
| **CapEx** | Capital Expenditure | Upfront investment in physical assets |
| **OpEx** | Operational Expenditure | Ongoing costs to run day-to-day operations |

## CapEx (Capital Expenditure)

### Characteristics
- **Large upfront costs**
- **Long-term investment** (3-5+ years)
- **Depreciates over time**
- **Appears on balance sheet** as an asset
- **Tax treatment**: Depreciated over useful life

### Examples
```
┌─────────────────────────────────────────────────────────────────┐
│                    CapEx Examples                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   • Server hardware purchases                                    │
│   • Data center construction                                     │
│   • Network equipment                                            │
│   • Storage arrays                                               │
│   • Perpetual software licenses                                  │
│   • Building/facility purchases                                  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

## OpEx (Operational Expenditure)

### Characteristics
- **Pay-as-you-go costs**
- **Short-term, recurring**
- **Expensed immediately**
- **Appears on income statement**
- **Tax treatment**: Fully deductible in current period

### Examples
```
┌─────────────────────────────────────────────────────────────────┐
│                    OpEx Examples                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   • AWS cloud services (EC2, S3, etc.)                          │
│   • Monthly software subscriptions (SaaS)                        │
│   • Utility bills (power, internet)                             │
│   • Maintenance contracts                                        │
│   • Staff salaries                                               │
│   • Consulting services                                          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

## Comparison

| Aspect | CapEx | OpEx |
|--------|-------|------|
| **Payment** | Large upfront | Ongoing, smaller |
| **Cash Flow** | Major impact | Spread over time |
| **Ownership** | Own the asset | Pay for usage |
| **Flexibility** | Low | High |
| **Risk** | Higher (guessing future needs) | Lower (scale as needed) |
| **Tax** | Depreciate over years | Deduct immediately |
| **Balance Sheet** | Listed as asset | Not an asset |
| **Scalability** | Difficult | Easy |

## Traditional IT vs Cloud

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    CapEx vs OpEx Model                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Traditional IT (CapEx Model)                                          │
│   ─────────────────────────────                                         │
│   Year 1:  💰💰💰💰💰 (Large server purchase)                           │
│   Year 2:  💵 (Maintenance)                                              │
│   Year 3:  💵 (Maintenance)                                              │
│   Year 4:  💰💰💰💰💰 (Refresh/replace servers)                         │
│                                                                          │
│   AWS Cloud (OpEx Model)                                                │
│   ───────────────────────                                               │
│   Year 1:  💵💵 (Pay for usage)                                         │
│   Year 2:  💵💵💵 (Usage grows)                                         │
│   Year 3:  💵💵 (Usage decreases)                                       │
│   Year 4:  💵💵💵 (Usage varies)                                        │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Benefits of OpEx Model (Cloud)

### 1. Improved Cash Flow
- No large upfront investments
- Preserve capital for core business
- More predictable monthly costs

### 2. Financial Flexibility
- Scale costs with business needs
- Reduce costs during slow periods
- No long-term commitments (with on-demand)

### 3. Reduced Risk
- No obsolete hardware
- No over/under provisioning
- Easier budget adjustments

### 4. Tax Advantages
- Immediate expense deduction
- No depreciation schedules
- Simpler accounting

### 5. Agility
- Faster time to market
- Easy experimentation
- Quick scaling

## When CapEx Might Still Make Sense

| Scenario | Reason |
|----------|--------|
| **Reserved Instances** | Significant savings for predictable workloads |
| **Dedicated Hosts** | Compliance or licensing requirements |
| **Outposts** | On-premises AWS for data residency |
| **Long-term stable workloads** | Known, consistent usage patterns |

## AWS Enables CapEx to OpEx Shift

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│   On-Premises (CapEx)          AWS Cloud (OpEx)                 │
│   ─────────────────────────────────────────────────────────     │
│                                                                  │
│   Buy servers          →       EC2 On-Demand (hourly)           │
│   Buy storage          →       S3 (per GB/month)                │
│   Buy network gear     →       VPC (included)                   │
│   Buy software licenses →      AWS managed services             │
│   Build data center    →       AWS global infrastructure        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

## 🎯 Exam Tips

- **CapEx** = Upfront, own the asset, depreciate over time
- **OpEx** = Ongoing, pay for use, expense immediately
- AWS cloud model converts **CapEx to OpEx**
- **Benefits of OpEx**: Cash flow, flexibility, reduced risk
- **Reserved Instances** can be considered more like CapEx (upfront payment for future use)
- Know that cloud shifts IT spending model fundamentally

## 💡 Key Takeaways

1. **CapEx** is upfront investment in assets you own
2. **OpEx** is ongoing operational costs
3. **AWS cloud** shifts IT from CapEx to OpEx
4. **OpEx model** provides more flexibility and lower risk
5. **Cash flow improves** with OpEx (no large outlays)
6. Cloud **reduces financial risk** of technology decisions

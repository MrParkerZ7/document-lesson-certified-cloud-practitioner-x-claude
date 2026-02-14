# 💰 AWS Billing Dashboard

## File Structure

```
lesson-18-billing-and-cost-management/
└── 01-aws-billing-dashboard/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The AWS Billing Dashboard is your central hub for managing all billing-related activities in your AWS account. It provides visibility into your current charges, payment methods, invoices, and credits. Understanding the Billing Dashboard is essential for managing costs and is frequently tested on the AWS Certified Cloud Practitioner exam.

## Accessing the Billing Dashboard

The Billing Dashboard can be accessed through the AWS Management Console:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        AWS Management Console                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│    [Account Name] ▼                                                      │
│    ┌──────────────────────────┐                                         │
│    │  Account                 │                                         │
│    │  Billing Dashboard    ←──┼─── Click here to access billing         │
│    │  Security Credentials    │                                         │
│    │  Organization            │                                         │
│    │  Sign Out                │                                         │
│    └──────────────────────────┘                                         │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Billing Dashboard Components

| Component | Description |
|-----------|-------------|
| **Spend Summary** | Current month's charges and forecast |
| **Cost Breakdown** | Costs by service |
| **Top Free Tier Services** | Free tier usage status |
| **Payment Methods** | Credit cards and bank accounts |
| **Invoices** | Monthly billing statements |
| **Credits** | Promotional and support credits |
| **Tax Settings** | Tax information and exemptions |

## Spend Summary

The Spend Summary provides a quick overview of your costs:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          Spend Summary                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Current Month-to-Date                      Forecasted Month End        │
│   ┌─────────────────────┐                   ┌─────────────────────┐     │
│   │                     │                   │                     │     │
│   │      $1,234.56      │                   │      $2,500.00      │     │
│   │                     │                   │                     │     │
│   │   As of Feb 12      │                   │   Est. by Feb 28    │     │
│   └─────────────────────┘                   └─────────────────────┘     │
│                                                                          │
│   Last Month Total: $2,345.67                                           │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Invoices and Payment Methods

### Invoice Types

| Invoice Type | Description | When Generated |
|--------------|-------------|----------------|
| **Monthly Invoice** | Summarizes all charges | Beginning of each month |
| **Tax Invoice** | Tax-specific invoice | With monthly invoice |
| **Detailed Invoice** | Line-item breakdown | Available via CSV/PDF |

### Payment Methods

| Payment Option | Description | Use Case |
|----------------|-------------|----------|
| **Credit Card** | Primary payment method | Most common |
| **Debit Card** | Alternative to credit | Personal accounts |
| **Bank Account (ACH)** | Direct bank transfer | US accounts |
| **AWS Credits** | Promotional credits | Applied automatically |

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         Payment Processing                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   1. Credits Applied First                                              │
│      ↓                                                                   │
│   2. Remaining Balance                                                   │
│      ↓                                                                   │
│   3. Primary Payment Method Charged                                      │
│                                                                          │
│   ┌─────────┐     ┌─────────┐     ┌─────────────────┐                  │
│   │ Credits │ --> │ Balance │ --> │ Payment Method  │                  │
│   │  $100   │     │  $400   │     │   Credit Card   │                  │
│   └─────────┘     └─────────┘     └─────────────────┘                  │
│                                                                          │
│   Total Bill: $500                                                       │
│   Credits Applied: -$100                                                 │
│   Amount Charged: $400                                                   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## AWS Credits

AWS Credits can be obtained through various programs:

| Credit Source | Description | Typical Amount |
|---------------|-------------|----------------|
| **Promotional Credits** | Marketing promotions | Varies |
| **Support Credits** | Service disruption compensation | Based on impact |
| **Partner Credits** | Partner program benefits | Varies |
| **Training Credits** | Education/training programs | $25-$300 |
| **Startup Credits** | AWS Activate program | Up to $100,000 |

### Credit Application Order

1. Credits with earliest expiration date applied first
2. Credits cannot be transferred between accounts
3. Credits may have service restrictions

## Free Tier Tracking

The Billing Dashboard shows Free Tier usage:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        Free Tier Usage Alerts                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Service          │ Free Tier Limit  │ Current Usage │ % Used          │
│   ─────────────────┼──────────────────┼───────────────┼──────────        │
│   EC2 (t2.micro)   │ 750 hours        │ 500 hours     │ ████░░░ 67%     │
│   S3 Storage       │ 5 GB             │ 2 GB          │ ██░░░░░ 40%     │
│   Lambda Requests  │ 1M requests      │ 800K          │ ████░░░ 80%     │
│   RDS (db.t2.micro)│ 750 hours        │ 750 hours     │ ███████ 100%⚠️  │
│                                                                          │
│   ⚠️ Warning: RDS has exceeded Free Tier limit                          │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## AWS Billing Preferences

Key settings available in Billing Preferences:

| Preference | Description | Recommendation |
|------------|-------------|----------------|
| **Receive PDF Invoice by Email** | Email monthly invoices | Enable |
| **Receive Free Tier Usage Alerts** | Notifications when approaching limits | Enable |
| **Receive Billing Alerts** | CloudWatch billing alarms | Enable |

## IAM Access to Billing

By default, only the root user can access billing information. To grant IAM users access:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     Enabling IAM Billing Access                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Step 1: Root User enables IAM access to billing                       │
│   ┌─────────────────────────────────────────────────────────────────┐  │
│   │  My Account > IAM User and Role Access to Billing Information    │  │
│   │  [✓] Activate IAM Access                                         │  │
│   └─────────────────────────────────────────────────────────────────┘  │
│                                                                          │
│   Step 2: Attach billing permissions to IAM users/groups                │
│   ┌─────────────────────────────────────────────────────────────────┐  │
│   │  aws-portal:ViewBilling       - View billing pages               │  │
│   │  aws-portal:ViewPaymentMethods - View payment methods            │  │
│   │  aws-portal:ModifyBilling     - Modify billing settings          │  │
│   └─────────────────────────────────────────────────────────────────┘  │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Billing Dashboard vs Other Cost Tools

| Feature | Billing Dashboard | Cost Explorer | Budgets |
|---------|-------------------|---------------|---------|
| **Current Charges** | ✓ | ✓ | ✓ |
| **Payment Methods** | ✓ | ✗ | ✗ |
| **Invoices** | ✓ | ✗ | ✗ |
| **Historical Analysis** | Limited | ✓ | ✗ |
| **Cost Forecasting** | Basic | Advanced | ✓ |
| **Alerts** | Basic | ✗ | ✓ |
| **Credits Management** | ✓ | ✗ | ✗ |

## 🎯 Exam Tips

- The **Billing Dashboard** is the central location for all billing activities
- **Root user** must enable IAM access to billing for other users
- **Credits** are applied automatically and use earliest expiration first
- **Free Tier alerts** help prevent unexpected charges
- Know the difference between **Billing Dashboard**, **Cost Explorer**, and **Budgets**
- **Invoices** are generated at the beginning of each month for the previous month
- **Payment methods** include credit cards, debit cards, and bank accounts (ACH)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Billing Dashboard | Central console for managing AWS billing and payments |
| Invoice | Monthly statement of AWS charges |
| AWS Credits | Promotional or compensation credits that offset charges |
| Free Tier | Limited usage of select services at no charge |
| Spend Summary | Overview of current and forecasted costs |
| Payment Method | Credit card, debit card, or bank account for payment |

## 💡 Key Takeaways

1. The Billing Dashboard provides visibility into current charges, invoices, and payment methods
2. Root user must enable IAM access for other users to view billing information
3. AWS Credits are applied automatically before charging payment methods
4. Free Tier usage can be tracked to avoid unexpected charges
5. Enable billing alerts and Free Tier notifications to monitor spending
6. Invoices are generated monthly and available in PDF and CSV formats

---

*Next: [02 - Cost Management Tools](../02-cost-management-tools/readme.md)*

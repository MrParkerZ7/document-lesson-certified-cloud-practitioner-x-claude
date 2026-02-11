# 📊 Cost Management Tools

## Introduction

AWS provides a suite of powerful cost management tools to help you understand, analyze, and control your AWS spending. For the AWS Certified Cloud Practitioner exam, you need to understand the key differences between Cost Explorer, AWS Budgets, and Cost and Usage Reports, as well as when to use each tool.

## Overview of AWS Cost Management Tools

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    AWS Cost Management Ecosystem                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐       │
│   │  Cost Explorer  │   │   AWS Budgets   │   │  Cost & Usage   │       │
│   │                 │   │                 │   │    Reports      │       │
│   ├─────────────────┤   ├─────────────────┤   ├─────────────────┤       │
│   │ Visualize costs │   │ Set spending    │   │ Detailed data   │       │
│   │ Analyze trends  │   │ thresholds      │   │ for analysis    │       │
│   │ Forecast usage  │   │ Get alerts      │   │ S3 export       │       │
│   └────────┬────────┘   └────────┬────────┘   └────────┬────────┘       │
│            │                     │                      │                │
│            v                     v                      v                │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │                    Informed Cost Decisions                       │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## AWS Cost Explorer

AWS Cost Explorer is a visual tool for understanding and analyzing your AWS costs and usage over time.

### Key Features

| Feature | Description |
|---------|-------------|
| **Cost Visualization** | Interactive graphs and charts of spending |
| **Filtering** | Filter by service, region, account, tag |
| **Forecasting** | Predict future costs based on historical data |
| **Savings Plans Recommendations** | Identify savings opportunities |
| **Reservation Recommendations** | Suggest Reserved Instance purchases |
| **Granularity** | Daily, monthly, or hourly (with additional cost) |

### Cost Explorer Views

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        AWS Cost Explorer                                 │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Cost ($)                                                               │
│   ▲                                                                      │
│   │                              ╭─────╮                                 │
│   │                         ╭────╯     ╰────╮                           │
│   │                    ╭────╯               ╰────╮     Forecast         │
│   │        ╭───────────╯                         ╰─ ─ ─ ─ ─ ─ ─ ─       │
│   │   ╭────╯                                                             │
│   │───╯                                                                  │
│   └─────────────────────────────────────────────────────────────────►   │
│        Jan    Feb    Mar    Apr    May    Jun    Jul    Aug    Sep      │
│                                                                          │
│   Legend: ━━━ EC2   ━━━ RDS   ━━━ S3   ━━━ Lambda   - - - Forecast     │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Cost Explorer Filters

| Filter Type | Examples |
|-------------|----------|
| **Service** | EC2, S3, RDS, Lambda |
| **Linked Account** | Different accounts in organization |
| **Region** | us-east-1, eu-west-1 |
| **Instance Type** | t2.micro, m5.large |
| **Tag** | Environment:Production, Project:WebApp |
| **Usage Type** | DataTransfer, Requests, Storage |

### Cost Explorer Pricing

| Feature | Cost |
|---------|------|
| **Standard Access** | Free |
| **Hourly Granularity** | Additional charge |
| **API Access** | $0.01 per request |

## AWS Budgets

AWS Budgets allows you to set custom budgets and receive alerts when you exceed or are forecasted to exceed your thresholds.

### Budget Types

| Budget Type | Description | Use Case |
|-------------|-------------|----------|
| **Cost Budget** | Track actual spending | Monitor monthly costs |
| **Usage Budget** | Track resource usage | Monitor EC2 hours, S3 storage |
| **Savings Plans Budget** | Track Savings Plans utilization | Ensure commitments are used |
| **Reservation Budget** | Track RI utilization | Ensure RIs are used |

### Budget Alert Thresholds

```
┌─────────────────────────────────────────────────────────────────────────┐
│                       AWS Budgets - Alert Example                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Monthly Cost Budget: $10,000                                           │
│                                                                          │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │                                                                  │   │
│   │  $0        $5,000       $7,500      $10,000     $12,000+        │   │
│   │  ├─────────────┼────────────┼───────────┼───────────┤           │   │
│   │                             │           │                        │   │
│   │                             │           │                        │   │
│   │                          75% Alert   100% Alert                  │   │
│   │                          (Warning)   (Critical)                  │   │
│   │                                                                  │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│   Alert Types:                                                           │
│   • Actual: When actual spending crosses threshold                       │
│   • Forecasted: When forecast predicts crossing threshold               │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Budget Alert Actions

| Action Type | Description |
|-------------|-------------|
| **Email Notification** | Send alert to email addresses |
| **SNS Topic** | Publish to SNS for integration |
| **AWS Chatbot** | Send to Slack or Chime |
| **Budget Actions** | Automatically apply IAM or SCP policies |

### AWS Budgets Pricing

| Feature | Cost |
|---------|------|
| **First 2 budgets** | Free |
| **Additional budgets** | $0.02 per budget per day |
| **Budget actions** | Additional charges may apply |

## AWS Cost and Usage Reports (CUR)

AWS Cost and Usage Reports provide the most comprehensive set of AWS cost and usage data, delivered to an S3 bucket.

### Key Features

| Feature | Description |
|---------|-------------|
| **Comprehensive Data** | Most detailed cost data available |
| **S3 Delivery** | Reports stored in your S3 bucket |
| **Integration** | Works with Athena, Redshift, QuickSight |
| **Granularity** | Hourly, daily, or monthly |
| **Resource-Level** | Track costs per resource ID |

### CUR Data Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Cost and Usage Report Pipeline                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ┌────────────┐      ┌────────────┐      ┌────────────────────────┐    │
│   │    AWS     │      │    S3      │      │   Analysis Tools       │    │
│   │  Billing   │ ───► │   Bucket   │ ───► │                        │    │
│   │   Data     │      │   (CUR)    │      │  ┌──────────────────┐  │    │
│   └────────────┘      └────────────┘      │  │ Amazon Athena    │  │    │
│                                            │  ├──────────────────┤  │    │
│   Generates comprehensive                  │  │ Amazon Redshift  │  │    │
│   CSV/Parquet files                        │  ├──────────────────┤  │    │
│                                            │  │ Amazon QuickSight│  │    │
│                                            │  ├──────────────────┤  │    │
│                                            │  │ Third-party BI   │  │    │
│                                            │  └──────────────────┘  │    │
│                                            └────────────────────────┘    │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### CUR Report Contents

| Data Category | Description |
|---------------|-------------|
| **Identity** | Account ID, invoice entity |
| **Bill** | Billing period, invoice ID |
| **Line Item** | Product, usage type, operation |
| **Pricing** | On-demand rates, public pricing |
| **Reservation** | RI ARN, utilization |
| **Savings Plans** | SP ARN, rate |
| **Resource** | Resource ID, tags |

### CUR Pricing

- **Report generation**: Free
- **S3 storage costs**: Standard S3 pricing applies
- **Analysis tools**: Athena, Redshift, QuickSight costs apply

## Comparing Cost Management Tools

| Feature | Cost Explorer | AWS Budgets | CUR |
|---------|---------------|-------------|-----|
| **Primary Purpose** | Visualization & Analysis | Alerting & Monitoring | Detailed Data Export |
| **Data Granularity** | Daily/Monthly (Hourly extra) | Budget period | Hourly/Daily/Monthly |
| **Alerting** | No | Yes | No |
| **Forecasting** | Yes | Yes | No |
| **Data Export** | Limited | No | Yes (S3) |
| **API Access** | Yes | Yes | Via S3 |
| **Free Tier** | Yes (basic) | 2 budgets | Yes |
| **Best For** | Understanding trends | Setting limits | Deep analysis |

## Use Cases

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         When to Use Each Tool                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   "Why did our costs increase last month?"                              │
│   └──► Use Cost Explorer to analyze and visualize                       │
│                                                                          │
│   "Alert me if we're going to exceed $10,000 this month"                │
│   └──► Use AWS Budgets with forecasted threshold                        │
│                                                                          │
│   "I need detailed line-item data for chargeback"                       │
│   └──► Use Cost and Usage Reports                                       │
│                                                                          │
│   "Which Reserved Instances should we purchase?"                        │
│   └──► Use Cost Explorer recommendations                                │
│                                                                          │
│   "Stop resources if spending exceeds budget"                           │
│   └──► Use AWS Budgets with Budget Actions                             │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## 🎯 Exam Tips

- **Cost Explorer** is for visualization and analysis of past and forecasted costs
- **AWS Budgets** is for setting thresholds and receiving alerts
- **Cost and Usage Reports** provides the most detailed data for deep analysis
- Know that Cost Explorer can provide **Savings Plans** and **Reserved Instance** recommendations
- AWS Budgets can trigger **automated actions** when thresholds are crossed
- CUR data is delivered to **S3** and can be queried with **Athena**
- First **2 budgets are free** in AWS Budgets
- Cost Explorer is **free** for basic use; hourly granularity costs extra

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Cost Explorer | Visual tool for analyzing AWS spending and usage trends |
| AWS Budgets | Service for setting cost/usage thresholds and alerts |
| Cost and Usage Reports (CUR) | Comprehensive billing data delivered to S3 |
| Forecast | Prediction of future costs based on historical usage |
| Savings Plans Recommendations | Suggestions for commitment-based discounts |
| Budget Actions | Automated responses when budget thresholds are crossed |

## 💡 Key Takeaways

1. Use Cost Explorer to visualize and analyze spending patterns and trends
2. Use AWS Budgets to set spending limits and receive alerts before overspending
3. Use Cost and Usage Reports for the most detailed billing data and chargeback
4. Cost Explorer provides recommendations for Savings Plans and Reserved Instances
5. AWS Budgets can automatically apply policies when thresholds are crossed
6. CUR integrates with Athena, Redshift, and QuickSight for advanced analysis

---

*Previous: [01 - AWS Billing Dashboard](../01-aws-billing-dashboard/readme.md) | Next: [03 - AWS Pricing Calculator](../03-aws-pricing-calculator/readme.md)*

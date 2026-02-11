# ⚠️ AWS Cost Anomaly Detection

## Introduction

AWS Cost Anomaly Detection is a service that uses machine learning to identify unusual spending patterns and alert you to unexpected cost increases. It helps prevent surprise bills by detecting cost anomalies early. Understanding this service is valuable for the AWS Certified Cloud Practitioner exam, particularly for questions about cost monitoring and optimization.

## What is AWS Cost Anomaly Detection?

AWS Cost Anomaly Detection automatically monitors your AWS spending using machine learning models to detect unusual patterns and alert you when costs deviate from expected levels.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    AWS Cost Anomaly Detection                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Normal Spending Pattern          Anomaly Detected!                     │
│                                                                          │
│   Cost ($)                         Cost ($)                              │
│   ▲                                ▲                                     │
│   │      ╭─╮   ╭─╮                │           ╭───╮  ← Anomaly          │
│   │    ╭─╯ ╰─╮╭╯ ╰╮               │     ╭─╮   │   │                     │
│   │  ╭─╯     ╰╯   ╰─╮             │   ╭─╯ ╰─╮ │   │                     │
│   │ ╭╯              ╰─╮           │ ╭─╯     ╰╮╯   │                     │
│   │─╯                 ╰──         │─╯        ╰────┘                     │
│   └─────────────────────►         └─────────────────────►               │
│        Time                            Time                              │
│                                                                          │
│   ML Model learns normal           Detects deviation                     │
│   spending patterns                and sends alert                       │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Key Features

| Feature | Description |
|---------|-------------|
| **Machine Learning** | Learns your unique spending patterns over time |
| **Automatic Detection** | No manual threshold setting required |
| **Root Cause Analysis** | Identifies services causing the anomaly |
| **Customizable Alerts** | Configure alert preferences and thresholds |
| **Multiple Monitors** | Create monitors for different segments |
| **Free Service** | No additional cost to use |

## How Cost Anomaly Detection Works

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    How Anomaly Detection Works                           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   1. Historical Data Analysis                                            │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  ML model analyzes past spending (minimum 10-14 days of data)    │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                               │                                          │
│                               ▼                                          │
│   2. Pattern Learning                                                    │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  Learns daily, weekly, and monthly spending patterns             │   │
│   │  Accounts for seasonality and growth trends                      │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                               │                                          │
│                               ▼                                          │
│   3. Continuous Monitoring                                               │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  Compares real-time spending against expected patterns           │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                               │                                          │
│                               ▼                                          │
│   4. Anomaly Detection                                                   │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  Flags spending that deviates significantly from expected        │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                               │                                          │
│                               ▼                                          │
│   5. Alert & Root Cause                                                  │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  Sends alerts with root cause analysis and affected services     │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Creating Cost Monitors

Cost monitors define what spending to track. You can create monitors for different segments of your AWS usage.

### Monitor Types

| Monitor Type | Description | Use Case |
|--------------|-------------|----------|
| **AWS Services** | Monitor all linked accounts and services | Overall organization monitoring |
| **Linked Accounts** | Monitor specific member accounts | Multi-account organizations |
| **Cost Categories** | Monitor custom cost categories | Project or team tracking |
| **Cost Allocation Tags** | Monitor by tag values | Department chargeback |

### Monitor Configuration

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Cost Monitor Configuration                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Monitor Name: Production Environment Monitor                           │
│                                                                          │
│   Monitor Type: ○ AWS Services (all accounts)                           │
│                 ● Linked Account                                         │
│                 ○ Cost Category                                          │
│                 ○ Cost Allocation Tag                                    │
│                                                                          │
│   Selected Accounts:                                                     │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  [✓] 123456789012 - Production Account                          │   │
│   │  [✓] 234567890123 - Production Database Account                 │   │
│   │  [ ] 345678901234 - Development Account                         │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│   Alert Subscription: Production-Alerts (SNS + Email)                   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Alert Subscriptions

Alert subscriptions define how you want to be notified when anomalies are detected.

| Notification Method | Description |
|---------------------|-------------|
| **Email** | Direct email notifications |
| **SNS Topic** | Publish to Amazon SNS for integration |
| **AWS Chatbot** | Send to Slack or Amazon Chime |

### Alert Configuration Options

| Setting | Description |
|---------|-------------|
| **Alert Threshold** | Minimum dollar amount to trigger alert |
| **Anomaly Score** | Confidence level of the anomaly |
| **Frequency** | Individual alerts or daily summary |

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Alert Subscription Settings                           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Subscription Name: Prod-Cost-Alerts                                    │
│                                                                          │
│   Alert Frequency: ● Individual alerts                                   │
│                    ○ Daily summary                                       │
│                    ○ Weekly summary                                      │
│                                                                          │
│   Threshold Settings:                                                    │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │                                                                  │   │
│   │  Alert when impact exceeds: $[ 100    ] dollars                 │   │
│   │                                                                  │   │
│   │  Alert when impact exceeds: [ 10     ] % of daily spend         │   │
│   │                                                                  │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│   Recipients:                                                            │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  [✓] Email: cloudops@company.com                                │   │
│   │  [✓] SNS Topic: arn:aws:sns:us-east-1:123456789012:cost-alerts │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Root Cause Analysis

When an anomaly is detected, Cost Anomaly Detection provides root cause analysis to help you understand what caused the unusual spending.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Anomaly Alert - Root Cause Analysis                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ⚠️ ANOMALY DETECTED                                                    │
│                                                                          │
│   Detection Date: February 12, 2026                                      │
│   Anomaly Duration: Feb 10 - Feb 12 (3 days)                            │
│   Total Impact: $2,450 (above expected)                                  │
│   Anomaly Score: 95% (High Confidence)                                  │
│                                                                          │
│   ROOT CAUSE BREAKDOWN:                                                  │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │                                                                  │   │
│   │  Primary Driver (78% of anomaly):                               │   │
│   │  ┌─────────────────────────────────────────────────────────┐   │   │
│   │  │  Service: Amazon EC2                                     │   │   │
│   │  │  Region: us-east-1                                       │   │   │
│   │  │  Usage Type: RunInstances                                │   │   │
│   │  │  Linked Account: 123456789012 (Production)               │   │   │
│   │  └─────────────────────────────────────────────────────────┘   │   │
│   │                                                                  │   │
│   │  Contributing Factors:                                          │   │
│   │  • 15 new c5.2xlarge instances launched                        │   │
│   │  • Expected: 4 instances | Actual: 19 instances                │   │
│   │                                                                  │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│   [View in Cost Explorer]  [Mark as Expected]  [Create Budget Alert]   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Anomaly Actions

When you receive an anomaly alert, you have several options:

| Action | Description |
|--------|-------------|
| **Investigate** | Drill down in Cost Explorer |
| **Mark as Expected** | Flag legitimate planned increases |
| **Create Budget** | Set a budget to prevent recurrence |
| **Take Action** | Address the root cause (e.g., terminate resources) |

## Cost Anomaly Detection vs AWS Budgets

| Feature | Cost Anomaly Detection | AWS Budgets |
|---------|------------------------|-------------|
| **Detection Method** | ML-based pattern analysis | Fixed thresholds |
| **Setup** | Automatic learning | Manual threshold setting |
| **Flexibility** | Adapts to changing patterns | Static thresholds |
| **Root Cause** | Yes, built-in | No |
| **Proactive** | Detects unusual patterns | Alerts at threshold |
| **Use Case** | Unexpected anomalies | Known budget limits |

### When to Use Each

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    When to Use Each Service                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Use Cost Anomaly Detection when:                                       │
│   • You want to catch unexpected spending patterns                      │
│   • You don't know what "normal" looks like yet                         │
│   • You need root cause analysis                                        │
│   • You have dynamic, changing workloads                                │
│                                                                          │
│   Use AWS Budgets when:                                                  │
│   • You have a specific spending limit to enforce                       │
│   • You need to track progress against a known budget                   │
│   • You want automated actions (SCPs, IAM policies)                     │
│   • You have predictable, stable spending patterns                      │
│                                                                          │
│   BEST PRACTICE: Use both together for comprehensive cost monitoring   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Best Practices

1. **Create multiple monitors** for different segments (production, development, by project)
2. **Set appropriate thresholds** to avoid alert fatigue
3. **Use daily summaries** for non-critical environments
4. **Integrate with SNS** for automated response workflows
5. **Mark expected anomalies** to improve model accuracy
6. **Combine with AWS Budgets** for comprehensive monitoring

## 🎯 Exam Tips

- Cost Anomaly Detection uses **machine learning** to detect unusual spending patterns
- It **does NOT require manual threshold setting** - it learns automatically
- Know that it provides **root cause analysis** identifying affected services
- The service is **free** to use
- Anomaly Detection needs **10-14 days of historical data** to start working
- It can monitor by **service, account, cost category, or tags**
- Understand the difference between **Cost Anomaly Detection** (ML-based) and **AWS Budgets** (threshold-based)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Cost Anomaly Detection | ML-powered service to detect unusual AWS spending |
| Cost Monitor | Configuration defining what spending to track |
| Alert Subscription | Defines how and when you receive anomaly notifications |
| Root Cause Analysis | Breakdown of services and factors causing the anomaly |
| Anomaly Score | Confidence level that the detected pattern is unusual |
| Threshold | Minimum impact amount required to trigger an alert |

## 💡 Key Takeaways

1. AWS Cost Anomaly Detection uses machine learning to identify unusual spending patterns
2. It automatically learns your normal spending patterns without manual threshold setting
3. Root cause analysis helps identify which services and accounts caused the anomaly
4. Create multiple monitors to track different segments of your AWS usage
5. The service is free and requires 10-14 days of data to start working
6. Use Cost Anomaly Detection alongside AWS Budgets for comprehensive cost monitoring
7. Alert subscriptions can be configured for email, SNS, or AWS Chatbot

---

*Previous: [05 - Cost Allocation Tags](../05-cost-allocation-tags/readme.md)*

---

*Return to: [Lesson 18 - Billing and Cost Management](../readme.md)*

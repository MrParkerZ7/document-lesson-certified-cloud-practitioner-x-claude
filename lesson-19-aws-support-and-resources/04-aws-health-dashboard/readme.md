# 💚 AWS Health Dashboard

## Introduction

AWS Health Dashboard provides personalized information about the health of AWS services that affect your resources and accounts. It includes two main components: the Personal Health Dashboard (account-specific) and the Service Health Dashboard (all AWS services). Understanding the difference between these dashboards is essential for the AWS Certified Cloud Practitioner exam.

## Overview of AWS Health Dashboards

AWS provides two types of health dashboards:

```
┌────────────────────────────────────────────────────────────────────────────┐
│                       AWS HEALTH DASHBOARDS                                 │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   ┌────────────────────────────────────────────────────────────────┐      │
│   │              AWS Personal Health Dashboard                      │      │
│   │              (Account-Specific View)                           │      │
│   │   ┌─────────────────────────────────────────────────────┐      │      │
│   │   │  "Your EC2 instance i-12345 in us-east-1 may be    │      │      │
│   │   │   affected by scheduled maintenance on Jan 20"      │      │      │
│   │   └─────────────────────────────────────────────────────┘      │      │
│   └────────────────────────────────────────────────────────────────┘      │
│                                                                            │
│   ┌────────────────────────────────────────────────────────────────┐      │
│   │              AWS Service Health Dashboard                       │      │
│   │              (Global AWS View)                                 │      │
│   │   ┌─────────────────────────────────────────────────────┐      │      │
│   │   │  "Amazon S3 experiencing increased error rates      │      │      │
│   │   │   in us-east-1 region"                              │      │      │
│   │   └─────────────────────────────────────────────────────┘      │      │
│   └────────────────────────────────────────────────────────────────┘      │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## AWS Personal Health Dashboard

### What is Personal Health Dashboard?

The Personal Health Dashboard (PHD) provides a **personalized view** of AWS service health that directly impacts YOUR resources and accounts. It shows:

- Events affecting your specific resources
- Scheduled maintenance for your infrastructure
- Proactive notifications relevant to your environment
- Historical event information

### Key Features

| Feature | Description |
|---------|-------------|
| **Personalized Alerts** | Only shows events affecting your resources |
| **Resource-Level Detail** | Identifies specific affected resources |
| **Proactive Notifications** | Advance warning of scheduled changes |
| **Remediation Guidance** | Recommended actions to address issues |
| **Event History** | 90 days of past events |
| **Integration** | Works with CloudWatch Events and EventBridge |

### Event Types in Personal Health Dashboard

```
┌────────────────────────────────────────────────────────────────────────────┐
│                   PERSONAL HEALTH DASHBOARD EVENTS                          │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  OPEN ISSUES                                                               │
│     Currently affecting your resources                                     │
│     Example: "RDS instance in degraded state"                              │
│                                                                            │
│  SCHEDULED CHANGES                                                         │
│     Planned maintenance or updates                                         │
│     Example: "EC2 maintenance window scheduled for March 15"               │
│                                                                            │
│  OTHER NOTIFICATIONS                                                       │
│     Security advisories, service updates                                   │
│     Example: "New EC2 instance types available in your region"             │
│                                                                            │
│  EVENT LOG                                                                 │
│     Historical record of past events                                       │
│     90 days of event history                                               │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### Personal Health Dashboard Benefits

| Benefit | Description |
|---------|-------------|
| **Proactive** | Know about issues before they impact you |
| **Actionable** | Specific guidance on what to do |
| **Automated** | Integrate with workflows via EventBridge |
| **Account-Specific** | No noise from unrelated services/regions |
| **Free** | Available to all AWS accounts |

## AWS Service Health Dashboard

### What is Service Health Dashboard?

The Service Health Dashboard (SHD) provides a **global view** of AWS service availability across all regions. It shows the status of ALL AWS services, not just those you use.

### Accessing Service Health Dashboard

- **URL**: status.aws.amazon.com
- **No authentication required** - publicly accessible
- Shows current and historical service status

### Service Health Dashboard Features

| Feature | Description |
|---------|-------------|
| **Service Status** | Current health of all AWS services |
| **Region View** | Status organized by AWS region |
| **Historical Data** | RSS feeds and status history |
| **Service Icons** | Green (operational), Yellow (degraded), Red (outage) |
| **Public Access** | No AWS account needed |

### Status Indicators

```
┌────────────────────────────────────────────────────────────────────────────┐
│                    SERVICE HEALTH STATUS ICONS                              │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   Green - Service Operating Normally                                       │
│      No known issues                                                       │
│                                                                            │
│   Info - Informational Message                                             │
│      Advisory notice, no impact                                            │
│                                                                            │
│   Yellow - Service Degradation                                             │
│      Partial impact, reduced performance                                   │
│                                                                            │
│   Red - Service Disruption                                                 │
│      Significant impact to service                                         │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## Comparison: Personal vs Service Health Dashboard

| Aspect | Personal Health Dashboard | Service Health Dashboard |
|--------|--------------------------|-------------------------|
| **Scope** | Your resources only | All AWS services globally |
| **Access** | Requires AWS login | Publicly available |
| **Personalization** | Highly personalized | No personalization |
| **Resource IDs** | Shows affected resource IDs | No resource-level detail |
| **Notifications** | Proactive alerts | No direct notifications |
| **URL** | AWS Console | status.aws.amazon.com |
| **Authentication** | Required | Not required |
| **Remediation** | Specific guidance | General status only |

## Visual Comparison

```
┌──────────────────────────────────────────────────────────────────────────────┐
│           PERSONAL HEALTH vs SERVICE HEALTH DASHBOARD                        │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   PERSONAL HEALTH DASHBOARD           SERVICE HEALTH DASHBOARD               │
│   ─────────────────────────           ────────────────────────               │
│                                                                              │
│   "YOUR EC2 instance                  "EC2 service experiencing              │
│       i-12345 affected"                   issues in us-east-1"              │
│                                                                              │
│   Sends notifications                 Check website manually                 │
│                                                                              │
│   Requires login                      Publicly accessible                    │
│                                                                              │
│   Only your resources                 All AWS services                       │
│                                                                              │
│   Specific remediation                General status info                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

## AWS Health API

Available for Business, Enterprise On-Ramp, and Enterprise Support plans:

### API Capabilities

- Programmatically access health events
- Integrate with monitoring systems
- Automate responses to events
- Aggregate health data across accounts

### Use Cases

| Use Case | Description |
|----------|-------------|
| **Automated Remediation** | Trigger Lambda functions on health events |
| **Custom Dashboards** | Build organization-wide health views |
| **Ticketing Integration** | Auto-create incidents in ITSM tools |
| **Multi-Account Monitoring** | Aggregate health across AWS Organizations |

## EventBridge Integration

Personal Health Dashboard events can be sent to Amazon EventBridge for automation:

```
┌────────────────────────────────────────────────────────────────────────────┐
│                    EVENTBRIDGE INTEGRATION                                  │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   AWS Health Event                                                         │
│         │                                                                  │
│         ▼                                                                  │
│   ┌─────────────────┐                                                      │
│   │  EventBridge    │                                                      │
│   │  Rule           │                                                      │
│   └────────┬────────┘                                                      │
│            │                                                               │
│     ┌──────┴──────┬─────────────┬────────────────┐                        │
│     ▼             ▼             ▼                ▼                         │
│  ┌──────┐   ┌──────────┐   ┌───────┐   ┌────────────────┐                 │
│  │Lambda│   │SNS Topic │   │ SQS   │   │Systems Manager │                 │
│  │      │   │(Email)   │   │ Queue │   │(Automation)    │                 │
│  └──────┘   └──────────┘   └───────┘   └────────────────┘                 │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## AWS Organizations Health View

For organizations using AWS Organizations:

- **Aggregated View**: See health events across all member accounts
- **Delegated Admin**: Grant access without sharing root credentials
- **Organizational Events**: Events affecting the entire organization

## Best Practices

### For Personal Health Dashboard

1. **Enable EventBridge integration** for automated responses
2. **Set up SNS notifications** for critical events
3. **Review scheduled changes** weekly
4. **Document remediation procedures** for common events
5. **Integrate with incident management** tools

### For Service Health Dashboard

1. **Bookmark status.aws.amazon.com** for quick access
2. **Subscribe to RSS feeds** for services you use
3. **Check during troubleshooting** to rule out AWS issues
4. **Monitor regions** where you have resources

## 🎯 Exam Tips

- **Personal Health Dashboard** shows events affecting YOUR specific resources
- **Service Health Dashboard** shows status of ALL AWS services globally
- Personal Health Dashboard is accessible **within the AWS Console** (login required)
- Service Health Dashboard is **publicly accessible** at status.aws.amazon.com
- **AWS Health API** requires Business support plan or higher
- Personal Health Dashboard provides **proactive notifications** about scheduled maintenance
- Know the **difference**: Personal = your resources, Service = all AWS
- Both dashboards are **FREE** to access (API requires paid support)
- Personal Health Dashboard integrates with **EventBridge** for automation

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Personal Health Dashboard | Account-specific view of AWS health events affecting your resources |
| Service Health Dashboard | Public dashboard showing global AWS service status |
| Health Event | An occurrence that may affect your AWS resources or account |
| Scheduled Change | Planned maintenance or update that may affect your resources |
| AWS Health API | Programmatic access to health events (Business+ support) |
| EventBridge | Service for routing health events to automated actions |
| Open Issue | Currently active event affecting your resources |

## 💡 Key Takeaways

1. **Two dashboards**: Personal Health (your resources) vs Service Health (all AWS services)
2. **Personal Health Dashboard** shows specific resource IDs affected by events
3. **Service Health Dashboard** is publicly available without AWS login
4. **Proactive notifications** from Personal Health Dashboard help you prepare for changes
5. **EventBridge integration** enables automated responses to health events
6. **AWS Health API** (Business+ support) allows programmatic access to health data
7. Both dashboards are **free**; the API requires Business support or higher
8. Personal Health Dashboard provides **90 days** of event history

---

*Previous: [03 - AWS Trusted Advisor](../03-aws-trusted-advisor/readme.md) | Next: [05 - Technical Resources](../05-technical-resources/readme.md)*

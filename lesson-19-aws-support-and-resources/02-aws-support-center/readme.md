# 🎫 AWS Support Center

## File Structure

```
lesson-19-aws-support-and-resources/
└── 02-aws-support-center/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The AWS Support Center is the central hub for creating and managing support cases, communicating with AWS support teams, and tracking the status of your issues. Understanding how to effectively use the Support Center, including severity levels and communication channels, is important for both real-world AWS usage and the AWS Certified Cloud Practitioner exam.

## What is AWS Support Center?

AWS Support Center is a web-based console that enables you to:

- Create, manage, and track support cases
- View case history and correspondence
- Access AWS documentation and resources
- Monitor service health
- Contact AWS support through various channels

```
┌────────────────────────────────────────────────────────────────────────────┐
│                         AWS SUPPORT CENTER                                  │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   ┌─────────────────────────────────────────────────────────────────┐     │
│   │                    Create Support Case                          │     │
│   │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │     │
│   │  │  Account &  │  │  Technical  │  │  Service    │             │     │
│   │  │  Billing    │  │  Support    │  │  Limit      │             │     │
│   │  └─────────────┘  └─────────────┘  └─────────────┘             │     │
│   └─────────────────────────────────────────────────────────────────┘     │
│                                                                            │
│   ┌─────────────────────────────────────────────────────────────────┐     │
│   │                      Your Cases                                 │     │
│   │  Case ID    Subject              Status      Created           │     │
│   │  ─────────────────────────────────────────────────────────      │     │
│   │  001234     EC2 instance issue   Open        2024-01-15        │     │
│   │  001233     Billing question     Resolved    2024-01-10        │     │
│   └─────────────────────────────────────────────────────────────────┘     │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## Types of Support Cases

AWS Support Center allows you to create three types of support cases:

| Case Type | Description | Available To |
|-----------|-------------|--------------|
| **Account and Billing** | Questions about AWS bills, account management, payment issues | All customers |
| **Technical Support** | Help with AWS services, troubleshooting, configuration | Developer plan and above |
| **Service Limit Increase** | Request to increase AWS service quotas/limits | All customers |

### Account and Billing Cases

- Available to ALL AWS customers (including Basic Support)
- 24/7 access for billing inquiries
- Topics include:
  - Bill explanations
  - Payment methods
  - Account closure
  - Tax-related questions
  - Reserved Instance purchases

### Technical Support Cases

- Requires Developer support plan or higher
- Help with AWS service issues
- Architecture guidance
- Best practice recommendations
- Troubleshooting and debugging

### Service Limit Increase Cases

- Available to ALL AWS customers
- Request higher limits for:
  - EC2 instances
  - VPCs
  - S3 buckets
  - IAM roles
  - And many other service limits

## Severity Levels

AWS uses severity levels to prioritize support cases based on business impact:

```
┌────────────────────────────────────────────────────────────────────────────┐
│                         SEVERITY LEVELS                                     │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   CRITICAL ──────────► Business-critical system down                       │
│   (Level 1)            Response: 15 min (Enterprise)                       │
│                                  30 min (Enterprise On-Ramp)               │
│                                                                            │
│   URGENT ────────────► Production system down                              │
│   (Level 2)            Response: 1 hour (Business+)                        │
│                                                                            │
│   HIGH ──────────────► Production system impaired                          │
│   (Level 3)            Response: 4 hours (Business+)                       │
│                                                                            │
│   NORMAL ────────────► System impaired                                     │
│   (Level 4)            Response: 12 hours (Developer+)                     │
│                                                                            │
│   LOW ───────────────► General guidance                                    │
│   (Level 5)            Response: 24 hours (Developer+)                     │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### Detailed Severity Level Definitions

| Level | Name | Description | Business Impact |
|-------|------|-------------|-----------------|
| **Critical** | Business-critical system down | Complete loss of business functions | Revenue/reputation at immediate risk |
| **Urgent** | Production system down | Important functions unavailable | Time-sensitive issue |
| **High** | Production system impaired | Important functions degraded | Noticeable impact on productivity |
| **Normal** | System impaired | Non-critical functions affected | Development work blocked |
| **Low** | General guidance | Questions, feature requests | No immediate impact |

### Severity Level Availability by Support Plan

| Severity | Basic | Developer | Business | Enterprise On-Ramp | Enterprise |
|----------|-------|-----------|----------|-------------------|------------|
| Critical | X | X | X | 30 min | 15 min |
| Urgent | X | X | 1 hour | 1 hour | 1 hour |
| High | X | X | 4 hours | 4 hours | 4 hours |
| Normal | X | 12 hours | 12 hours | 12 hours | 12 hours |
| Low | X | 24 hours | 24 hours | 24 hours | 24 hours |

## Communication Channels

AWS Support offers multiple communication channels depending on your support plan:

```
┌────────────────────────────────────────────────────────────────────────────┐
│                    COMMUNICATION CHANNELS BY PLAN                          │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Plan              Web    Email    Phone    Chat    TAM    Concierge      │
│  ───────────────────────────────────────────────────────────────────      │
│  Basic              Y      X        X        X       X        X           │
│  Developer          Y      Y        X        X       X        X           │
│  Business           Y      Y        Y        Y       X        X           │
│  Enterprise On-Ramp Y      Y        Y        Y      Pool     Y           │
│  Enterprise         Y      Y        Y        Y    Dedicated  Y           │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### Channel Details

| Channel | Description | Availability |
|---------|-------------|--------------|
| **Web Console** | Create and manage cases via AWS Console | All plans |
| **Email** | Receive updates and respond via email | Developer+ |
| **Phone** | Direct voice support with AWS engineers | Business+ |
| **Chat** | Real-time text chat with AWS support | Business+ |
| **TAM** | Dedicated technical expert relationship | Enterprise tiers |
| **Concierge** | Billing and account specialists | Enterprise tiers |

## Creating a Support Case

### Step-by-Step Process

1. **Navigate to Support Center**
   - Access via AWS Console > Support > Support Center

2. **Click "Create Case"**
   - Choose case type (Account/Billing, Technical, or Service Limit)

3. **Select Service and Category**
   - Pick the AWS service related to your issue
   - Choose the specific category

4. **Set Severity Level**
   - Select appropriate severity based on impact

5. **Describe the Issue**
   - Provide detailed description
   - Include error messages, logs
   - Attach relevant files

6. **Choose Contact Method**
   - Select preferred communication channel

7. **Submit and Track**
   - Monitor case status
   - Respond to AWS communications

## Case Status Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CASE STATUS WORKFLOW                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│    ┌────────┐     ┌────────────┐     ┌────────────┐     ┌──────────┐       │
│    │  Open  │ ──► │ In Progress│ ──► │ Pending    │ ──► │ Resolved │       │
│    └────────┘     └────────────┘     │ Customer   │     └──────────┘       │
│                                      │ Action     │                         │
│                                      └────────────┘                         │
│                                            │                                │
│                                            ▼                                │
│                                      ┌────────────┐                         │
│                                      │ Reopened   │                         │
│                                      └────────────┘                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

| Status | Description |
|--------|-------------|
| **Open** | Case submitted, awaiting AWS response |
| **In Progress** | AWS actively working on the case |
| **Pending Customer Action** | AWS requires additional information |
| **Resolved** | Issue addressed, case closed |
| **Reopened** | Previously resolved case reopened |

## Best Practices for Support Cases

### Writing Effective Cases

| Do | Don't |
|----|-------|
| Provide specific error messages | Submit vague descriptions |
| Include resource IDs (instance ID, ARN) | Forget to include affected resources |
| Describe steps to reproduce | Assume AWS knows your environment |
| Attach relevant logs | Send sensitive credentials in case text |
| Set accurate severity level | Over-escalate non-critical issues |

### Information to Include

- **What** happened (error, unexpected behavior)
- **When** it occurred (timestamps in UTC)
- **Where** (region, resource IDs)
- **Impact** on your business
- **Steps** already taken to troubleshoot
- **Expected** vs actual behavior

## AWS Support API

For Business, Enterprise On-Ramp, and Enterprise support plans:

- Create, manage, and resolve cases programmatically
- Integrate support workflows with your systems
- Automate case creation for monitoring alerts
- Retrieve case history and details

## 🎯 Exam Tips

- **Basic Support** can only create billing/account cases, NOT technical support cases
- **Severity levels** determine response time commitments
- **Critical severity** (15-30 min response) is only available for Enterprise plans
- **Phone support** requires Business plan or higher
- Know that **Service Limit Increase** requests are available to ALL customers
- Understand that **response times** are based on severity level AND support plan
- **24/7 support** for technical issues requires Business plan or above
- **AWS Support API** is available for Business plan and above

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Support Case | A ticket or request for assistance from AWS Support |
| Severity Level | Classification indicating the business impact of an issue |
| Response Time | Maximum time AWS commits to initial response |
| Correspondence | Communication thread within a support case |
| Case Status | Current state of a support case (Open, Resolved, etc.) |
| Service Limit | Maximum resources AWS allows by default for a service |
| Quota Increase | Request to raise default AWS service limits |

## 💡 Key Takeaways

1. **AWS Support Center** is the central hub for creating and managing support cases
2. **Three case types**: Account/Billing (all customers), Technical (Developer+), and Service Limits (all customers)
3. **Five severity levels** range from Low (general guidance) to Critical (business down)
4. **Critical severity** with 15-minute response is only for Enterprise Support customers
5. **Communication channels** expand as you move to higher support tiers
6. **Phone and chat support** require Business plan or higher
7. Providing **detailed information** in cases leads to faster resolution
8. **Support API** enables programmatic case management for Business+ plans

---

*Previous: [01 - AWS Support Plans](../01-aws-support-plans/readme.md) | Next: [03 - AWS Trusted Advisor](../03-aws-trusted-advisor/readme.md)*

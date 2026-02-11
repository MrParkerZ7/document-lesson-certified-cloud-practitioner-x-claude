# 🏢 AWS Organizations

## Introduction

AWS Organizations is a service that enables you to centrally manage and govern multiple AWS accounts. It provides consolidated billing, hierarchical account management, and policy-based controls. Understanding AWS Organizations is critical for the AWS Certified Cloud Practitioner exam, particularly for questions about multi-account management and cost optimization.

## What is AWS Organizations?

AWS Organizations allows you to create a hierarchy of AWS accounts, apply policies across the organization, and consolidate billing into a single payment method.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        AWS Organizations Structure                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│                        ┌─────────────────────┐                          │
│                        │   Management        │                          │
│                        │   Account (Root)    │                          │
│                        │   ───────────────   │                          │
│                        │   • Pays all bills  │                          │
│                        │   • Creates OUs     │                          │
│                        │   • Applies SCPs    │                          │
│                        └─────────┬───────────┘                          │
│                                  │                                       │
│              ┌───────────────────┼───────────────────┐                  │
│              │                   │                   │                  │
│              ▼                   ▼                   ▼                  │
│   ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐       │
│   │  Production OU   │ │  Development OU  │ │   Sandbox OU     │       │
│   └────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘       │
│            │                    │                    │                  │
│     ┌──────┴──────┐      ┌──────┴──────┐      ┌──────┴──────┐          │
│     ▼             ▼      ▼             ▼      ▼             ▼          │
│  ┌──────┐     ┌──────┐ ┌──────┐    ┌──────┐ ┌──────┐    ┌──────┐      │
│  │Prod-1│     │Prod-2│ │Dev-1 │    │Dev-2 │ │Test-1│    │Test-2│      │
│  │Acct  │     │Acct  │ │Acct  │    │Acct  │ │Acct  │    │Acct  │      │
│  └──────┘     └──────┘ └──────┘    └──────┘ └──────┘    └──────┘      │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Management Account** | The primary account that creates and manages the organization |
| **Member Account** | Any account that joins the organization |
| **Organizational Unit (OU)** | Container for accounts within the organization |
| **Service Control Policy (SCP)** | Policy that defines maximum permissions for accounts |
| **Root** | Top-level container for all accounts and OUs |

## Consolidated Billing

One of the primary benefits of AWS Organizations is consolidated billing, which combines the billing from all member accounts.

### How Consolidated Billing Works

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        Consolidated Billing                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Member Account Usage:                                                  │
│                                                                          │
│   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐                   │
│   │  Account A  │   │  Account B  │   │  Account C  │                   │
│   │  ─────────  │   │  ─────────  │   │  ─────────  │                   │
│   │  EC2: $500  │   │  EC2: $300  │   │  EC2: $200  │                   │
│   │  S3: $100   │   │  S3: $150   │   │  S3: $50    │                   │
│   │  RDS: $200  │   │  RDS: $100  │   │  RDS: $150  │                   │
│   └──────┬──────┘   └──────┬──────┘   └──────┬──────┘                   │
│          │                 │                 │                           │
│          └─────────────────┼─────────────────┘                          │
│                            ▼                                             │
│                  ┌─────────────────────┐                                │
│                  │  Management Account │                                │
│                  │  ─────────────────  │                                │
│                  │  SINGLE INVOICE     │                                │
│                  │  ─────────────────  │                                │
│                  │  EC2:    $1,000     │                                │
│                  │  S3:     $300       │                                │
│                  │  RDS:    $450       │                                │
│                  │  ─────────────────  │                                │
│                  │  TOTAL:  $1,750     │                                │
│                  └─────────────────────┘                                │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Benefits of Consolidated Billing

| Benefit | Description |
|---------|-------------|
| **Single Payment** | One bill for all accounts |
| **Volume Discounts** | Combined usage qualifies for tiered pricing |
| **Cost Tracking** | View costs by account |
| **Free** | No additional cost for consolidated billing |
| **Easy Management** | Simplify payment and accounting |

### Volume Discount Example

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    S3 Volume Pricing Example                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   S3 Standard Storage Pricing (example):                                │
│   • First 50 TB/month:    $0.023 per GB                                 │
│   • Next 450 TB/month:    $0.022 per GB                                 │
│   • Over 500 TB/month:    $0.021 per GB                                 │
│                                                                          │
│   Without Consolidated Billing:          With Consolidated Billing:     │
│   ┌─────────────────────────────┐        ┌─────────────────────────────┐│
│   │ Account A: 40 TB @ $0.023   │        │ Combined: 120 TB            ││
│   │ Account B: 40 TB @ $0.023   │   ──►  │ 50 TB @ $0.023              ││
│   │ Account C: 40 TB @ $0.023   │        │ 70 TB @ $0.022 (discount!)  ││
│   └─────────────────────────────┘        └─────────────────────────────┘│
│                                                                          │
│   Savings: Aggregated usage qualifies for volume discounts              │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Service Control Policies (SCPs)

SCPs are policies that define the maximum available permissions for accounts in your organization.

### SCP Key Points

| Feature | Description |
|---------|-------------|
| **Central Control** | Define permissions from management account |
| **Restrictive Only** | SCPs can only deny, never grant permissions |
| **Inheritance** | SCPs are inherited down the OU hierarchy |
| **Override IAM** | SCPs can restrict even root user in member accounts |
| **Do Not Affect Management Account** | SCPs don't apply to management account |

### SCP vs IAM Policies

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    SCP and IAM Policy Interaction                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ┌───────────────────────────────────────────────────────────────┐     │
│   │                    Service Control Policy                      │     │
│   │                  (Maximum Permissions)                         │     │
│   │   ┌─────────────────────────────────────────────────────────┐ │     │
│   │   │                                                          │ │     │
│   │   │  Allowed Actions: EC2, S3, Lambda, RDS                  │ │     │
│   │   │                                                          │ │     │
│   │   │   ┌───────────────────────────────────────────────────┐ │ │     │
│   │   │   │            IAM Policy                              │ │ │     │
│   │   │   │         (Granted Permissions)                      │ │ │     │
│   │   │   │                                                    │ │ │     │
│   │   │   │   Granted: EC2, S3, Lambda                        │ │ │     │
│   │   │   │                                                    │ │ │     │
│   │   │   │   ┌─────────────────────────────────────────────┐ │ │ │     │
│   │   │   │   │         EFFECTIVE PERMISSIONS               │ │ │ │     │
│   │   │   │   │                                              │ │ │ │     │
│   │   │   │   │   User can use: EC2, S3, Lambda             │ │ │ │     │
│   │   │   │   │   (intersection of SCP and IAM)             │ │ │ │     │
│   │   │   │   └─────────────────────────────────────────────┘ │ │ │     │
│   │   │   └───────────────────────────────────────────────────┘ │ │     │
│   │   └─────────────────────────────────────────────────────────┘ │     │
│   └───────────────────────────────────────────────────────────────┘     │
│                                                                          │
│   Note: RDS is allowed by SCP but NOT granted by IAM, so user cannot   │
│         use RDS. Permissions are the INTERSECTION of both.              │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Example SCP

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "DenyEC2OutsideUSEast1",
            "Effect": "Deny",
            "Action": "ec2:*",
            "Resource": "*",
            "Condition": {
                "StringNotEquals": {
                    "aws:RequestedRegion": "us-east-1"
                }
            }
        }
    ]
}
```

## Organizational Units (OUs)

OUs are containers for organizing accounts within your organization.

### Common OU Structures

| OU Pattern | Purpose |
|------------|---------|
| **By Environment** | Production, Development, Testing, Sandbox |
| **By Business Unit** | Finance, Marketing, Engineering |
| **By Compliance** | Regulated, Non-Regulated |
| **By Workload** | Core Services, Data Analytics, External Apps |

### OU Best Practices

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Recommended OU Structure                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│                            Root                                          │
│                              │                                           │
│       ┌──────────────────────┼──────────────────────┐                   │
│       │                      │                      │                   │
│       ▼                      ▼                      ▼                   │
│   ┌──────────┐         ┌──────────┐          ┌──────────┐              │
│   │ Security │         │Workloads │          │ Sandbox  │              │
│   │    OU    │         │    OU    │          │    OU    │              │
│   └────┬─────┘         └────┬─────┘          └────┬─────┘              │
│        │                    │                     │                     │
│   ┌────┴────┐        ┌──────┼──────┐        ┌────┴────┐               │
│   │Log Acct │        │      │      │        │ Dev Test│               │
│   │Sec Acct │      Prod   Dev   Test        │ Accounts│               │
│   └─────────┘       OU     OU    OU         └─────────┘               │
│                                                                          │
│   Apply strict      Apply env-        Allow more                        │
│   SCPs for          specific          permissive                        │
│   security          policies          policies                          │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Reserved Instance Sharing

With consolidated billing, Reserved Instances can be shared across accounts in the organization.

| Feature | Description |
|---------|-------------|
| **Automatic Sharing** | RIs apply to matching usage across organization |
| **Disable Sharing** | Can turn off RI/Savings Plan sharing per account |
| **Cost Allocation** | Charges appear in account that used the RI |
| **Maximum Savings** | Unused RI capacity benefits the organization |

## AWS Organizations Features Summary

| Feature | Description | Free |
|---------|-------------|------|
| **Consolidated Billing** | Single bill for all accounts | Yes |
| **Organizational Units** | Group accounts hierarchically | Yes |
| **Service Control Policies** | Maximum permission boundaries | Yes |
| **Tag Policies** | Standardize tags across accounts | Yes |
| **Backup Policies** | Central backup management | Yes |
| **AI Services Opt-Out** | Control AI training data | Yes |

## 🎯 Exam Tips

- **Consolidated billing** combines all accounts into one bill for volume discounts
- **SCPs** define maximum permissions; they cannot grant permissions, only restrict
- **SCPs do NOT affect the management account** - be careful with this account
- **Reserved Instances** are shared by default across the organization
- Know the difference between **SCPs** (organization-level) and **IAM policies** (account-level)
- OUs can be **nested** up to 5 levels deep
- **Member accounts can only belong to one organization** at a time
- Consolidated billing is **free** - no additional cost

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| AWS Organizations | Service for managing multiple AWS accounts centrally |
| Management Account | The account that creates and manages the organization |
| Member Account | Any account that joins the organization |
| Organizational Unit (OU) | Container for grouping accounts |
| Service Control Policy (SCP) | Policy defining maximum permissions for accounts |
| Consolidated Billing | Single bill for all accounts with volume discounts |

## 💡 Key Takeaways

1. AWS Organizations enables central management of multiple AWS accounts
2. Consolidated billing provides a single bill and volume discounts
3. Service Control Policies set maximum permission boundaries for accounts
4. SCPs can restrict even the root user in member accounts (but not the management account)
5. Organizational Units help organize accounts hierarchically
6. Reserved Instances and Savings Plans are shared across the organization by default
7. AWS Organizations is free to use

---

*Previous: [03 - AWS Pricing Calculator](../03-aws-pricing-calculator/readme.md) | Next: [05 - Cost Allocation Tags](../05-cost-allocation-tags/readme.md)*

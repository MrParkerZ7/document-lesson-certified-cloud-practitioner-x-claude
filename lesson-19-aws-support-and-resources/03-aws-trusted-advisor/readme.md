# ✅ AWS Trusted Advisor

## Introduction

AWS Trusted Advisor is an automated service that analyzes your AWS environment and provides real-time recommendations to help you optimize your infrastructure. It inspects your resources across five key categories: Cost Optimization, Performance, Security, Fault Tolerance, and Service Limits. Understanding Trusted Advisor and its five pillars is crucial for the AWS Certified Cloud Practitioner exam.

## What is AWS Trusted Advisor?

Trusted Advisor acts as your cloud consultant, continuously monitoring your AWS environment and comparing it against AWS best practices. It provides actionable recommendations to:

- Reduce costs
- Improve performance
- Enhance security
- Increase fault tolerance
- Stay within service limits

```
┌────────────────────────────────────────────────────────────────────────────┐
│                         AWS TRUSTED ADVISOR                                 │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│                    Your AWS Environment                                    │
│                           │                                                │
│                           ▼                                                │
│                ┌─────────────────────┐                                     │
│                │   Trusted Advisor   │                                     │
│                │   Analysis Engine   │                                     │
│                └─────────────────────┘                                     │
│                           │                                                │
│           ┌───────────────┼───────────────┐                               │
│           │               │               │                                │
│           ▼               ▼               ▼                                │
│     ┌─────────┐     ┌─────────┐     ┌─────────┐                           │
│     │   Red   │     │ Yellow  │     │  Green  │                           │
│     │ Action  │     │ Invest- │     │   OK    │                           │
│     │ Required│     │ igation │     │         │                           │
│     └─────────┘     └─────────┘     └─────────┘                           │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## The Five Categories (Pillars)

### 1. Cost Optimization

Identifies opportunities to reduce your AWS spending.

| Check Type | What It Finds |
|------------|---------------|
| Idle Resources | EC2 instances, RDS databases not being used |
| Underutilized Resources | Resources with low utilization |
| Reserved Instance Coverage | Opportunities for RI purchases |
| Unattached EBS Volumes | Storage volumes not attached to instances |
| Idle Load Balancers | Load balancers with no traffic |

**Example Recommendations:**
- "You have 5 idle EC2 instances costing $500/month"
- "Consider Reserved Instances for 80% savings"
- "10 unattached EBS volumes wasting $50/month"

### 2. Performance

Recommends improvements to enhance speed and responsiveness.

| Check Type | What It Finds |
|------------|---------------|
| High Utilization | Overloaded EC2 instances |
| CloudFront Configuration | Content delivery optimization |
| EBS Provisioned IOPS | Storage performance issues |
| EC2 Instance Types | Better instance type matches |
| Database Connections | RDS connection pooling |

**Example Recommendations:**
- "EC2 instance running at 95% CPU - consider upgrading"
- "Enable CloudFront caching to reduce latency"
- "Use provisioned IOPS for database workloads"

### 3. Security

Identifies security vulnerabilities and gaps in your configuration.

| Check Type | What It Finds |
|------------|---------------|
| Security Groups | Unrestricted access (0.0.0.0/0) |
| IAM Use | Root account usage, MFA status |
| S3 Bucket Permissions | Public access settings |
| EBS/RDS Snapshots | Publicly shared snapshots |
| CloudTrail Logging | Audit trail configuration |

**Example Recommendations:**
- "Enable MFA on root account"
- "5 security groups allow unrestricted SSH access"
- "S3 bucket 'data-bucket' is publicly accessible"

### 4. Fault Tolerance

Helps improve reliability and availability of your applications.

| Check Type | What It Finds |
|------------|---------------|
| EBS Snapshots | Missing or old backups |
| RDS Multi-AZ | Single-AZ database deployments |
| EC2 Availability Zones | Resources in single AZ |
| Load Balancer Optimization | Cross-zone balancing |
| Auto Scaling Configuration | Scaling policy gaps |

**Example Recommendations:**
- "RDS instance not using Multi-AZ - single point of failure"
- "EBS volume has no recent snapshots"
- "Enable cross-zone load balancing"

### 5. Service Limits (Service Quotas)

Monitors your usage against AWS service limits.

| Check Type | What It Finds |
|------------|---------------|
| EC2 Instance Limits | Approaching instance quota |
| VPC Limits | Near maximum VPCs per region |
| EBS Volume Limits | Storage quota status |
| IAM Limits | Users, groups, roles quotas |
| RDS Limits | Database instance limits |

**Example Recommendations:**
- "80% of EC2 instance limit used in us-east-1"
- "VPC limit at 4/5 - request increase before launching"
- "EBS snapshots approaching 10,000 limit"

## Visual Summary of Five Categories

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                     TRUSTED ADVISOR FIVE PILLARS                             │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│    COST                   PERFORMANCE              SECURITY                  │
│    OPTIMIZATION                                                              │
│    ─────────────          ──────────────           ─────────                 │
│    • Idle resources       • High utilization       • Security groups        │
│    • Right-sizing         • CloudFront config      • MFA status             │
│    • Reserved capacity    • Instance types         • S3 permissions         │
│    • Unattached storage   • Database tuning        • IAM policies           │
│                                                                              │
│    FAULT TOLERANCE         SERVICE LIMITS                                    │
│    ──────────────────      ───────────────                                   │
│    • Backup status         • EC2 instances                                  │
│    • Multi-AZ usage        • VPCs per region                                │
│    • AZ distribution       • EBS volumes                                    │
│    • Load balancing        • IAM entities                                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Access by Support Plan

| Support Plan | Trusted Advisor Access |
|--------------|----------------------|
| **Basic** | 7 core security checks only |
| **Developer** | 7 core security checks only |
| **Business** | Full access - all 5 categories |
| **Enterprise On-Ramp** | Full access + API |
| **Enterprise** | Full access + API |

### The 7 Core Security Checks (Free)

Available to ALL AWS accounts:

1. **S3 Bucket Permissions** - Buckets with open access
2. **Security Groups - Specific Ports Unrestricted** - Risky open ports
3. **IAM Use** - Whether IAM is being used (vs root)
4. **MFA on Root Account** - Multi-factor authentication status
5. **EBS Public Snapshots** - Publicly shared EBS snapshots
6. **RDS Public Snapshots** - Publicly shared RDS snapshots
7. **Service Limits** - Core service limit checks

## Trusted Advisor Dashboard

```
┌────────────────────────────────────────────────────────────────────────────┐
│                    TRUSTED ADVISOR DASHBOARD                                │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Category              Red Action   Yellow Warning   Green OK    Total     │
│  ───────────────────────────────────────────────────────────────          │
│  Cost Optimization          3             5            12         20       │
│  Performance                0             2             8         10       │
│  Security                   2             3            10         15       │
│  Fault Tolerance            1             4             5         10       │
│  Service Limits             0             1            24         25       │
│  ───────────────────────────────────────────────────────────────          │
│  TOTAL                      6            15            59         80       │
│                                                                            │
│  Status Legend:                                                            │
│  Red    = Action recommended (problem detected)                            │
│  Yellow = Investigation recommended (potential issue)                      │
│  Green  = No problem detected (meets best practices)                       │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## Trusted Advisor Notifications

Configure weekly email notifications for:
- Summary of check status
- New recommendations
- Changes in resource status

## Integration with Other Services

| Service | Integration |
|---------|-------------|
| **CloudWatch** | Create alarms based on Trusted Advisor metrics |
| **Lambda** | Automate responses to recommendations |
| **SNS** | Get notifications on status changes |
| **Service Catalog** | Enforce compliance through portfolios |

## Common Use Cases

### 1. Cost Reduction Review
```
Monthly Review Workflow:
1. Open Trusted Advisor Dashboard
2. Review Cost Optimization category
3. Identify idle resources
4. Terminate or downsize unused resources
5. Track savings over time
```

### 2. Security Audit
```
Security Audit Workflow:
1. Check Security category weekly
2. Address all RED items immediately
3. Investigate YELLOW items
4. Document exceptions
5. Monitor trends
```

### 3. Pre-Launch Checklist
```
Before Production Launch:
1. Verify no critical security issues
2. Confirm fault tolerance configurations
3. Check service limits have headroom
4. Validate performance settings
5. Review cost optimization opportunities
```

## 🎯 Exam Tips

- **Know the 5 categories**: Cost Optimization, Performance, Security, Fault Tolerance, Service Limits
- **Basic and Developer** plans only get **7 core security checks**
- **Business plan and above** gets **full Trusted Advisor** access
- Trusted Advisor is **FREE** with limited checks (7 security checks)
- Remember the **color coding**: Red (action), Yellow (investigate), Green (OK)
- Trusted Advisor provides **automated best practice recommendations**
- It helps with **right-sizing** resources (cost and performance)
- **Service Limits** category helps prevent hitting AWS quotas
- Trusted Advisor can send **weekly notification emails**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Check | An individual Trusted Advisor inspection against best practices |
| Recommendation | Suggested action to improve your AWS environment |
| Core Check | One of the 7 free security checks available to all accounts |
| Status | Color-coded result (Red, Yellow, Green) indicating check result |
| Refresh | Action to update check results with current resource status |
| Suppression | Ability to hide irrelevant recommendations |
| Right-sizing | Matching resource capacity to actual workload needs |

## 💡 Key Takeaways

1. **AWS Trusted Advisor** inspects your environment and provides best practice recommendations
2. **Five categories** (pillars): Cost Optimization, Performance, Security, Fault Tolerance, Service Limits
3. **Basic/Developer support** only includes 7 core security checks
4. **Business support and above** unlocks all Trusted Advisor checks across all categories
5. **Color-coded results**: Red (action needed), Yellow (investigate), Green (no issues)
6. Helps with **cost savings** by identifying idle and underutilized resources
7. **Security checks** identify vulnerabilities like open security groups and missing MFA
8. **Service Limits** monitoring helps prevent hitting AWS quotas unexpectedly

---

*Previous: [02 - AWS Support Center](../02-aws-support-center/readme.md) | Next: [04 - AWS Health Dashboard](../04-aws-health-dashboard/readme.md)*

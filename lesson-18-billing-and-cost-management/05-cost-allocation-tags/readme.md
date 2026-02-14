# 🏷️ Cost Allocation Tags

## File Structure

```
lesson-18-billing-and-cost-management/
└── 05-cost-allocation-tags/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Cost allocation tags are labels that you attach to AWS resources to categorize and track costs. They are essential for understanding where your AWS spending is going, enabling chargebacks to departments, and optimizing costs by project or environment. The AWS Certified Cloud Practitioner exam frequently tests knowledge of how tags work for cost management.

## What Are Cost Allocation Tags?

Cost allocation tags are key-value pairs that help you organize and track AWS costs by various dimensions such as project, department, or environment.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        Cost Allocation Tags                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   EC2 Instance                                                           │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │                                                                  │   │
│   │   Instance ID: i-0abc123def456789                               │   │
│   │                                                                  │   │
│   │   Tags:                                                          │   │
│   │   ┌─────────────────────────────────────────────────────────┐   │   │
│   │   │  Key              │  Value                              │   │   │
│   │   ├───────────────────┼─────────────────────────────────────┤   │   │
│   │   │  Environment      │  Production                         │   │   │
│   │   │  Project          │  WebPortal                          │   │   │
│   │   │  Department       │  Engineering                        │   │   │
│   │   │  CostCenter       │  CC-12345                           │   │   │
│   │   │  Owner            │  john.doe@company.com               │   │   │
│   │   └─────────────────────────────────────────────────────────┘   │   │
│   │                                                                  │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Types of Cost Allocation Tags

| Tag Type | Description | Created By |
|----------|-------------|------------|
| **User-Defined Tags** | Tags you create and apply to resources | You |
| **AWS-Generated Tags** | Tags automatically created by AWS | AWS |

### User-Defined Tags

User-defined tags are custom tags that you create to categorize resources.

| Characteristic | Description |
|----------------|-------------|
| **Prefix** | Must NOT start with `aws:` |
| **Case Sensitive** | `Environment` differs from `environment` |
| **Max Tags** | Up to 50 user-defined tags per resource |
| **Key Length** | 1-128 characters |
| **Value Length** | 0-256 characters |

### AWS-Generated Tags

AWS automatically generates certain tags prefixed with `aws:`.

| Tag | Description |
|-----|-------------|
| `aws:createdBy` | Principal that created the resource |
| `aws:cloudformation:stack-name` | CloudFormation stack name |
| `aws:cloudformation:stack-id` | CloudFormation stack ID |
| `aws:elasticmapreduce:*` | EMR-related tags |

## Activating Cost Allocation Tags

Tags must be activated in the Billing console before they appear in cost reports.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Activating Cost Allocation Tags                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Step 1: Apply tags to resources (EC2, S3, RDS, etc.)                  │
│                       │                                                  │
│                       ▼                                                  │
│   Step 2: Navigate to Billing Console > Cost Allocation Tags            │
│                       │                                                  │
│                       ▼                                                  │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │                  Cost Allocation Tags                            │   │
│   ├─────────────────────────────────────────────────────────────────┤   │
│   │                                                                  │   │
│   │   User-Defined Tags    │  Status                                │   │
│   │   ─────────────────────┼─────────────────────────────────       │   │
│   │   Environment          │  [✓] Active                            │   │
│   │   Project              │  [✓] Active                            │   │
│   │   Department           │  [ ] Inactive                          │   │
│   │   CostCenter           │  [✓] Active                            │   │
│   │                                                                  │   │
│   │   AWS-Generated Tags   │  Status                                │   │
│   │   ─────────────────────┼─────────────────────────────────       │   │
│   │   aws:createdBy        │  [✓] Active                            │   │
│   │                                                                  │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                       │                                                  │
│                       ▼                                                  │
│   Step 3: Tags appear in Cost Explorer and CUR after 24 hours           │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Using Tags in Cost Reports

Once activated, tags appear as filterable dimensions in Cost Explorer and Cost and Usage Reports.

### Cost Explorer Filtering by Tags

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Cost Explorer - Tag Filtering                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Filter by Tag: Environment                                             │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  [✓] Production     $4,500                                       │   │
│   │  [✓] Development    $1,200                                       │   │
│   │  [✓] Testing        $800                                         │   │
│   │  [ ] Untagged       $500                                         │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│   Cost ($)                                                               │
│   ▲                                                                      │
│   │   █████████████████████████████████████  Production                 │
│   │   ████████████  Development                                         │
│   │   ████████  Testing                                                  │
│   │   █████  Untagged                                                    │
│   └───────────────────────────────────────────────────────────────────► │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Common Tagging Strategies

### Recommended Tag Keys

| Tag Key | Purpose | Example Values |
|---------|---------|----------------|
| **Environment** | Identify workload environment | Production, Development, Testing |
| **Project** | Track by project/application | WebApp, MobileAPI, DataPlatform |
| **Department** | Departmental chargeback | Engineering, Marketing, Finance |
| **CostCenter** | Financial tracking | CC-12345, CC-67890 |
| **Owner** | Resource accountability | john.doe@company.com |
| **Application** | Application grouping | CRM, ERP, Analytics |

### Tagging Best Practices

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Tagging Best Practices                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ✓ Define a consistent tagging strategy before deploying resources     │
│                                                                          │
│   ✓ Use Tag Policies (AWS Organizations) to enforce tag standards       │
│                                                                          │
│   ✓ Tag resources at creation time (via CloudFormation, CLI, SDK)       │
│                                                                          │
│   ✓ Use automation to ensure all resources are tagged                   │
│                                                                          │
│   ✓ Include cost allocation tags in your Infrastructure as Code         │
│                                                                          │
│   ✓ Regularly audit for untagged resources                              │
│                                                                          │
│   ✗ Don't use different cases (Environment vs environment)              │
│                                                                          │
│   ✗ Don't use spaces in tag keys (use CamelCase or hyphens)            │
│                                                                          │
│   ✗ Don't include sensitive information in tags                         │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Tag Policies (AWS Organizations)

Tag Policies help enforce consistent tagging across your organization.

| Feature | Description |
|---------|-------------|
| **Standardization** | Define allowed tag keys and values |
| **Compliance** | Identify non-compliant resources |
| **Organization-wide** | Apply across all accounts in OUs |
| **Enforcement** | Optional - can prevent or warn |

### Tag Policy Example

```json
{
    "tags": {
        "Environment": {
            "tag_key": {
                "@@assign": "Environment"
            },
            "tag_value": {
                "@@assign": [
                    "Production",
                    "Development",
                    "Testing"
                ]
            },
            "enforced_for": {
                "@@assign": [
                    "ec2:instance",
                    "rds:db"
                ]
            }
        }
    }
}
```

## Chargeback and Showback

Tags enable financial accountability through chargeback and showback models.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Chargeback with Tags                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Monthly AWS Bill: $10,000                                              │
│                                                                          │
│   Filter by Department Tag:                                              │
│                                                                          │
│   ┌─────────────────┬──────────────┬──────────────────────────────┐     │
│   │   Department    │    Cost      │           Chargeback         │     │
│   ├─────────────────┼──────────────┼──────────────────────────────┤     │
│   │   Engineering   │   $4,500     │  ────►  Bill Engineering     │     │
│   │   Marketing     │   $2,200     │  ────►  Bill Marketing       │     │
│   │   Finance       │   $1,800     │  ────►  Bill Finance         │     │
│   │   Data Science  │   $1,000     │  ────►  Bill Data Science    │     │
│   │   Untagged      │   $500       │  ────►  Shared Pool          │     │
│   └─────────────────┴──────────────┴──────────────────────────────┘     │
│                                                                          │
│   Showback: Report costs to departments (no actual billing)             │
│   Chargeback: Actually bill departments for their usage                 │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Finding Untagged Resources

It's important to identify untagged resources to ensure complete cost visibility.

| Method | Description |
|--------|-------------|
| **Cost Explorer** | Filter for "No tag key" to find untagged costs |
| **Resource Groups** | Create groups to find untagged resources |
| **AWS Config** | Rule to check for required tags |
| **Tag Editor** | Search for resources without specific tags |

## 🎯 Exam Tips

- **User-defined tags** must be activated in the Billing console before appearing in reports
- **AWS-generated tags** start with the prefix `aws:` and are created automatically
- Tags appear in cost reports approximately **24 hours after activation**
- Know the difference between **chargeback** (actual billing) and **showback** (reporting only)
- **Tag Policies** in AWS Organizations help enforce consistent tagging
- **Cost allocation tags** are essential for tracking costs by project, department, or environment
- Untagged resources appear as "No tag key" in Cost Explorer

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Cost Allocation Tag | Key-value pair used to categorize and track AWS costs |
| User-Defined Tag | Custom tag created by users (no `aws:` prefix) |
| AWS-Generated Tag | Tag automatically created by AWS (starts with `aws:`) |
| Tag Policy | AWS Organizations policy for enforcing tag standards |
| Chargeback | Billing departments for their actual AWS usage |
| Showback | Reporting costs without actual billing |

## 💡 Key Takeaways

1. Cost allocation tags are key-value pairs that help categorize and track AWS costs
2. Tags must be activated in the Billing console before appearing in cost reports
3. User-defined tags are created by you; AWS-generated tags are created automatically
4. Define a consistent tagging strategy before deploying resources
5. Use Tag Policies in AWS Organizations to enforce tagging standards
6. Tags enable chargeback and showback for departmental cost accountability
7. Regularly audit for untagged resources to ensure complete cost visibility

---

*Previous: [04 - AWS Organizations](../04-aws-organizations/readme.md) | Next: [06 - AWS Cost Anomaly Detection](../06-aws-cost-anomaly-detection/readme.md)*

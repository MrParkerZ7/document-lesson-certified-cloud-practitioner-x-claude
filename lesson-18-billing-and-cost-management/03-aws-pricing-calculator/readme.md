# 🧮 AWS Pricing Calculator

## File Structure

```
lesson-18-billing-and-cost-management/
└── 03-aws-pricing-calculator/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Understanding AWS pricing before deploying resources is crucial for budget planning and cost optimization. AWS provides the AWS Pricing Calculator (and formerly the TCO Calculator) to help estimate costs and compare cloud versus on-premises expenses. The AWS Certified Cloud Practitioner exam frequently tests knowledge of these estimation tools.

## AWS Pricing Calculator Overview

The AWS Pricing Calculator is a free web-based tool that allows you to estimate the cost of AWS services for your specific use case.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      AWS Pricing Calculator                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   URL: https://calculator.aws/                                          │
│                                                                          │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │                                                                  │   │
│   │   1. Add Services    2. Configure     3. View Estimate          │   │
│   │      ┌─────┐           Parameters        ┌──────────┐           │   │
│   │      │ EC2 │           • Instance       │ Monthly  │           │   │
│   │      │ S3  │           • Region         │ $5,432   │           │   │
│   │      │ RDS │           • Usage          │          │           │   │
│   │      │ ... │           • Quantity       │ Export   │           │   │
│   │      └─────┘                            │ & Share  │           │   │
│   │                                         └──────────┘           │   │
│   │                                                                  │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Key Features

| Feature | Description |
|---------|-------------|
| **Service Selection** | Add any AWS service to estimate |
| **Configuration** | Specify region, instance type, usage |
| **Grouping** | Organize services into logical groups |
| **Export** | Download estimates as CSV or PDF |
| **Share** | Generate shareable links |
| **Compare** | Compare different configurations |
| **Free to Use** | No cost to create estimates |

## Using the AWS Pricing Calculator

### Step-by-Step Process

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Creating an Estimate                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Step 1: Create Estimate                                                │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  Click "Create estimate" to start a new calculation              │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                         │                                                │
│                         ▼                                                │
│   Step 2: Add Services                                                   │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  Search for and add services (EC2, S3, RDS, etc.)               │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                         │                                                │
│                         ▼                                                │
│   Step 3: Configure Service                                              │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  • Select region (us-east-1, eu-west-1, etc.)                   │   │
│   │  • Choose configuration (instance type, storage size)           │   │
│   │  • Specify usage (hours/month, GB transferred)                  │   │
│   │  • Select pricing model (On-Demand, Reserved, Spot)             │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                         │                                                │
│                         ▼                                                │
│   Step 4: View and Export                                                │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  Review monthly/yearly estimate, export, or share link          │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Configuration Options by Service

| Service | Key Configuration Parameters |
|---------|------------------------------|
| **EC2** | Instance type, region, OS, usage hours, pricing model |
| **S3** | Storage class, data stored, requests, data transfer |
| **RDS** | DB engine, instance type, storage, Multi-AZ, backups |
| **Lambda** | Requests/month, duration, memory allocated |
| **EBS** | Volume type, size, IOPS, snapshots |
| **Data Transfer** | Out to internet, between regions |

## AWS Pricing Calculator Example

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    Sample Estimate: Web Application                      │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Service             │ Configuration              │ Monthly Cost        │
│   ────────────────────┼────────────────────────────┼─────────────────    │
│   Amazon EC2          │ 2x t3.medium, us-east-1    │ $60.74             │
│                       │ On-Demand, Linux, 730 hrs  │                     │
│   ────────────────────┼────────────────────────────┼─────────────────    │
│   Amazon RDS          │ db.t3.medium, MySQL        │ $49.64             │
│                       │ Multi-AZ, 100GB storage    │                     │
│   ────────────────────┼────────────────────────────┼─────────────────    │
│   Amazon S3           │ 500 GB Standard storage    │ $11.50             │
│                       │ 1M GET, 100K PUT requests  │                     │
│   ────────────────────┼────────────────────────────┼─────────────────    │
│   Elastic Load        │ Application Load Balancer  │ $22.27             │
│   Balancing           │ 500 GB processed           │                     │
│   ────────────────────┼────────────────────────────┼─────────────────    │
│   Data Transfer       │ 100 GB out to internet     │ $9.00              │
│   ════════════════════╧════════════════════════════╧═════════════════    │
│                              TOTAL MONTHLY COST:    │ $153.15            │
│                              TOTAL ANNUAL COST:     │ $1,837.80          │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## TCO Calculator (Legacy)

The Total Cost of Ownership (TCO) Calculator was a tool to compare costs of on-premises versus AWS. While it has been replaced by the Migration Evaluator, understanding TCO concepts is still important.

### TCO Components

```
┌─────────────────────────────────────────────────────────────────────────┐
│                Total Cost of Ownership Comparison                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   On-Premises Costs               │   AWS Cloud Costs                   │
│   ────────────────────────────────│──────────────────────────────────   │
│                                    │                                     │
│   Server Hardware     $100,000    │   EC2 Instances      $30,000/yr     │
│   Storage Hardware    $50,000     │   EBS/S3 Storage     $5,000/yr      │
│   Network Equipment   $25,000     │   Data Transfer      $2,000/yr      │
│   Data Center Space   $40,000/yr  │   (No data center)   $0             │
│   Power & Cooling     $30,000/yr  │   (Included)         $0             │
│   IT Staff (3 FTE)    $300,000/yr │   (Reduced need)     $100,000/yr    │
│   Maintenance         $20,000/yr  │   (Included)         $0             │
│   Licensing           $50,000/yr  │   (Pay-as-you-go)    $10,000/yr     │
│   ────────────────────────────────│──────────────────────────────────   │
│   3-Year TCO:         $1,445,000  │   3-Year TCO:        $441,000       │
│                                    │                                     │
│                    SAVINGS WITH AWS: ~70% ($1,004,000)                  │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### TCO Cost Categories

| Cost Category | On-Premises | AWS Cloud |
|---------------|-------------|-----------|
| **Server Costs** | Hardware purchase | EC2 pricing |
| **Storage Costs** | SAN/NAS purchase | EBS, S3 pricing |
| **Network Costs** | Equipment, bandwidth | Data transfer fees |
| **Facilities** | Data center, power, cooling | Included |
| **IT Labor** | Operations, maintenance | Reduced staff |
| **Downtime** | Outage costs | High availability |

## AWS Migration Evaluator

AWS Migration Evaluator (formerly TSO Logic) is the modern replacement for the TCO Calculator, providing a more comprehensive analysis.

| Feature | Description |
|---------|-------------|
| **Data Collection** | Agentless discovery of on-premises inventory |
| **Rightsizing** | Recommendations for optimal AWS sizing |
| **TCO Analysis** | Detailed cost comparison |
| **Business Case** | Executive-ready reports |
| **Free Service** | No cost for assessment |

## Pricing Calculator Best Practices

### Tips for Accurate Estimates

1. **Choose the correct region** - Prices vary by region
2. **Estimate usage accurately** - Consider peak vs average usage
3. **Include data transfer** - Often overlooked cost component
4. **Consider Reserved Instances** - For predictable workloads
5. **Account for growth** - Build in capacity for scaling

```
┌─────────────────────────────────────────────────────────────────────────┐
│                   Common Estimation Mistakes                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ✗ Forgetting data transfer OUT costs                                  │
│   ✗ Not accounting for cross-AZ traffic                                 │
│   ✗ Ignoring EBS snapshot costs                                         │
│   ✗ Underestimating request counts (API, S3)                           │
│   ✗ Missing support costs                                               │
│   ✗ Not including backup storage                                        │
│                                                                          │
│   ✓ Include ALL services your application will use                      │
│   ✓ Add 10-20% buffer for unexpected costs                             │
│   ✓ Review and update estimates regularly                               │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Comparing Estimation Tools

| Tool | Purpose | Best For |
|------|---------|----------|
| **AWS Pricing Calculator** | Estimate AWS service costs | Planning new deployments |
| **Migration Evaluator** | TCO analysis for migration | Building migration business case |
| **Cost Explorer Forecast** | Predict based on history | Existing AWS usage |

## 🎯 Exam Tips

- **AWS Pricing Calculator** is the primary tool for estimating AWS costs before deployment
- The calculator is **free to use** and accessible without an AWS account
- Know that prices **vary by region** - always specify the correct region
- Remember to include **data transfer costs** in estimates
- The **TCO Calculator** has been replaced by **Migration Evaluator**
- TCO comparisons should include **hidden on-premises costs** (power, cooling, staff)
- **Reserved Instances** and **Savings Plans** can significantly reduce estimated costs

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| AWS Pricing Calculator | Free tool to estimate AWS service costs |
| TCO (Total Cost of Ownership) | Complete cost including direct and indirect expenses |
| Migration Evaluator | AWS service for TCO analysis during migration |
| Data Transfer | Costs for moving data in and out of AWS |
| Rightsizing | Selecting the most cost-effective resource size |
| Break-even Analysis | Point where cloud costs equal on-premises costs |

## 💡 Key Takeaways

1. AWS Pricing Calculator helps estimate costs before deploying resources
2. The calculator is free and accessible without an AWS account
3. Prices vary by region - always select the correct region for accurate estimates
4. Include data transfer, storage, and all associated services in estimates
5. TCO analysis should include hidden on-premises costs like power and facilities
6. Migration Evaluator provides comprehensive migration cost analysis
7. Reserved Instances and Savings Plans can significantly reduce costs in estimates

---

*Previous: [02 - Cost Management Tools](../02-cost-management-tools/readme.md) | Next: [04 - AWS Organizations](../04-aws-organizations/readme.md)*

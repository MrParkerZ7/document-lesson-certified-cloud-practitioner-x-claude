# 🆓 AWS Free Tier

## File Structure

```
lesson-17-aws-pricing-models/
└── 05-free-tier/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The AWS Free Tier enables you to explore and try AWS services free of charge up to specified limits. Understanding the different types of free tier offerings helps you learn AWS without unexpected costs while building proof-of-concept applications.

## Three Types of Free Tier Offers

```
+------------------------------------------------------------------+
|                    AWS FREE TIER TYPES                            |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |  ALWAYS FREE     |  |  12-MONTH FREE   |  |  FREE TRIALS     | |
|   |                  |  |                  |  |                  | |
|   |  No expiration   |  |  Expires after   |  |  Short-term      | |
|   |  Available to    |  |  12 months from  |  |  Usually 30-90   | |
|   |  all accounts    |  |  account signup  |  |  days            | |
|   |                  |  |                  |  |                  | |
|   |  Examples:       |  |  Examples:       |  |  Examples:       | |
|   |  - Lambda        |  |  - EC2 t2.micro  |  |  - SageMaker     | |
|   |  - DynamoDB      |  |  - S3 5GB        |  |  - Redshift      | |
|   |  - CloudWatch    |  |  - RDS           |  |  - Inspector     | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Free Tier Types Comparison

| Type | Duration | Best For | Limit Reset |
|------|----------|----------|-------------|
| Always Free | Forever | Production workloads (within limits) | Monthly |
| 12-Month Free | 12 months from signup | Learning and experimentation | Monthly |
| Free Trials | Varies (30-90 days) | Evaluating specific services | One-time |

## Always Free Services

These services are always free within specified limits, regardless of account age.

| Service | Free Tier Limit | Reset Period |
|---------|-----------------|--------------|
| AWS Lambda | 1M requests/month, 400,000 GB-seconds | Monthly |
| Amazon DynamoDB | 25 GB storage, 25 RCU, 25 WCU | Monthly |
| Amazon CloudWatch | 10 custom metrics, 10 alarms | Monthly |
| Amazon SNS | 1M publishes | Monthly |
| Amazon SQS | 1M requests | Monthly |
| AWS CodeBuild | 100 build minutes/month | Monthly |
| AWS CodePipeline | 1 active pipeline | Monthly |
| Amazon Cognito | 50,000 MAUs | Monthly |
| AWS Glue | 1M objects stored in Data Catalog | Monthly |

## 12-Month Free Tier Services

Available for 12 months from AWS account creation.

```
+------------------------------------------------------------------+
|                   12-MONTH FREE TIER                              |
+------------------------------------------------------------------+
|                                                                   |
|   Account Created: January 1, 2024                                |
|   Free Tier Expires: December 31, 2024                            |
|                                                                   |
|   +------------------+------------------------------------------+ |
|   | Service          | 12-Month Free Tier Limit                 | |
|   +------------------+------------------------------------------+ |
|   | EC2              | 750 hours/month of t2.micro or t3.micro  | |
|   | S3               | 5 GB standard storage                    | |
|   | RDS              | 750 hours/month of db.t2.micro           | |
|   | EBS              | 30 GB of General Purpose (SSD)           | |
|   | CloudFront       | 50 GB data transfer out                  | |
|   | Elastic Load     | 750 hours/month                          | |
|   | Balancing        |                                          | |
|   | ElastiCache      | 750 hours/month of cache.t2.micro        | |
|   | EFS              | 5 GB of storage                          | |
|   +------------------+------------------------------------------+ |
|                                                                   |
|   WARNING: After 12 months, standard rates apply!                 |
|                                                                   |
+------------------------------------------------------------------+
```

## Popular 12-Month Free Services

| Service | Free Tier Allowance | Notes |
|---------|---------------------|-------|
| Amazon EC2 | 750 hours/month t2.micro or t3.micro | Linux and Windows |
| Amazon S3 | 5 GB storage, 20,000 GET, 2,000 PUT | Standard storage only |
| Amazon RDS | 750 hours/month db.t2.micro | Single-AZ only |
| Amazon EBS | 30 GB storage | gp2 or gp3 |
| Amazon CloudFront | 50 GB data out, 2M requests | All edge locations |
| Amazon ELB | 750 hours/month | Classic or Application |
| Amazon API Gateway | 1M API calls/month | REST APIs |
| Amazon SNS | 1M publishes, 100K HTTP deliveries | - |

## Free Trials

Short-term trials for specific services to evaluate before committing.

| Service | Trial Duration | Trial Limit |
|---------|---------------|-------------|
| Amazon SageMaker | 2 months | 250 hours/month |
| Amazon Redshift | 2 months | 750 hours/month |
| Amazon Inspector | 15 days | - |
| Amazon QuickSight | 30 days | 4 users |
| Amazon Macie | 30 days | 1 GB/month |
| Amazon Detective | 30 days | - |
| AWS Database Migration Service | 6 months | 750 hours dms.t2.micro |

## EC2 Free Tier Details

```
+------------------------------------------------------------------+
|                    EC2 FREE TIER BREAKDOWN                        |
+------------------------------------------------------------------+
|                                                                   |
|   Total Monthly Hours: 750                                        |
|                                                                   |
|   +-----------------------+-----------------------------------+   |
|   | Instance Type         | t2.micro or t3.micro              |   |
|   | vCPU                  | 1                                 |   |
|   | Memory                | 1 GB                              |   |
|   | Operating Systems     | Linux and Windows                 |   |
|   | Duration              | 12 months from signup             |   |
|   +-----------------------+-----------------------------------+   |
|                                                                   |
|   Example Usage:                                                  |
|   - 1 instance running 24/7 = ~720 hours (within limit)           |
|   - 2 instances running 12 hours/day = 720 hours (within limit)   |
|   - 3 instances running 24/7 = 2,160 hours (EXCEEDS FREE TIER!)   |
|                                                                   |
+------------------------------------------------------------------+
```

## Common Free Tier Mistakes

```
+------------------------------------------------------------------+
|                  COMMON FREE TIER MISTAKES                        |
+------------------------------------------------------------------+
|                                                                   |
|   MISTAKE 1: Running multiple instances                           |
|   +-----------------------------------------------------------+   |
|   | 2 x t2.micro 24/7 = 1,440 hours = 690 hours CHARGED       |   |
|   +-----------------------------------------------------------+   |
|                                                                   |
|   MISTAKE 2: Using wrong instance type                            |
|   +-----------------------------------------------------------+   |
|   | t2.small instead of t2.micro = ALL hours CHARGED          |   |
|   +-----------------------------------------------------------+   |
|                                                                   |
|   MISTAKE 3: Running in multiple regions                          |
|   +-----------------------------------------------------------+   |
|   | Free tier is per service, not per region                  |   |
|   | 750 hours TOTAL across ALL regions                        |   |
|   +-----------------------------------------------------------+   |
|                                                                   |
|   MISTAKE 4: Forgetting to stop resources                         |
|   +-----------------------------------------------------------+   |
|   | EBS volumes, Elastic IPs, etc. still incur charges        |   |
|   +-----------------------------------------------------------+   |
|                                                                   |
|   MISTAKE 5: Expired free tier                                    |
|   +-----------------------------------------------------------+   |
|   | 12-month services charge after first year                 |   |
|   +-----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Monitoring Free Tier Usage

| Tool | Description |
|------|-------------|
| AWS Billing Dashboard | View current charges and free tier usage |
| AWS Budgets | Set alerts for spending thresholds |
| Free Tier Usage Alerts | Automatic email when approaching limits |
| Cost Explorer | Analyze spending patterns |

## Setting Up Free Tier Alerts

```
+------------------------------------------------------------------+
|               FREE TIER USAGE ALERTS                              |
+------------------------------------------------------------------+
|                                                                   |
|   1. AWS Billing Dashboard                                        |
|      +---------------------------------------------------+        |
|      | View free tier usage percentage per service       |        |
|      +---------------------------------------------------+        |
|                                                                   |
|   2. AWS Budgets (recommended)                                    |
|      +---------------------------------------------------+        |
|      | Create a Zero Spend Budget                        |        |
|      | Alert when costs exceed $0                        |        |
|      +---------------------------------------------------+        |
|                                                                   |
|   3. Billing Preferences                                          |
|      +---------------------------------------------------+        |
|      | Enable "Free Tier Usage Alerts"                   |        |
|      | Get email at 85% of free tier limit               |        |
|      +---------------------------------------------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## Free Tier Best Practices

| Practice | Description |
|----------|-------------|
| Set billing alerts | Create budgets to avoid surprise charges |
| Use correct instance types | Always verify t2.micro or t3.micro |
| Monitor usage regularly | Check billing dashboard weekly |
| Terminate unused resources | Clean up after experiments |
| Track 12-month expiration | Set calendar reminder |
| Use single region | Easier to track free tier limits |
| Review EBS volumes | Delete unattached volumes |
| Release Elastic IPs | Unused Elastic IPs incur charges |

## Services NOT in Free Tier

Some commonly used services are not included in the free tier:

| Service | Why Not Free |
|---------|--------------|
| NAT Gateway | Per hour + data processing charges |
| Elastic IP (unattached) | Charged when not associated with running instance |
| EBS Snapshots | Charged for storage |
| Data Transfer OUT | Charged per GB (beyond minimal amounts) |
| Route 53 | Charged per hosted zone and queries |
| Secrets Manager | Charged per secret per month |

## 🎯 Exam Tips

- **Three types**: Always Free, 12-Month Free, and Free Trials
- **Always Free** services never expire (Lambda, DynamoDB, CloudWatch)
- **12-Month Free** starts from account creation date
- **t2.micro/t3.micro** EC2 = 750 hours/month for 12 months
- **S3** = 5 GB standard storage for 12 months
- Free tier limits are **per service**, not per region
- **AWS Budgets** can alert you before exceeding free tier
- Running instances across regions still counts against the SAME free tier limit

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Always Free | AWS services free forever within specified limits |
| 12-Month Free Tier | Services free for 12 months from account signup |
| Free Trial | Short-term trial period for specific services |
| t2.micro | Free tier eligible EC2 instance type (1 vCPU, 1 GB RAM) |
| AWS Budgets | Service to set cost and usage alerts |
| Billing Dashboard | Console page showing charges and free tier usage |
| Free Tier Usage Alert | Automatic notification when approaching limits |

## 💡 Key Takeaways

1. AWS Free Tier has three types: Always Free, 12-Month Free, and Free Trials
2. Always Free services (Lambda, DynamoDB) never expire within limits
3. 12-Month Free Tier expires exactly 12 months from account creation
4. EC2 t2.micro/t3.micro: 750 hours/month for 12 months (total, not per instance)
5. Free tier limits are per service across ALL regions combined
6. Set up AWS Budgets and billing alerts to avoid surprise charges
7. Common mistakes include wrong instance types and forgetting to stop resources
8. Always clean up resources after experiments to avoid charges

---

*Previous: [04 - Data Transfer Costs](../04-data-transfer-costs/readme.md)*

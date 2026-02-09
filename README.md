# AWS Certified Cloud Practitioner (CLF-C02) - Complete Study Guide

A comprehensive lesson plan for preparing for the AWS Certified Cloud Practitioner certification exam.

## Exam Overview

| Attribute | Details |
|-----------|---------|
| Exam Code | CLF-C02 |
| Questions | 65 (multiple choice / multiple response) |
| Duration | 90 minutes |
| Passing Score | 700/1000 |

---

## Domain Breakdown

| Domain | Weight | Lessons |
|--------|--------|---------|
| Domain 1: Cloud Concepts | 24% | Lessons 1-4 |
| Domain 2: Security and Compliance | 30% | Lessons 5-8 |
| Domain 3: Cloud Technology and Services | 34% | Lessons 9-16 |
| Domain 4: Billing, Pricing, and Support | 12% | Lessons 17-19 |

---

## Domain 1: Cloud Concepts (24%)

### Lesson 1: Benefits of the AWS Cloud
- 1.1 Value Proposition of AWS Cloud
- 1.2 Benefits of Global Infrastructure
  - Speed of deployment
  - Global reach
- 1.3 High Availability
- 1.4 Elasticity and Scalability
- 1.5 Agility and Flexibility

### Lesson 2: AWS Well-Architected Framework
- 2.1 Introduction to Well-Architected Framework
- 2.2 Operational Excellence Pillar
- 2.3 Security Pillar
- 2.4 Reliability Pillar
- 2.5 Performance Efficiency Pillar
- 2.6 Cost Optimization Pillar
- 2.7 Sustainability Pillar
- 2.8 Differences and Trade-offs Between Pillars

### Lesson 3: Cloud Migration Strategies
- 3.1 AWS Cloud Adoption Framework (AWS CAF)
  - Business perspective
  - People perspective
  - Governance perspective
  - Platform perspective
  - Security perspective
  - Operations perspective
- 3.2 Benefits of Migration
  - Reduced business risk
  - Improved ESG performance
  - Increased revenue
  - Increased operational efficiency
- 3.3 Migration Strategies (The 7 R's)
  - Rehost (Lift and Shift)
  - Replatform
  - Refactor/Re-architect
  - Repurchase
  - Retire
  - Retain
  - Relocate
- 3.4 Migration Tools
  - AWS Database Migration Service (DMS)
  - AWS Snow Family (Snowball, Snowcone, Snowmobile)
  - AWS Application Migration Service

### Lesson 4: Cloud Economics
- 4.1 Fixed Costs vs. Variable Costs
- 4.2 On-Premises vs. Cloud Cost Comparison
- 4.3 Capital Expenditure (CapEx) vs. Operational Expenditure (OpEx)
- 4.4 Licensing Strategies
  - Bring Your Own License (BYOL)
  - License-included models
- 4.5 Right-sizing Resources
- 4.6 Benefits of Automation
- 4.7 Managed Services Value
- 4.8 Economies of Scale

---

## Domain 2: Security and Compliance (30%)

### Lesson 5: AWS Shared Responsibility Model
- 5.1 Understanding the Shared Responsibility Model
- 5.2 AWS Responsibilities ("Security OF the Cloud")
  - Physical security
  - Infrastructure
  - Hardware/Software
- 5.3 Customer Responsibilities ("Security IN the Cloud")
  - Data encryption
  - Identity management
  - Application security
  - Operating system patches
- 5.4 Shared Responsibilities
  - Patch management
  - Configuration management
  - Awareness and training
- 5.5 Responsibility Shifts by Service Type
  - IaaS (EC2)
  - PaaS (RDS, Elastic Beanstalk)
  - SaaS (Lambda)

### Lesson 6: Security, Governance, and Compliance
- 6.1 AWS Compliance Programs
  - SOC reports
  - PCI DSS
  - HIPAA
  - GDPR
  - FedRAMP
- 6.2 AWS Artifact
- 6.3 Geographic and Industry Compliance Requirements
- 6.4 Encryption Options
  - Encryption at rest
  - Encryption in transit
  - AWS Key Management Service (KMS)
  - AWS CloudHSM
- 6.5 Security Services
  - Amazon Inspector
  - AWS Security Hub
  - Amazon GuardDuty
  - AWS Shield (Standard and Advanced)
  - AWS WAF
  - AWS Firewall Manager
- 6.6 Governance and Auditing Services
  - Amazon CloudWatch
  - AWS CloudTrail
  - AWS Config
  - AWS Audit Manager

### Lesson 7: AWS Access Management
- 7.1 AWS Identity and Access Management (IAM)
  - Users
  - Groups
  - Roles
  - Policies (managed vs. custom)
- 7.2 Root User Account
  - Protection strategies
  - Tasks only root can perform
- 7.3 Principle of Least Privilege
- 7.4 Authentication Methods
  - Multi-Factor Authentication (MFA)
  - Access keys
  - Password policies
- 7.5 AWS IAM Identity Center (SSO)
- 7.6 Federated Identity Management
- 7.7 Cross-Account Access
- 7.8 Credential Management
  - AWS Secrets Manager
  - AWS Systems Manager Parameter Store

### Lesson 8: Security Resources and Components
- 8.1 AWS Security Services Overview
  - AWS WAF
  - AWS Shield
  - AWS Firewall Manager
  - Amazon GuardDuty
- 8.2 AWS Marketplace Security Products
- 8.3 AWS Security Information Resources
  - AWS Knowledge Center
  - AWS Security Center
  - AWS Security Blog
- 8.4 AWS Trusted Advisor Security Checks
- 8.5 AWS Trust and Safety Team

---

## Domain 3: Cloud Technology and Services (34%)

### Lesson 9: Deploying and Operating in AWS
- 9.1 Ways to Access AWS Services
  - AWS Management Console
  - AWS Command Line Interface (CLI)
  - AWS Software Development Kits (SDKs)
  - APIs
- 9.2 Infrastructure as Code
  - AWS CloudFormation
  - AWS CDK
- 9.3 Cloud Deployment Models
  - Public cloud
  - Private cloud
  - Hybrid cloud
  - Multi-cloud
- 9.4 One-Time Operations vs. Repeatable Processes

### Lesson 10: AWS Global Infrastructure
- 10.1 AWS Regions
  - Region selection criteria
  - Data sovereignty
- 10.2 Availability Zones (AZs)
  - High availability design
  - Fault isolation
- 10.3 Edge Locations and Points of Presence
- 10.4 Amazon CloudFront (CDN)
- 10.5 AWS Local Zones
- 10.6 AWS Wavelength
- 10.7 AWS Outposts
- 10.8 Multi-Region Strategies
  - Disaster recovery
  - Business continuity
  - Low latency

### Lesson 11: AWS Compute Services
- 11.1 Amazon EC2
  - Instance types (General, Compute, Memory, Storage, Accelerated)
  - Instance families
  - Amazon Machine Images (AMIs)
- 11.2 Container Services
  - Amazon Elastic Container Service (ECS)
  - Amazon Elastic Kubernetes Service (EKS)
  - AWS Fargate
  - Amazon ECR
- 11.3 Serverless Computing
  - AWS Lambda
  - Use cases and event-driven architecture
- 11.4 Other Compute Services
  - AWS Elastic Beanstalk
  - AWS Batch
  - Amazon Lightsail
- 11.5 Auto Scaling
  - EC2 Auto Scaling
  - Application Auto Scaling
- 11.6 Elastic Load Balancing
  - Application Load Balancer (ALB)
  - Network Load Balancer (NLB)
  - Gateway Load Balancer (GWLB)

### Lesson 12: AWS Database Services
- 12.1 Database Types Overview
- 12.2 Relational Databases
  - Amazon RDS (MySQL, PostgreSQL, Oracle, SQL Server, MariaDB)
  - Amazon Aurora
- 12.3 NoSQL Databases
  - Amazon DynamoDB
  - Amazon DocumentDB
- 12.4 In-Memory Databases
  - Amazon ElastiCache (Redis, Memcached)
  - Amazon MemoryDB for Redis
- 12.5 Other Database Services
  - Amazon Neptune (Graph)
  - Amazon Timestream (Time-series)
  - Amazon QLDB (Ledger)
  - Amazon Keyspaces (Cassandra)
- 12.6 Database Migration
  - AWS Database Migration Service (DMS)
  - AWS Schema Conversion Tool (SCT)
- 12.7 EC2-Hosted vs. AWS Managed Databases

### Lesson 13: AWS Networking Services
- 13.1 Amazon Virtual Private Cloud (VPC)
  - Subnets (public and private)
  - Route tables
  - Internet Gateway
  - NAT Gateway
- 13.2 VPC Security
  - Security Groups
  - Network Access Control Lists (NACLs)
- 13.3 Amazon Route 53
  - DNS service
  - Routing policies
  - Health checks
- 13.4 Connectivity Options
  - AWS VPN
  - AWS Direct Connect
  - VPC Peering
  - AWS Transit Gateway
- 13.5 Content Delivery
  - Amazon CloudFront
  - AWS Global Accelerator

### Lesson 14: AWS Storage Services
- 14.1 Object Storage
  - Amazon S3
  - S3 Storage Classes (Standard, IA, One Zone-IA, Glacier, Glacier Deep Archive, Intelligent-Tiering)
  - S3 Features (versioning, lifecycle policies, replication)
- 14.2 Block Storage
  - Amazon Elastic Block Store (EBS)
  - EBS volume types
  - Instance Store
- 14.3 File Storage
  - Amazon Elastic File System (EFS)
  - Amazon FSx (Windows File Server, Lustre, NetApp ONTAP, OpenZFS)
- 14.4 Hybrid and Edge Storage
  - AWS Storage Gateway
  - AWS Snow Family
- 14.5 Backup and Recovery
  - AWS Backup
  - Lifecycle policies

### Lesson 15: AWS AI/ML and Analytics Services
- 15.1 AI/ML Services
  - Amazon SageMaker AI
  - Amazon Rekognition
  - Amazon Lex
  - Amazon Polly
  - Amazon Transcribe
  - Amazon Translate
  - Amazon Comprehend
  - Amazon Kendra
  - Amazon Textract
- 15.2 Analytics Services
  - Amazon Athena
  - Amazon Kinesis
  - AWS Glue
  - Amazon QuickSight
  - Amazon EMR
  - Amazon Redshift
  - AWS Data Exchange

### Lesson 16: Other AWS Services
- 16.1 Application Integration
  - Amazon EventBridge
  - Amazon Simple Notification Service (SNS)
  - Amazon Simple Queue Service (SQS)
  - AWS Step Functions
- 16.2 Business Applications
  - Amazon Connect
  - Amazon Simple Email Service (SES)
- 16.3 Developer Tools
  - AWS CodeCommit
  - AWS CodeBuild
  - AWS CodeDeploy
  - AWS CodePipeline
  - AWS X-Ray
- 16.4 End-User Computing
  - Amazon WorkSpaces
  - Amazon AppStream 2.0
  - Amazon WorkSpaces Secure Browser
- 16.5 Frontend Web and Mobile
  - AWS Amplify
  - AWS AppSync
- 16.6 IoT Services
  - AWS IoT Core
  - AWS IoT Greengrass

---

## Domain 4: Billing, Pricing, and Support (12%)

### Lesson 17: AWS Pricing Models
- 17.1 Compute Purchasing Options
  - On-Demand Instances
  - Reserved Instances (Standard, Convertible, Scheduled)
  - Spot Instances
  - AWS Savings Plans (Compute, EC2, SageMaker)
  - Dedicated Hosts
  - Dedicated Instances
  - Capacity Reservations
- 17.2 Reserved Instance Flexibility
  - AWS Organizations behavior
  - Size flexibility
- 17.3 Storage Pricing
  - S3 pricing tiers
  - EBS pricing
  - Data transfer costs
- 17.4 Data Transfer Costs
  - Inbound vs. outbound
  - Cross-region transfer
  - Same-region transfer
- 17.5 Free Tier
  - Always free
  - 12 months free
  - Trials

### Lesson 18: Billing and Cost Management
- 18.1 AWS Billing Dashboard
- 18.2 Cost Management Tools
  - AWS Cost Explorer
  - AWS Budgets
  - AWS Cost and Usage Report
- 18.3 AWS Pricing Calculator
- 18.4 AWS Organizations
  - Consolidated billing
  - Service Control Policies (SCPs)
  - Organizational Units (OUs)
- 18.5 Cost Allocation Tags
  - AWS-generated tags
  - User-defined tags
- 18.6 AWS Cost Anomaly Detection

### Lesson 19: AWS Support and Resources
- 19.1 AWS Support Plans
  - Basic Support
  - Developer Support
  - Business Support
  - Enterprise On-Ramp Support
  - Enterprise Support
- 19.2 AWS Support Center
- 19.3 AWS Trusted Advisor
  - Cost optimization
  - Performance
  - Security
  - Fault tolerance
  - Service limits
- 19.4 AWS Health Dashboard
  - Personal Health Dashboard
  - Service Health Dashboard
  - AWS Health API
- 19.5 Technical Resources
  - AWS Documentation
  - AWS Whitepapers
  - AWS Blogs
  - AWS Prescriptive Guidance
  - AWS Knowledge Center
  - AWS re:Post
- 19.6 AWS Partner Network (APN)
  - AWS Partners
  - AWS Marketplace
  - AWS Professional Services
  - AWS Solutions Architects
- 19.7 AWS Trust and Safety Team

---

## Lesson Progress Tracker

| Lesson | Topic | Status |
|--------|-------|--------|
| 1 | Benefits of the AWS Cloud | [ ] |
| 2 | AWS Well-Architected Framework | [ ] |
| 3 | Cloud Migration Strategies | [ ] |
| 4 | Cloud Economics | [ ] |
| 5 | AWS Shared Responsibility Model | [ ] |
| 6 | Security, Governance, and Compliance | [ ] |
| 7 | AWS Access Management | [ ] |
| 8 | Security Resources and Components | [ ] |
| 9 | Deploying and Operating in AWS | [ ] |
| 10 | AWS Global Infrastructure | [ ] |
| 11 | AWS Compute Services | [ ] |
| 12 | AWS Database Services | [ ] |
| 13 | AWS Networking Services | [ ] |
| 14 | AWS Storage Services | [ ] |
| 15 | AWS AI/ML and Analytics Services | [ ] |
| 16 | Other AWS Services | [ ] |
| 17 | AWS Pricing Models | [ ] |
| 18 | Billing and Cost Management | [ ] |
| 19 | AWS Support and Resources | [ ] |

---

## Additional Resources

- [AWS Certified Cloud Practitioner Exam Guide](https://docs.aws.amazon.com/aws-certification/latest/examguides/cloud-practitioner-02.html)
- [AWS Free Tier](https://aws.amazon.com/free/)
- [AWS Skill Builder](https://skillbuilder.aws/)
- [AWS Whitepapers](https://aws.amazon.com/whitepapers/)

---

*This study guide is structured based on the official AWS CLF-C02 exam domains and task statements.*

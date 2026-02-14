# 🏪 AWS Marketplace Security Products

## File Structure

```
lesson-08-security-resources-and-components/
└── 02-aws-marketplace-security-products/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Marketplace is a digital catalog that offers thousands of software listings from independent software vendors. It includes a wide range of security products that can enhance your AWS security posture beyond native AWS services.

## What is AWS Marketplace?

AWS Marketplace allows you to find, test, buy, and deploy software that runs on AWS.

```
+------------------------------------------------------------------+
|                     AWS MARKETPLACE                               |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |    DISCOVER      |  |      TRY        |  |      BUY         | |
|   +------------------+  +------------------+  +------------------+ |
|   | Browse catalog   |  | Free trials     |  | Pay-as-you-go    | |
|   | Search products  |  | Test drive      |  | Annual contracts | |
|   | Read reviews     |  | Evaluate        |  | Private offers   | |
|   +------------------+  +------------------+  +------------------+ |
|                              |                                    |
|                              v                                    |
|                    +------------------+                           |
|                    |     DEPLOY       |                           |
|                    +------------------+                           |
|                    | Launch in AWS    |                           |
|                    | Consolidated bill|                           |
|                    +------------------+                           |
|                                                                   |
+------------------------------------------------------------------+
```

## Security Product Categories

| Category | Examples | Use Cases |
|----------|----------|-----------|
| Firewalls | Palo Alto, Fortinet, Check Point | Network security |
| Endpoint Protection | CrowdStrike, Trend Micro | EC2 protection |
| SIEM | Splunk, Sumo Logic | Log analysis |
| Vulnerability Management | Qualys, Rapid7, Tenable | Scanning |
| Identity | Okta, Ping Identity | SSO, MFA |
| Data Security | Varonis, Imperva | Data protection |
| Compliance | Qualys, Coalfire | Audit support |

## Benefits of AWS Marketplace Security Products

| Benefit | Description |
|---------|-------------|
| Quick deployment | Launch in minutes |
| Pay-as-you-go | No upfront costs |
| Consolidated billing | Single AWS bill |
| Pre-configured | Optimized for AWS |
| Scalable | Grows with your needs |
| Vetted vendors | AWS reviewed |

## Deployment Models

```
+------------------------------------------------------------------+
|              MARKETPLACE DEPLOYMENT OPTIONS                       |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------------+    +------------------------+        |
|   |    AMI-Based Products  |    |    SaaS Products       |        |
|   +------------------------+    +------------------------+        |
|   | • Deploy to EC2        |    | • No infrastructure   |        |
|   | • Self-managed         |    | • Vendor-managed      |        |
|   | • Full control         |    | • Quick setup         |        |
|   | • Pay hourly/annual    |    | • Usage-based billing |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
|   +------------------------+    +------------------------+        |
|   |   Container Products   |    |   Data Products        |        |
|   +------------------------+    +------------------------+        |
|   | • ECS/EKS deployment   |    | • Threat intel feeds  |        |
|   | • Kubernetes native    |    | • IP reputation lists |        |
|   | • Portable             |    | • Subscribe and use   |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## Popular Security Vendors on Marketplace

| Vendor | Product Category | AWS Integration |
|--------|-----------------|-----------------|
| Palo Alto Networks | Firewall, VM-Series | VPC integration |
| Fortinet | FortiGate | Network security |
| CrowdStrike | Falcon | Endpoint detection |
| Splunk | SIEM | CloudWatch, S3 logs |
| Trend Micro | Cloud One | Workload security |
| Qualys | Vulnerability Scanner | EC2 scanning |
| Tenable | Nessus | Vulnerability assessment |
| Okta | Identity | IAM integration |

## Purchasing Options

| Option | Description | Best For |
|--------|-------------|----------|
| Free trial | Try before you buy | Evaluation |
| Hourly | Pay by the hour | Variable workloads |
| Monthly | Pay monthly | Predictable short-term |
| Annual | 1-year commitment | Cost savings |
| Multi-year | 2-3 year commitment | Maximum savings |
| BYOL | Bring Your Own License | Existing licenses |

## Private Marketplace

Organizations can create a curated catalog of approved products.

| Feature | Description |
|---------|-------------|
| Governance | Control which products can be purchased |
| Compliance | Ensure only approved software |
| Standardization | Consistent security tools |
| Central management | Admins control catalog |

## Integration with AWS Services

```
+------------------------------------------------------------------+
|           MARKETPLACE INTEGRATION WITH AWS                        |
+------------------------------------------------------------------+
|                                                                   |
|   Marketplace Product                 AWS Services                |
|   +-----------------+                +-------------------+        |
|   |   Security      |  <-----------> |   CloudWatch      |        |
|   |   Product       |                |   (Monitoring)    |        |
|   +-----------------+                +-------------------+        |
|          |                                    |                   |
|          v                                    v                   |
|   +-----------------+                +-------------------+        |
|   |   VPC           |                |   S3              |        |
|   |   Integration   |                |   (Log Storage)   |        |
|   +-----------------+                +-------------------+        |
|          |                                    |                   |
|          v                                    v                   |
|   +-----------------+                +-------------------+        |
|   |   EC2/ECS       |                |   Security Hub    |        |
|   |   Deployment    |                |   (Aggregation)   |        |
|   +-----------------+                +-------------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Marketplace for Security: Best Practices

1. **Evaluate free trials** before purchasing
2. **Check AWS reviews** and ratings
3. **Verify AWS competencies** of vendors
4. **Use Private Marketplace** for governance
5. **Consider consolidated billing** benefits
6. **Review licensing models** for cost optimization

## Finding Security Products

| Method | Steps |
|--------|-------|
| Browse by category | AWS Marketplace > Security |
| Search | Use keywords like "firewall", "SIEM" |
| Filter by pricing | Hourly, annual, free tier |
| AWS Partner Network | Filter by APN status |

## 🎯 Exam Tips

- **AWS Marketplace** = third-party software catalog
- Products are **pre-configured** for AWS
- Supports **AMI**, **SaaS**, and **container** deployments
- **Consolidated billing** through AWS bill
- **Private Marketplace** for organizational control
- Many products offer **free trials**
- Know common security product categories

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| AWS Marketplace | Digital catalog for third-party software |
| AMI | Amazon Machine Image for EC2 deployment |
| SaaS | Software as a Service (vendor managed) |
| BYOL | Bring Your Own License |
| Private Marketplace | Curated catalog for organizations |
| ISV | Independent Software Vendor |

## 💡 Key Takeaways

1. AWS Marketplace offers third-party security products optimized for AWS
2. Products can be deployed as AMIs, SaaS, or containers
3. Consolidated billing simplifies procurement
4. Private Marketplace enables governance and compliance
5. Many products integrate natively with AWS services
6. Free trials allow evaluation before purchase
7. Marketplace complements native AWS security services

---

*Next: [03 - AWS Security Information Resources](../03-aws-security-information-resources/readme.md)*

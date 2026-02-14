# 📄 AWS Artifact

## File Structure

```
lesson-06-security-governance-and-compliance/
└── 02-aws-artifact/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Artifact is a self-service portal that provides on-demand access to AWS security and compliance reports and select online agreements. It is a critical service for organizations that need to demonstrate compliance to auditors, regulators, or internal stakeholders.

## What is AWS Artifact?

AWS Artifact is a no-cost, self-service portal for on-demand access to AWS's compliance reports and agreements. It provides access to AWS security and compliance documents, such as AWS ISO certifications, Payment Card Industry (PCI), and Service Organization Control (SOC) reports.

## Key Features

### Artifact Reports

Access to third-party audit reports that validate AWS compliance:

| Report Type | Description | Use Case |
|-------------|-------------|----------|
| SOC 1 | Financial reporting controls | Financial audits |
| SOC 2 | Security, availability, confidentiality | Security assessments |
| SOC 3 | Public-facing summary report | General assurance |
| ISO 27001 | Information security management | Security certification |
| PCI DSS | Payment card security | Payment processing |

### Artifact Agreements

Manage legal agreements between you and AWS:

| Agreement | Purpose | Required For |
|-----------|---------|--------------|
| BAA | Business Associate Agreement | HIPAA workloads |
| NDA | Non-Disclosure Agreement | Confidential information |
| Data Processing Addendum | GDPR compliance | EU data processing |

## How AWS Artifact Works

```
+------------------------------------------------------------------+
|                        AWS ARTIFACT PORTAL                        |
+------------------------------------------------------------------+
|                                                                   |
|    +------------------+          +------------------+             |
|    |   Your Account   |   --->   |   AWS Artifact   |             |
|    +------------------+          +------------------+             |
|                                          |                        |
|                    +---------------------+---------------------+  |
|                    |                     |                     |  |
|                    v                     v                     v  |
|           +---------------+     +---------------+     +----------+|
|           |   Artifact    |     |   Artifact    |     | Account  ||
|           |   Reports     |     |   Agreements  |     | Settings ||
|           +---------------+     +---------------+     +----------+|
|           | • SOC Reports |     | • BAA         |     | • Access ||
|           | • ISO Certs   |     | • NDA         |     | • Users  ||
|           | • PCI Reports |     | • DPA         |     | • Audit  ||
|           +---------------+     +---------------+     +----------+|
|                                                                   |
+------------------------------------------------------------------+
```

## Accessing AWS Artifact

### Through AWS Console

1. Sign in to the AWS Management Console
2. Navigate to AWS Artifact
3. Choose Reports or Agreements
4. Download or accept as needed

### Access Requirements

| Requirement | Description |
|-------------|-------------|
| IAM Permissions | artifact:GetReport, artifact:AcceptAgreement |
| Account Type | AWS account holder |
| Region | Available globally |
| Cost | Free to access |

## AWS Artifact Reports

### Available Report Categories

| Category | Examples |
|----------|----------|
| Global Certifications | ISO 27001, ISO 27017, ISO 27018 |
| Government | FedRAMP, DoD SRG, ITAR |
| Industry | PCI DSS, HIPAA, SOC |
| Regional | GDPR, C5, MTCS, IRAP |

### Report Download Process

```
+------------+     +------------+     +------------+     +------------+
|   Login    | --> |   Select   | --> |   Accept   | --> |  Download  |
|  to AWS    |     |   Report   |     |    NDA     |     |   Report   |
+------------+     +------------+     +------------+     +------------+
```

## AWS Artifact Agreements

### Business Associate Agreement (BAA)

Required for HIPAA compliance when handling Protected Health Information (PHI):

- **Scope**: Covers eligible AWS services
- **Process**: Accept online through Artifact
- **Coverage**: Account-level or Organization-level
- **Requirement**: Must be accepted before storing PHI

### Managing Agreements

| Action | Description | Who Can Perform |
|--------|-------------|-----------------|
| View | See current agreements | Account users with permissions |
| Accept | Accept new agreements | Account administrators |
| Download | Get agreement copies | Account users with permissions |
| Terminate | End agreements | Account administrators |

## Using AWS Artifact with AWS Organizations

```
+------------------------------------------------------------------+
|                      AWS Organizations                            |
+------------------------------------------------------------------+
|                                                                   |
|    +------------------+                                           |
|    | Management Acct  |                                           |
|    | (AWS Artifact)   |                                           |
|    +--------+---------+                                           |
|             |                                                     |
|    +--------+---------+---------+---------+                       |
|    |        |         |         |         |                       |
|    v        v         v         v         v                       |
| +------+ +------+ +------+ +------+ +------+                      |
| |Acct 1| |Acct 2| |Acct 3| |Acct 4| |Acct 5|                      |
| +------+ +------+ +------+ +------+ +------+                      |
|                                                                   |
|    Organization Agreements apply to all member accounts           |
|                                                                   |
+------------------------------------------------------------------+
```

## Common Use Cases

| Use Case | Artifact Feature | Benefit |
|----------|-----------------|---------|
| Annual audit | Reports download | Provide auditors with AWS certifications |
| HIPAA compliance | BAA agreement | Enable PHI storage |
| Customer assurance | SOC 3 report | Share public compliance summary |
| EU data processing | DPA agreement | Meet GDPR requirements |
| Government contracts | FedRAMP reports | Demonstrate federal compliance |

## 🎯 Exam Tips

- **AWS Artifact** is the portal for compliance reports and agreements
- **BAA** must be signed through Artifact for HIPAA compliance
- Reports are **free** to download
- Agreements can be managed at **account or organization level**
- Know that Artifact provides **on-demand, self-service** access

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| AWS Artifact | Self-service compliance portal |
| Artifact Reports | Third-party audit documentation |
| Artifact Agreements | Legal agreements with AWS |
| BAA | Business Associate Agreement for HIPAA |
| SOC Report | Service Organization Control audit |
| NDA | Non-Disclosure Agreement |

## 💡 Key Takeaways

1. AWS Artifact is a free, self-service portal for compliance documentation
2. Two main sections: Reports (audit documents) and Agreements (legal documents)
3. BAA for HIPAA must be signed through AWS Artifact
4. Reports include SOC, ISO, PCI, and regional certifications
5. Agreements can be managed at both account and organization levels

---

*Next: [03 - Geographic and Industry Compliance](../03-geographic-and-industry-compliance/readme.md)*

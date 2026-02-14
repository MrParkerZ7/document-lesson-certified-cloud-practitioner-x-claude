# 🌍 Geographic and Industry Compliance

## File Structure

```
lesson-06-security-governance-and-compliance/
└── 03-geographic-and-industry-compliance/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Different regions and industries have specific compliance requirements that organizations must meet when operating in the cloud. AWS provides services and certifications that help customers meet these diverse regulatory requirements across the globe.

## Geographic Compliance Requirements

### European Union (EU)

| Regulation | Description | Key Requirements |
|------------|-------------|------------------|
| GDPR | General Data Protection Regulation | Data privacy, consent, right to erasure |
| ePrivacy | Electronic communications privacy | Cookie consent, marketing rules |
| NIS Directive | Network security | Critical infrastructure protection |
| EU-US DPF | Data Privacy Framework | Transatlantic data transfers |

### United States

| Regulation | Scope | Key Requirements |
|------------|-------|------------------|
| HIPAA | Healthcare | PHI protection, BAA required |
| SOX | Financial | Internal controls, audit trails |
| GLBA | Financial services | Customer data protection |
| FERPA | Education | Student records privacy |
| CCPA/CPRA | California | Consumer data privacy rights |
| FedRAMP | Federal government | Cloud security authorization |

### Asia-Pacific

| Region | Regulation | Focus Area |
|--------|------------|------------|
| Singapore | PDPA | Personal data protection |
| Australia | Privacy Act | Consumer data protection |
| Japan | APPI | Personal information handling |
| South Korea | PIPA | Personal information protection |
| India | IT Act / DPDP | Data protection |

## AWS Regional Compliance Support

```
+------------------------------------------------------------------+
|                    AWS GLOBAL COMPLIANCE                          |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------+   +----------------+   +----------------+    |
|   |    AMERICAS    |   |     EMEA       |   |   ASIA-PACIFIC |    |
|   +----------------+   +----------------+   +----------------+    |
|   | • FedRAMP      |   | • GDPR         |   | • PDPA         |    |
|   | • HIPAA        |   | • C5           |   | • APPI         |    |
|   | • SOC 1/2/3    |   | • ENS          |   | • MTCS         |    |
|   | • PCI DSS      |   | • Cyber Ess.   |   | • IRAP         |    |
|   | • SOX          |   | • NIS          |   | • K-ISMS       |    |
|   +----------------+   +----------------+   +----------------+    |
|                                                                   |
+------------------------------------------------------------------+
```

## Industry-Specific Compliance

### Healthcare (HIPAA)

| Requirement | AWS Support |
|-------------|-------------|
| BAA Agreement | Available via AWS Artifact |
| Encryption | AWS KMS, S3 encryption |
| Access Controls | IAM, CloudTrail |
| Audit Logging | CloudTrail, CloudWatch |
| Data Integrity | Versioning, checksums |

**HIPAA-Eligible Services:**
- Amazon EC2, S3, RDS
- AWS Lambda, API Gateway
- Amazon DynamoDB
- AWS KMS, CloudTrail

### Financial Services (PCI DSS)

| PCI Requirement | AWS Implementation |
|-----------------|-------------------|
| Network security | VPC, Security Groups |
| Data protection | Encryption, KMS |
| Access management | IAM, MFA |
| Monitoring | CloudTrail, GuardDuty |
| Testing | AWS Config, Inspector |

### Government (FedRAMP)

| Authorization Level | Impact Level | Use Cases |
|--------------------|--------------|-----------|
| Low | Minimal confidentiality | Public data |
| Moderate | Serious adverse effect | Most workloads |
| High | Severe/catastrophic | Classified data |

### Life Sciences (GxP)

| Regulation | Focus | AWS Support |
|------------|-------|-------------|
| FDA 21 CFR Part 11 | Electronic records | Audit trails, signatures |
| EU Annex 11 | Computerized systems | Validation, change control |
| GAMP 5 | Good practices | Qualification support |

## Data Residency and Sovereignty

### AWS Regions for Data Residency

| Requirement | AWS Solution |
|-------------|--------------|
| Keep data in specific country | Choose appropriate AWS Region |
| Data cannot leave region | Configure services accordingly |
| Local backup required | Use same-region backups |
| Compliance certification | Region-specific compliance |

### Data Transfer Considerations

```
+------------------------------------------------------------------+
|                    DATA RESIDENCY OPTIONS                         |
+------------------------------------------------------------------+
|                                                                   |
|    Data must stay in EU              Data can be global           |
|    +------------------+              +------------------+         |
|    | AWS EU Regions   |              | Any AWS Region   |         |
|    | • eu-west-1      |              | • us-east-1      |         |
|    | • eu-central-1   |              | • ap-southeast-1 |         |
|    | • eu-north-1     |              | • etc.           |         |
|    +------------------+              +------------------+         |
|                                                                   |
|    Local compliance:                 Global distribution:         |
|    • GDPR                            • CloudFront CDN             |
|    • National laws                   • Global Accelerator         |
|    • Industry rules                  • Multi-region deploy        |
|                                                                   |
+------------------------------------------------------------------+
```

## Compliance Frameworks by Industry

| Industry | Primary Regulations | AWS Certifications |
|----------|--------------------|--------------------|
| Healthcare | HIPAA, HITECH | BAA, HITRUST |
| Financial | PCI DSS, SOX, GLBA | PCI Level 1, SOC |
| Government | FedRAMP, FISMA | FedRAMP High |
| Education | FERPA | FERPA-compliant services |
| Retail | PCI DSS, GDPR | PCI, ISO 27001 |
| Media | MPAA | Content security |

## AWS Tools for Compliance

| Tool | Purpose | Use Case |
|------|---------|----------|
| AWS Config | Configuration compliance | Track resource configurations |
| AWS Audit Manager | Audit automation | Continuous compliance assessment |
| AWS Security Hub | Security posture | Aggregate compliance findings |
| Amazon Macie | Data discovery | Identify sensitive data |
| AWS CloudTrail | Activity logging | Audit trail for compliance |

## 🎯 Exam Tips

- Know that **GDPR** applies to EU data protection
- Remember **HIPAA** requires a **BAA** from AWS Artifact
- Understand that **data residency** is controlled by **Region selection**
- Know that **FedRAMP** has three authorization levels (Low, Moderate, High)
- **PCI DSS** is required for payment card processing
- AWS provides **regional compliance** certifications

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Data Residency | Requirement to store data in specific geographic location |
| Data Sovereignty | Laws governing data based on country of origin |
| GDPR | EU General Data Protection Regulation |
| FedRAMP | US Federal cloud security program |
| PCI DSS | Payment Card Industry Data Security Standard |
| PHI | Protected Health Information (HIPAA) |

## 💡 Key Takeaways

1. Different regions have different compliance requirements (GDPR, HIPAA, PDPA)
2. AWS Region selection determines where your data resides
3. Industry-specific compliance (healthcare, finance, government) has unique requirements
4. AWS provides certifications and tools to help meet compliance requirements
5. Data residency requirements can be met by choosing appropriate AWS Regions

---

*Next: [04 - Encryption Options](../04-encryption-options/readme.md)*

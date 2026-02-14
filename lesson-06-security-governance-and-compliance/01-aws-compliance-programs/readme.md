# 📋 AWS Compliance Programs

## File Structure

```
lesson-06-security-governance-and-compliance/
└── 01-aws-compliance-programs/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Compliance Programs provide the foundation for organizations to meet regulatory requirements and industry standards when using cloud services. Understanding these programs is essential for the AWS Certified Cloud Practitioner exam, as compliance is a shared responsibility between AWS and its customers.

## What are AWS Compliance Programs?

AWS Compliance Programs are third-party certifications, attestations, and audit reports that demonstrate AWS's commitment to maintaining the highest standards of security and compliance. These programs help customers meet their own compliance requirements by leveraging AWS's certified infrastructure.

## Key Compliance Categories

### Security and Privacy Certifications

| Certification | Description | Scope |
|--------------|-------------|-------|
| SOC 1/2/3 | Service Organization Control reports | Financial and operational controls |
| ISO 27001 | Information Security Management | Global security standard |
| ISO 27017 | Cloud-specific security controls | Cloud security best practices |
| ISO 27018 | Personal data protection | PII in cloud environments |
| ISO 27701 | Privacy Information Management | Privacy management system |

### Industry-Specific Compliance

| Standard | Industry | Key Requirements |
|----------|----------|------------------|
| HIPAA | Healthcare | Protected Health Information (PHI) |
| PCI DSS | Financial | Payment card data security |
| FedRAMP | Government | Federal cloud security |
| GxP | Life Sciences | FDA-regulated systems |
| FERPA | Education | Student data protection |

### Regional Compliance

| Region | Compliance Program | Focus Area |
|--------|-------------------|------------|
| EU | GDPR | Data protection and privacy |
| Germany | C5 | Cloud security controls |
| UK | Cyber Essentials | Basic security controls |
| Singapore | MTCS | Multi-tier cloud security |
| Australia | IRAP | Government security |

## How AWS Achieves Compliance

```
+------------------------------------------------------------------+
|                    AWS COMPLIANCE FRAMEWORK                       |
+------------------------------------------------------------------+
|                                                                   |
|  +------------------------+    +------------------------+         |
|  |   Third-Party Audits   |    |   Internal Controls    |         |
|  |  • Independent auditors|    |  • Security policies   |         |
|  |  • Annual assessments  |    |  • Risk management     |         |
|  |  • Continuous testing  |    |  • Change control      |         |
|  +------------------------+    +------------------------+         |
|                                                                   |
|  +------------------------+    +------------------------+         |
|  |   Certifications       |    |   Attestations         |         |
|  |  • ISO standards       |    |  • SOC reports         |         |
|  |  • Industry standards  |    |  • Third-party audits  |         |
|  |  • Regional standards  |    |  • Penetration tests   |         |
|  +------------------------+    +------------------------+         |
|                                                                   |
+------------------------------------------------------------------+
```

## Compliance and the Shared Responsibility Model

| Responsibility | AWS | Customer |
|---------------|-----|----------|
| Infrastructure compliance | Yes | |
| Physical security certification | Yes | |
| Network compliance | Yes | |
| Application compliance | | Yes |
| Data classification | | Yes |
| User access management | | Yes |
| Data encryption choices | Shared | Shared |

## AWS Compliance Resources

### AWS Artifact

- Central resource for compliance documentation
- On-demand access to AWS security and compliance reports
- Self-service download of AWS audit artifacts
- Access to AWS agreements (BAA, NDA)

### AWS Compliance Center

- Educational hub for compliance information
- Industry-specific guidance
- Compliance whitepapers and case studies
- Partner solutions for compliance

## Benefits of AWS Compliance Programs

1. **Inherited Controls** - Leverage AWS's compliance certifications
2. **Reduced Audit Scope** - Focus on your responsibilities only
3. **Faster Compliance** - Pre-certified infrastructure
4. **Continuous Compliance** - AWS maintains certifications continuously
5. **Global Coverage** - Meet regional requirements worldwide

## 🎯 Exam Tips

- Know that **AWS Artifact** is where you access compliance reports
- Understand that compliance is a **shared responsibility**
- Remember that AWS maintains **SOC, ISO, and PCI** certifications
- Know that **HIPAA compliance** requires a BAA (Business Associate Agreement)
- Understand that customers inherit **infrastructure compliance** from AWS

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| SOC Report | Service Organization Control audit report |
| ISO 27001 | International security management standard |
| PCI DSS | Payment Card Industry Data Security Standard |
| FedRAMP | Federal Risk and Authorization Management Program |
| BAA | Business Associate Agreement (HIPAA requirement) |
| Attestation | Third-party validation of compliance |

## 💡 Key Takeaways

1. AWS maintains over 143 security standards and compliance certifications
2. Compliance is a shared responsibility between AWS and customers
3. AWS Artifact provides on-demand access to compliance reports
4. Customers inherit infrastructure compliance but are responsible for their applications
5. Different industries and regions have specific compliance requirements

---

*Next: [02 - AWS Artifact](../02-aws-artifact/readme.md)*

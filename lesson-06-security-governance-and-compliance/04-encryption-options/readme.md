# 🔐 Encryption Options on AWS

## File Structure

```
lesson-06-security-governance-and-compliance/
└── 04-encryption-options/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Encryption is a fundamental security control that protects data confidentiality. AWS provides comprehensive encryption capabilities for data at rest and data in transit, helping organizations meet security requirements and compliance mandates.

## Types of Encryption

### Encryption at Rest

Protects data stored on disk or in databases:

| Service | Default Encryption | Key Management |
|---------|-------------------|----------------|
| Amazon S3 | SSE-S3 (default) | AWS managed or customer managed |
| Amazon EBS | Optional | AWS KMS |
| Amazon RDS | Optional | AWS KMS |
| DynamoDB | Default enabled | AWS owned or customer managed |
| Amazon EFS | Optional | AWS KMS |

### Encryption in Transit

Protects data moving between locations:

| Protocol | Use Case | AWS Support |
|----------|----------|-------------|
| TLS/SSL | HTTPS connections | All services |
| IPsec | VPN connections | Site-to-Site VPN |
| SSH | Remote access | EC2 instances |
| SFTP | File transfers | AWS Transfer Family |

## AWS Key Management Service (KMS)

### Overview

```
+------------------------------------------------------------------+
|                        AWS KMS                                    |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+   +------------------+   +----------------+|
|   | AWS Managed Keys |   | Customer Managed |   | Custom Key     ||
|   |                  |   | Keys (CMK)       |   | Stores         ||
|   +------------------+   +------------------+   +----------------+|
|   | • Created by AWS |   | • You create     |   | • CloudHSM     ||
|   | • Auto rotation  |   | • You control    |   | • External     ||
|   | • No extra cost  |   | • Audit via      |   | • On-premises  ||
|   |                  |   |   CloudTrail     |   |                ||
|   +------------------+   +------------------+   +----------------+|
|                                                                   |
+------------------------------------------------------------------+
```

### Key Types

| Key Type | Who Creates | Who Manages | Cost |
|----------|-------------|-------------|------|
| AWS Owned | AWS | AWS | Free |
| AWS Managed | AWS | AWS | Free (most services) |
| Customer Managed | Customer | Customer | $1/month + usage |
| Imported | Customer | Customer | $1/month + usage |

### KMS Key Policies

- Define who can use and manage keys
- Required for every KMS key
- Supports IAM policies and grants
- Enables cross-account access

## Server-Side Encryption Options for S3

```
+------------------------------------------------------------------+
|                    S3 ENCRYPTION OPTIONS                          |
+------------------------------------------------------------------+
|                                                                   |
|   +---------------+   +---------------+   +---------------+       |
|   |    SSE-S3     |   |   SSE-KMS     |   |    SSE-C      |       |
|   +---------------+   +---------------+   +---------------+       |
|   | • AWS manages |   | • KMS manages |   | • You manage  |       |
|   |   keys        |   |   keys        |   |   keys        |       |
|   | • AES-256     |   | • Audit trail |   | • Must provide|       |
|   | • Default     |   | • Key rotation|   |   key with    |       |
|   |               |   |               |   |   each request|       |
|   +---------------+   +---------------+   +---------------+       |
|                                                                   |
|   +-------------------------------------------------------+       |
|   |                  Client-Side Encryption               |       |
|   +-------------------------------------------------------+       |
|   | • Encrypt before upload                               |       |
|   | • Customer manages keys entirely                      |       |
|   | • AWS never sees unencrypted data                     |       |
|   +-------------------------------------------------------+       |
|                                                                   |
+------------------------------------------------------------------+
```

### S3 Encryption Comparison

| Option | Key Management | Use Case |
|--------|---------------|----------|
| SSE-S3 | AWS | Simple, default encryption |
| SSE-KMS | Customer via KMS | Audit requirements, key control |
| SSE-C | Customer provided | Full key control |
| Client-side | Customer | Maximum control, encrypt before upload |

## AWS CloudHSM

### Overview

Dedicated hardware security module for:

- Custom key stores for KMS
- SSL/TLS offloading
- Digital signing
- PKCS#11, JCE, CNG interfaces

### CloudHSM vs KMS

| Feature | AWS KMS | AWS CloudHSM |
|---------|---------|--------------|
| Hardware | Shared (multi-tenant) | Dedicated (single-tenant) |
| Key Storage | AWS managed HSM | Customer-controlled HSM |
| Access | AWS API | Industry-standard APIs |
| Compliance | FIPS 140-2 Level 2 | FIPS 140-2 Level 3 |
| Management | Fully managed | Customer managed |
| Cost | Pay per key/request | Hourly + transfer |

## Encryption for AWS Services

### Database Encryption

| Database | At Rest | In Transit | Key Source |
|----------|---------|------------|------------|
| RDS | KMS encryption | TLS | KMS |
| Aurora | KMS encryption | TLS | KMS |
| DynamoDB | Default enabled | TLS | AWS owned or KMS |
| Redshift | KMS or HSM | TLS | KMS or CloudHSM |

### Storage Encryption

| Storage | Encryption Method | Key Options |
|---------|------------------|-------------|
| S3 | SSE-S3, SSE-KMS, SSE-C | Multiple |
| EBS | AES-256 | KMS |
| EFS | AES-256 | KMS |
| FSx | AES-256 | KMS |
| Glacier | Default enabled | AWS managed |

### Compute Encryption

| Service | Data Protection | Notes |
|---------|-----------------|-------|
| EC2 | EBS encryption | Encrypt volumes and snapshots |
| Lambda | Environment variables | KMS encryption |
| ECS/EKS | Secrets Manager | Encrypted secrets |

## Encryption Best Practices

1. **Enable encryption by default** - Use service defaults where available
2. **Use KMS for audit trails** - CloudTrail logs key usage
3. **Rotate keys regularly** - Enable automatic rotation
4. **Use customer managed keys** for sensitive workloads
5. **Encrypt in transit** - Use TLS 1.2 or higher

## 🎯 Exam Tips

- **KMS** is the primary key management service on AWS
- Know the difference between **SSE-S3, SSE-KMS, and SSE-C**
- **CloudHSM** provides dedicated hardware for maximum control
- **S3 default encryption** is SSE-S3 (enabled by default)
- **KMS keys** can be AWS managed or customer managed
- Encryption **in transit** uses TLS/SSL protocols

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| KMS | Key Management Service |
| CMK | Customer Master Key (now called KMS key) |
| HSM | Hardware Security Module |
| SSE | Server-Side Encryption |
| AES-256 | Advanced Encryption Standard (256-bit) |
| TLS | Transport Layer Security |
| Envelope Encryption | Encrypting data key with master key |

## 💡 Key Takeaways

1. AWS provides encryption at rest and in transit for all services
2. AWS KMS is the central key management service
3. Three S3 server-side encryption options: SSE-S3, SSE-KMS, SSE-C
4. CloudHSM offers dedicated hardware for FIPS 140-2 Level 3 compliance
5. Customer managed keys provide audit trails and key control
6. Encryption should be enabled by default for compliance

---

*Next: [05 - Security Services](../05-security-services/readme.md)*

# 🔑 Credential Management

## File Structure

```
lesson-07-aws-access-management/
└── 08-credential-management/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Proper credential management is critical for AWS security. This includes managing passwords, access keys, certificates, and secrets. AWS provides several services and best practices to help secure and manage credentials throughout their lifecycle.

## Types of AWS Credentials

| Credential Type | Use Case | Best Practice |
|----------------|----------|---------------|
| Console password | Human users (console) | Strong password + MFA |
| Access keys | Programmatic access | Use roles instead when possible |
| SSH keys | EC2 instance access | EC2 Instance Connect preferred |
| Signing certificates | Code signing | ACM for certificates |
| Database credentials | Application database access | Secrets Manager |

## Credential Security Best Practices

```
+------------------------------------------------------------------+
|              CREDENTIAL SECURITY BEST PRACTICES                   |
+------------------------------------------------------------------+
|                                                                   |
|  +------------------+  +------------------+  +------------------+ |
|  |     ROTATE       |  |     STORE        |  |    AUDIT         | |
|  |   Credentials    |  |    Securely      |  |   Access         | |
|  +------------------+  +------------------+  +------------------+ |
|  | • Regular key    |  | • Secrets Manager|  | • CloudTrail     | |
|  |   rotation       |  | • Parameter Store|  | • IAM Credential | |
|  | • Auto-rotation  |  | • Never in code  |  |   Report         | |
|  | • Password expiry|  | • Never in Git   |  | • Access Analyzer| |
|  +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Secrets Manager

Centralized secrets management service for storing and rotating credentials.

### Key Features

| Feature | Description |
|---------|-------------|
| Secure storage | Encrypted with KMS |
| Automatic rotation | Built-in rotation for RDS, Redshift |
| Fine-grained access | IAM policies control access |
| Audit | CloudTrail logs all access |
| Cross-account | Share secrets across accounts |

### Secrets Manager vs Parameter Store

| Feature | Secrets Manager | Parameter Store |
|---------|-----------------|-----------------|
| Auto-rotation | Yes (built-in) | No (manual) |
| Cost | $0.40/secret/month | Free tier available |
| Encryption | Always encrypted | Optional encryption |
| Database integration | Native for RDS | Manual |
| Versioning | Yes | Yes |
| Best for | Database credentials | Configuration data |

## AWS Systems Manager Parameter Store

Secure, hierarchical storage for configuration data and secrets.

| Parameter Type | Description | Use Case |
|----------------|-------------|----------|
| String | Plain text | Configuration values |
| StringList | Comma-separated | Lists of values |
| SecureString | Encrypted with KMS | Secrets, passwords |

## Access Key Best Practices

### Do

| Practice | Reason |
|----------|--------|
| Use IAM roles | No keys to manage |
| Rotate keys regularly | Limit exposure window |
| Delete unused keys | Reduce attack surface |
| Use temporary credentials | More secure than long-term |
| One key per application | Isolate access |

### Don't

| Anti-Pattern | Risk |
|--------------|------|
| Embed in code | Exposed in repos |
| Share keys | No accountability |
| Use root keys | Unlimited access |
| Store in plain text | Easy to steal |
| Keep inactive keys | Unused attack vector |

## IAM Credential Report

A downloadable report showing all IAM users and their credential status.

| Field | Information |
|-------|-------------|
| User | IAM username |
| Password status | Enabled, disabled, never used |
| Password last used | Date of last console login |
| Access keys | Status and last used date |
| MFA | Whether MFA is enabled |

### Generating Credential Report

```
1. IAM Console -> Credential Report
2. Click "Download Report"
3. Review CSV for security issues
```

## Key Rotation Strategies

### Access Key Rotation

```
+------------------------------------------------------------------+
|                    KEY ROTATION PROCESS                           |
+------------------------------------------------------------------+
|                                                                   |
|   1. Create New Key    2. Update Apps    3. Test    4. Delete Old |
|   +-------------+      +-------------+   +------+   +-------------+
|   | New Key     | ---> | Deploy new  |-->| Test |-->| Remove old  |
|   | (Active)    |      | key to apps |   |      |   | key         |
|   +-------------+      +-------------+   +------+   +-------------+
|                                                                   |
+------------------------------------------------------------------+
```

### Automatic Rotation with Secrets Manager

| Database | Rotation Support |
|----------|-----------------|
| RDS | Built-in |
| Aurora | Built-in |
| Redshift | Built-in |
| DocumentDB | Built-in |
| Other | Custom Lambda |

## Password Policies

Configure password requirements for IAM users:

| Setting | Options |
|---------|---------|
| Minimum length | 6-128 characters |
| Require uppercase | Yes/No |
| Require lowercase | Yes/No |
| Require numbers | Yes/No |
| Require symbols | Yes/No |
| Password expiration | 1-1095 days |
| Prevent reuse | 1-24 previous passwords |
| Allow self-change | Yes/No |

## AWS Certificate Manager (ACM)

Manage SSL/TLS certificates for AWS services.

| Feature | Description |
|---------|-------------|
| Free public certs | For AWS services |
| Auto-renewal | Automatic before expiry |
| Integration | CloudFront, ELB, API Gateway |
| Private CA | For internal certificates |

## Monitoring Credentials

| Service | Purpose |
|---------|---------|
| CloudTrail | Log API calls including credential use |
| IAM Access Analyzer | Find unused permissions |
| IAM Credential Report | Overview of all credentials |
| GuardDuty | Detect compromised credentials |
| Config | Track IAM configuration changes |

## 🎯 Exam Tips

- **Secrets Manager** = best for database credentials with auto-rotation
- **Parameter Store** = configuration and secrets (cheaper)
- **Credential Report** = shows all users and credential status
- **Access keys** should be rotated regularly
- **Never embed credentials** in code
- **Use IAM roles** instead of access keys when possible
- Know the difference between **Secrets Manager** and **Parameter Store**
- **MFA** should be enabled for all users

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Secrets Manager | Service for storing and rotating secrets |
| Parameter Store | Hierarchical storage for config/secrets |
| Credential Report | Report of all IAM user credentials |
| Key Rotation | Process of replacing old keys with new |
| ACM | AWS Certificate Manager |
| SecureString | Encrypted parameter in Parameter Store |

## 💡 Key Takeaways

1. Never embed credentials in code or commit to version control
2. Use IAM roles instead of access keys when possible
3. Secrets Manager provides automatic rotation for database credentials
4. Parameter Store is cost-effective for configuration data
5. Generate IAM Credential Reports regularly for security audits
6. Rotate access keys on a regular schedule
7. Enable MFA for all users, especially those with console access

---

*Next: [Lesson 08 - Security Resources and Components](../../lesson-08-security-resources-and-components/01-aws-security-services-overview/readme.md)*

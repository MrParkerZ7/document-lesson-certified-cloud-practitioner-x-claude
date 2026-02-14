# 🔄 Cross-Account Access

## File Structure

```
lesson-07-aws-access-management/
└── 07-cross-account-access/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Cross-account access allows users and services in one AWS account to access resources in another AWS account. This is essential for organizations that use multiple AWS accounts for different environments, teams, or purposes.

## What is Cross-Account Access?

Cross-account access enables controlled sharing of resources and permissions between separate AWS accounts without sharing credentials.

```
+------------------------------------------------------------------+
|                    CROSS-ACCOUNT ACCESS                           |
+------------------------------------------------------------------+
|                                                                   |
|   Account A                           Account B                   |
|   (Source)                            (Target)                    |
|   +-------------+                     +-------------+             |
|   |  IAM User/  |   Assume Role       |  IAM Role   |             |
|   |  Role       | ------------------>  | (Trust A)  |             |
|   +-------------+                     +-------------+             |
|                                              |                    |
|                                              v                    |
|                                       +-------------+             |
|                                       |  Resources  |             |
|                                       +-------------+             |
|                                                                   |
+------------------------------------------------------------------+
```

## Why Use Cross-Account Access?

| Benefit | Description |
|---------|-------------|
| Security | No credential sharing between accounts |
| Isolation | Keep environments separate |
| Centralized billing | Consolidated billing with Organizations |
| Delegation | Grant specific access without full admin |
| Audit | Clear audit trail of who accessed what |

## How Cross-Account Access Works

### Step 1: Create Role in Target Account (Account B)

The target account creates an IAM role with:
- **Trust policy**: Who can assume the role (Account A)
- **Permission policy**: What the role can do

### Step 2: Grant Permission in Source Account (Account A)

The source account grants users permission to assume the role in Account B.

### Step 3: Assume the Role

Users in Account A call `sts:AssumeRole` to get temporary credentials for Account B.

## Trust Policy Example

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::111111111111:root"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

## Cross-Account Access Flow

```
+------------------------------------------------------------------+
|                    ASSUME ROLE FLOW                               |
+------------------------------------------------------------------+
|                                                                   |
|   1. User in Account A        2. STS returns               3. User|
|      calls AssumeRole            temporary credentials        uses |
|                                                              creds|
|   +-------+                   +-------+                   +-------+
|   | Acct A|  --AssumeRole-->  |  STS  |  --Temp Creds-->  | Acct B|
|   | User  |                   +-------+                   | Role  |
|   +-------+                                               +-------+
|                                                                   |
|   Temp credentials include:                                       |
|   - Access Key ID                                                 |
|   - Secret Access Key                                             |
|   - Session Token                                                 |
|   - Expiration                                                    |
|                                                                   |
+------------------------------------------------------------------+
```

## Methods for Cross-Account Access

### 1. IAM Roles (Recommended)

| Feature | Description |
|---------|-------------|
| Method | Assume role in target account |
| Credentials | Temporary (from STS) |
| Security | High - no shared credentials |
| Use case | Most cross-account scenarios |

### 2. Resource-Based Policies

Some services support resource-based policies that allow cross-account access directly.

| Service | Resource Policy |
|---------|-----------------|
| S3 | Bucket policy |
| KMS | Key policy |
| SQS | Queue policy |
| SNS | Topic policy |
| Lambda | Function policy |

### 3. AWS Organizations

| Feature | Description |
|---------|-------------|
| SCPs | Control maximum permissions |
| RAM | Resource Access Manager for sharing |
| Trusted access | Enable service integrations |

## Common Cross-Account Scenarios

| Scenario | Solution |
|----------|----------|
| Central logging | Log account assumes role in other accounts |
| Deployment | CI/CD account deploys to prod account |
| Shared services | Central account provides services |
| Security audit | Security account audits all accounts |
| Backup | Backup account accesses data accounts |

## AWS Resource Access Manager (RAM)

AWS RAM allows sharing of resources across accounts.

| Shareable Resources | Use Case |
|--------------------|----------|
| VPC Subnets | Shared networking |
| Transit Gateways | Network connectivity |
| Route 53 Resolver | DNS resolution |
| License Manager | License sharing |
| AWS Outposts | Shared edge compute |

## Cross-Account Best Practices

1. **Use IAM roles**, not shared credentials
2. **Apply least privilege** to cross-account roles
3. **Use external IDs** for third-party access
4. **Enable CloudTrail** in all accounts
5. **Use AWS Organizations** for account management
6. **Require MFA** for assuming sensitive roles
7. **Regularly review** cross-account access

## External ID for Third-Party Access

External ID prevents the "confused deputy" problem when granting third-party access.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::THIRD-PARTY-ACCOUNT:root"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "sts:ExternalId": "YOUR-UNIQUE-EXTERNAL-ID"
                }
            }
        }
    ]
}
```

## 🎯 Exam Tips

- **IAM roles** are the recommended method for cross-account access
- **Trust policy** defines who can assume the role
- **STS AssumeRole** returns temporary credentials
- **Resource-based policies** can also enable cross-account access (S3, KMS)
- **External ID** is used for third-party access
- **AWS Organizations** simplifies multi-account management
- No credentials are shared - only temporary credentials are used

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Cross-Account | Access between different AWS accounts |
| Trust Policy | IAM role policy defining who can assume |
| AssumeRole | STS API to get temporary credentials |
| External ID | Unique identifier for third-party access |
| Resource-Based Policy | Policy attached to a resource |
| RAM | Resource Access Manager |

## 💡 Key Takeaways

1. Cross-account access uses IAM roles, not shared credentials
2. Trust policies define which accounts can assume a role
3. Users call AssumeRole to get temporary credentials
4. Resource-based policies provide an alternative for some services
5. External IDs protect against confused deputy attacks
6. AWS Organizations and RAM simplify multi-account management

---

*Next: [08 - Credential Management](../08-credential-management/readme.md)*

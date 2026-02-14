# 🔐 AWS IAM Overview

## File Structure

```
lesson-07-aws-access-management/
└── 01-aws-iam-overview/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Identity and Access Management (IAM) is a foundational service that controls who can access your AWS resources and what actions they can perform. Understanding IAM is essential for the AWS Certified Cloud Practitioner exam and for securing any AWS environment.

## What is AWS IAM?

IAM is a web service that helps you securely control access to AWS resources. It enables you to create and manage AWS users, groups, and permissions to allow or deny access to AWS resources.

## Key IAM Components

```
+------------------------------------------------------------------+
|                           AWS IAM                                 |
+------------------------------------------------------------------+
|                                                                   |
|   +-------------+    +-------------+    +-------------+           |
|   |    USERS    |    |   GROUPS    |    |    ROLES    |           |
|   +-------------+    +-------------+    +-------------+           |
|   | Individual  |    | Collection  |    | Temporary   |           |
|   | identities  |    | of users    |    | credentials |           |
|   | for people  |    | with same   |    | for services|           |
|   |             |    | permissions |    | & federation|           |
|   +-------------+    +-------------+    +-------------+           |
|          |                 |                   |                  |
|          +--------+--------+--------+----------+                  |
|                   |                                               |
|                   v                                               |
|          +------------------+                                     |
|          |     POLICIES     |                                     |
|          +------------------+                                     |
|          | JSON documents   |                                     |
|          | that define      |                                     |
|          | permissions      |                                     |
|          +------------------+                                     |
|                                                                   |
+------------------------------------------------------------------+
```

## IAM Users

Individual identities that represent a person or application needing AWS access.

| Feature | Description |
|---------|-------------|
| Long-term credentials | Password for console, access keys for CLI/API |
| Individual identity | One user per person (best practice) |
| Direct permissions | Can attach policies directly to user |
| Group membership | Can belong to multiple groups |

## IAM Groups

Collections of IAM users that share the same permissions.

| Feature | Description |
|---------|-------------|
| Simplify management | Apply permissions to multiple users at once |
| Logical grouping | Organize users by job function |
| No nesting | Groups cannot contain other groups |
| Users in multiple groups | A user can belong to multiple groups |

### Common Group Examples

| Group Name | Purpose | Typical Permissions |
|------------|---------|-------------------|
| Administrators | Full AWS access | AdministratorAccess |
| Developers | Development resources | EC2, S3, Lambda access |
| ReadOnly | View-only access | ReadOnlyAccess |
| Billing | Cost management | Billing and cost reports |

## IAM Roles

Temporary security credentials for trusted entities.

| Feature | Description |
|---------|-------------|
| No long-term credentials | Temporary credentials via STS |
| Assumable | Can be assumed by users, services, accounts |
| Cross-account access | Enable access across AWS accounts |
| Service roles | Allow AWS services to perform actions |

### Common Role Use Cases

| Use Case | Example |
|----------|---------|
| EC2 instance role | Allow EC2 to access S3 |
| Lambda execution role | Allow Lambda to write to DynamoDB |
| Cross-account | Allow Account B to access Account A resources |
| Federation | Allow external users to access AWS |

## IAM Policies

JSON documents that define permissions.

### Policy Structure

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::my-bucket/*"
        }
    ]
}
```

### Policy Types

| Policy Type | Description | Use Case |
|-------------|-------------|----------|
| AWS Managed | Pre-built by AWS | Common use cases |
| Customer Managed | Created by you | Custom requirements |
| Inline | Embedded in entity | Strict 1:1 relationship |

### Key Policy Elements

| Element | Description | Example |
|---------|-------------|---------|
| Effect | Allow or Deny | "Allow" |
| Action | What operations | "s3:GetObject" |
| Resource | Which resources | "arn:aws:s3:::bucket/*" |
| Condition | When to apply | IP address, time, MFA |

## IAM Best Practices

1. **Enable MFA** - Add extra authentication factor
2. **Use groups** - Don't attach policies to users directly
3. **Least privilege** - Grant minimum permissions needed
4. **Use roles** - Prefer roles over long-term credentials
5. **Rotate credentials** - Regular key rotation
6. **Remove unused credentials** - Clean up inactive users/keys
7. **Use policy conditions** - Add extra restrictions

## IAM Features Summary

| Feature | Free | Global | Purpose |
|---------|------|--------|---------|
| Users | Yes | Yes | Individual identities |
| Groups | Yes | Yes | Organize users |
| Roles | Yes | Yes | Temporary credentials |
| Policies | Yes | Yes | Define permissions |
| MFA | Yes | Yes | Extra security |

## 🎯 Exam Tips

- IAM is **global** - not region-specific
- IAM is **free** to use
- **Root user** should rarely be used; create IAM users instead
- **Groups** can only contain users, not other groups
- **Roles** provide temporary credentials (no permanent keys)
- **Policies** are JSON documents with Effect, Action, Resource
- **Deny** always wins over Allow
- Know the difference between **authentication** (who you are) and **authorization** (what you can do)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| IAM User | Individual identity for person or application |
| IAM Group | Collection of users with shared permissions |
| IAM Role | Temporary credentials for trusted entities |
| IAM Policy | JSON document defining permissions |
| Principal | Entity that can request actions on AWS resources |
| ARN | Amazon Resource Name - unique identifier |

## 💡 Key Takeaways

1. IAM controls authentication and authorization for AWS resources
2. Users are for individuals; groups organize users; roles provide temporary access
3. Policies define what actions are allowed or denied on which resources
4. IAM is global and free to use
5. Always follow the principle of least privilege
6. Use roles instead of sharing access keys

---

*Next: [02 - Root User Account](../02-root-user-account/readme.md)*

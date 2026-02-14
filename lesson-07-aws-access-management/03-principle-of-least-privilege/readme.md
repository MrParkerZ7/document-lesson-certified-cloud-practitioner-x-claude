# 🔒 Principle of Least Privilege

## File Structure

```
lesson-07-aws-access-management/
└── 03-principle-of-least-privilege/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The principle of least privilege (PoLP) is a fundamental security concept that states users, applications, and systems should only have the minimum permissions necessary to perform their intended functions. This principle is crucial for AWS security and is a key topic for the Cloud Practitioner exam.

## What is Least Privilege?

Least privilege means granting only the permissions required to complete a task - nothing more, nothing less. It reduces the risk of accidental or malicious misuse of access.

```
+------------------------------------------------------------------+
|              PRINCIPLE OF LEAST PRIVILEGE                         |
+------------------------------------------------------------------+
|                                                                   |
|   TOO MUCH ACCESS              LEAST PRIVILEGE                    |
|   (Risky)                      (Secure)                           |
|                                                                   |
|   +----------------+           +----------------+                  |
|   | User: DevOps   |           | User: DevOps   |                  |
|   +----------------+           +----------------+                  |
|   | Permission:    |           | Permission:    |                  |
|   | Admin Access   |           | EC2: Start/Stop|                  |
|   | (Everything)   |           | S3: Read bucket|                  |
|   |                |           | Lambda: Deploy |                  |
|   +----------------+           +----------------+                  |
|          |                            |                           |
|          v                            v                           |
|   Risk: Can delete    Risk: Limited to                            |
|   anything by         specific tasks                              |
|   mistake                                                         |
|                                                                   |
+------------------------------------------------------------------+
```

## Why Least Privilege Matters

| Benefit | Description |
|---------|-------------|
| Reduced risk | Limits damage from compromised credentials |
| Compliance | Required by many regulatory frameworks |
| Audit trail | Easier to track who did what |
| Blast radius | Contains incidents to smaller scope |
| Defense in depth | Part of layered security strategy |

## Implementing Least Privilege in AWS

### Start with No Permissions

```
+------------------------------------------------------------------+
|                 PERMISSION BUILD-UP                               |
+------------------------------------------------------------------+
|                                                                   |
|   Step 1: Start Empty     Step 2: Add Needed      Step 3: Review  |
|   +----------------+      +----------------+      +----------------+
|   | No permissions |  ->  | + EC2 read     |  ->  | Verify access  |
|   |                |      | + S3 list      |      | Remove unused  |
|   +----------------+      +----------------+      +----------------+
|                                                                   |
+------------------------------------------------------------------+
```

### Use IAM Policy Structure

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeInstances",
                "ec2:StartInstances",
                "ec2:StopInstances"
            ],
            "Resource": "arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0"
        }
    ]
}
```

## Least Privilege Best Practices

### 1. Start with AWS Managed Policies

| Approach | Description | When to Use |
|----------|-------------|-------------|
| AWS Managed | Pre-built by AWS | Common use cases |
| Job Function | Role-based policies | Standard job roles |
| Custom | You create | Specific requirements |

### 2. Use Conditions

Add extra restrictions to policies:

| Condition | Example Use |
|-----------|-------------|
| IP Address | Only allow from corporate IP |
| MFA | Require MFA for sensitive actions |
| Time | Only during business hours |
| Region | Restrict to specific regions |

### 3. Scope Resources

| Resource Scope | Example | Security Level |
|----------------|---------|----------------|
| All resources (*) | "Resource": "*" | Lowest |
| Service-wide | "Resource": "arn:aws:s3:::*" | Low |
| Specific bucket | "arn:aws:s3:::my-bucket" | Medium |
| Specific object | "arn:aws:s3:::my-bucket/folder/*" | High |

## AWS Tools for Least Privilege

### IAM Access Analyzer

| Feature | Description |
|---------|-------------|
| Unused access | Identifies permissions not being used |
| Policy validation | Checks policies for issues |
| External access | Finds resources shared externally |
| Policy generation | Creates policies from access activity |

### IAM Access Advisor

| Feature | Description |
|---------|-------------|
| Service last accessed | Shows when services were last used |
| Unused permissions | Identify over-permissioned users |
| Refinement guidance | Suggests permission reductions |

### AWS Organizations SCPs

Service Control Policies provide guardrails:

| Use Case | SCP Implementation |
|----------|-------------------|
| Deny unused regions | Block services in non-approved regions |
| Require encryption | Deny unencrypted resource creation |
| Prevent service usage | Block expensive or risky services |

## Common Mistakes to Avoid

| Mistake | Problem | Solution |
|---------|---------|----------|
| Using * for actions | Grants all actions | List specific actions |
| Using * for resources | Applies to everything | Specify resource ARNs |
| Copying admin policies | Over-permissioned | Start minimal, add as needed |
| Not reviewing | Permissions creep | Regular audits |
| Sharing credentials | No accountability | Individual users |

## Least Privilege Examples

### Example 1: S3 Read-Only User

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::reports-bucket",
                "arn:aws:s3:::reports-bucket/*"
            ]
        }
    ]
}
```

### Example 2: Lambda Developer

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lambda:CreateFunction",
                "lambda:UpdateFunctionCode",
                "lambda:InvokeFunction"
            ],
            "Resource": "arn:aws:lambda:us-east-1:123456789012:function:my-function"
        }
    ]
}
```

## 🎯 Exam Tips

- **Least privilege** = minimum permissions needed
- Start with **no permissions** and add what's needed
- Use **IAM Access Analyzer** to identify unused permissions
- **Conditions** add extra restrictions (IP, MFA, time)
- Avoid **wildcards (*)** when possible
- **Review permissions** regularly
- Know that least privilege is a **security best practice**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Least Privilege | Minimum permissions necessary |
| Permissions Boundary | Maximum permissions limit |
| Access Analyzer | Tool to identify unused access |
| Access Advisor | Shows last accessed services |
| Resource-level | Permissions on specific resources |
| Action-level | Permissions on specific operations |

## 💡 Key Takeaways

1. Grant only the minimum permissions necessary to perform a task
2. Start with no permissions and add incrementally
3. Use IAM Access Analyzer and Access Advisor to audit permissions
4. Avoid wildcards in Actions and Resources when possible
5. Use conditions to add additional restrictions
6. Regularly review and remove unused permissions

---

*Next: [04 - Authentication Methods](../04-authentication-methods/readme.md)*

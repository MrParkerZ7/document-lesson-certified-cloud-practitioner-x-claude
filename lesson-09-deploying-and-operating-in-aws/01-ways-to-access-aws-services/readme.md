# 🔗 Ways to Access AWS Services

## File Structure

```
lesson-09-deploying-and-operating-in-aws/
└── 01-ways-to-access-aws-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides multiple ways to access and manage your cloud resources. Understanding these access methods is essential for effectively working with AWS services. Each method has its own use cases and advantages.

## AWS Access Methods Overview

```
+------------------------------------------------------------------+
|                    WAYS TO ACCESS AWS                             |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   | AWS MANAGEMENT   |  |    AWS CLI       |  |   AWS SDKs       | |
|   |    CONSOLE       |  |                  |  |                  | |
|   +------------------+  +------------------+  +------------------+ |
|   | Web-based GUI    |  | Command-line     |  | Programming      | |
|   | Point and click  |  | Scripting        |  | language access  | |
|   | Visual feedback  |  | Automation       |  | Application      | |
|   |                  |  |                  |  | integration      | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
|                       +------------------+                        |
|                       |    AWS APIs      |                        |
|                       +------------------+                        |
|                       | Direct HTTP calls |                       |
|                       | All methods use   |                       |
|                       | APIs underneath   |                       |
|                       +------------------+                        |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Management Console

The web-based graphical user interface for AWS.

| Feature | Description |
|---------|-------------|
| Access | Browser-based, any device |
| Authentication | Username/password + MFA |
| Use cases | Visual management, learning, ad-hoc tasks |
| URL | console.aws.amazon.com |

### Console Features

| Feature | Description |
|---------|-------------|
| Service search | Quick search for any service |
| Resource groups | Organize resources |
| CloudShell | Built-in CLI in browser |
| Region selector | Switch between regions |
| Account settings | Manage account |

## AWS Command Line Interface (CLI)

Command-line tool for managing AWS services.

| Feature | Description |
|---------|-------------|
| Installation | Windows, macOS, Linux |
| Authentication | Access keys or IAM roles |
| Output formats | JSON, YAML, text, table |
| Use cases | Scripting, automation, quick commands |

### CLI Examples

```bash
# List S3 buckets
aws s3 ls

# Describe EC2 instances
aws ec2 describe-instances

# Create an S3 bucket
aws s3 mb s3://my-bucket-name

# Get caller identity
aws sts get-caller-identity
```

### CLI Versions

| Version | Description |
|---------|-------------|
| AWS CLI v2 | Current version, recommended |
| AWS CLI v1 | Legacy version |

## AWS SDKs

Software Development Kits for programming languages.

| Language | SDK Name |
|----------|----------|
| Python | Boto3 |
| JavaScript | AWS SDK for JavaScript |
| Java | AWS SDK for Java |
| .NET | AWS SDK for .NET |
| Go | AWS SDK for Go |
| Ruby | AWS SDK for Ruby |
| PHP | AWS SDK for PHP |
| C++ | AWS SDK for C++ |

### SDK Use Cases

| Use Case | Description |
|----------|-------------|
| Application integration | Build apps that use AWS |
| Automation | Programmatic resource management |
| Custom tools | Build internal tools |
| Lambda functions | Interact with AWS from Lambda |

## AWS CloudShell

Browser-based shell in the AWS Console.

| Feature | Description |
|---------|-------------|
| Access | Built into AWS Console |
| Pre-installed | AWS CLI, SDKs, common tools |
| Storage | 1 GB persistent storage |
| Authentication | Uses console credentials |
| Cost | Free to use |

## AWS APIs

All access methods use AWS APIs underneath.

| Component | Description |
|-----------|-------------|
| REST APIs | HTTP-based service interfaces |
| Authentication | Signature Version 4 |
| Endpoints | Service-specific URLs |
| Actions | Operations on resources |

## Comparison of Access Methods

| Method | Best For | Authentication |
|--------|----------|----------------|
| Console | Visual tasks, learning | Username/password + MFA |
| CLI | Scripting, quick commands | Access keys, IAM roles |
| SDKs | Application development | Access keys, IAM roles |
| CloudShell | Quick CLI access | Console session |
| APIs | Custom implementations | Signature V4 |

## Infrastructure as Code Access

| Tool | Description |
|------|-------------|
| CloudFormation | AWS-native IaC |
| Terraform | Multi-cloud IaC |
| CDK | Code-based infrastructure |
| SAM | Serverless deployment |

## Mobile and Additional Access

| Tool | Description |
|------|-------------|
| AWS Console Mobile App | Mobile device access |
| AWS Tools for PowerShell | PowerShell cmdlets |
| AWS Tools for Visual Studio | IDE integration |
| AWS Toolkit for VS Code | VS Code extension |

## Authentication Methods

```
+------------------------------------------------------------------+
|                    AUTHENTICATION OPTIONS                         |
+------------------------------------------------------------------+
|                                                                   |
|   Console                 CLI/SDK                APIs             |
|   +-------------+        +-------------+        +-------------+   |
|   | Username +  |        | Access Keys |        | Signature   |   |
|   | Password    |        | (ID + Secret)|       | Version 4   |   |
|   +-------------+        +-------------+        +-------------+   |
|        |                       |                      |           |
|        v                       v                      v           |
|   +-------------+        +-------------+        +-------------+   |
|   | MFA Token   |        | IAM Roles   |        | STS Tokens  |   |
|   | (Optional)  |        | (Preferred) |        |             |   |
|   +-------------+        +-------------+        +-------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **Console** = web-based GUI, good for visual management
- **CLI** = command-line, good for scripting and automation
- **SDKs** = programming language libraries for app development
- **CloudShell** = free browser-based CLI in console
- **All methods use AWS APIs** underneath
- **Access keys** = ID + secret for programmatic access
- **IAM roles** preferred over access keys for EC2, Lambda

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| AWS Console | Web-based management interface |
| AWS CLI | Command-line interface tool |
| SDK | Software Development Kit |
| CloudShell | Browser-based shell environment |
| Access Keys | Credentials for programmatic access |
| API | Application Programming Interface |

## 💡 Key Takeaways

1. AWS provides multiple access methods: Console, CLI, SDKs, CloudShell
2. The Console is best for visual management and learning
3. CLI is ideal for scripting and automation
4. SDKs enable programmatic access from applications
5. CloudShell provides free CLI access from the browser
6. All access methods use AWS APIs underneath
7. IAM roles are preferred over access keys for programmatic access

---

*Next: [02 - Infrastructure as Code](../02-infrastructure-as-code/readme.md)*

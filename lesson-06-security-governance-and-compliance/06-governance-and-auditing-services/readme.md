# 📊 Governance and Auditing Services

## File Structure

```
lesson-06-security-governance-and-compliance/
└── 06-governance-and-auditing-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides comprehensive governance and auditing services that help organizations maintain control, ensure compliance, and track all activities within their AWS environment. These services are essential for security, compliance audits, and operational visibility.

## AWS CloudTrail

### Overview

AWS CloudTrail is a service that enables governance, compliance, and operational and risk auditing of your AWS account. It records all API calls and events across your AWS infrastructure.

```
+------------------------------------------------------------------+
|                        AWS CLOUDTRAIL                             |
+------------------------------------------------------------------+
|                                                                   |
|    API Call Made          Event Recorded         Stored in S3     |
|   +-------------+        +-------------+        +-------------+   |
|   |  Console    |  --->  |  CloudTrail |  --->  |   S3 Bucket |   |
|   |  CLI        |        |   Event     |        |   (Logs)    |   |
|   |  SDK        |        |             |        |             |   |
|   |  Service    |        +-------------+        +-------------+   |
|   +-------------+               |                                 |
|                                 v                                 |
|                        +-------------+                            |
|                        | CloudWatch  |                            |
|                        |   Logs      |                            |
|                        +-------------+                            |
|                                                                   |
+------------------------------------------------------------------+
```

### CloudTrail Features

| Feature | Description |
|---------|-------------|
| Event History | 90 days of management events (free) |
| Trails | Long-term storage to S3 |
| Multi-Region | Single trail for all regions |
| Organization Trail | Trail for all accounts in org |
| Data Events | S3 object-level, Lambda invocations |
| Insights | Detect unusual API activity |

### Event Types

| Event Type | What It Captures | Example |
|------------|------------------|---------|
| Management Events | Control plane operations | CreateBucket, LaunchInstance |
| Data Events | Data plane operations | GetObject, PutObject |
| Insights Events | Unusual activity patterns | Spike in API calls |

### CloudTrail Best Practices

1. **Enable in all regions** - Capture activity everywhere
2. **Enable log file integrity** - Detect tampering
3. **Encrypt logs** - Use KMS encryption
4. **Send to CloudWatch Logs** - Enable real-time monitoring
5. **Enable Insights** - Detect anomalies

## AWS Config

### Overview

AWS Config provides a detailed view of AWS resource configurations and how they change over time. It enables compliance auditing, security analysis, and change management.

```
+------------------------------------------------------------------+
|                          AWS CONFIG                               |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------+    +----------------+    +----------------+  |
|   | Configuration  |    |   Config       |    |   Compliance   |  |
|   | Recording      |--->|   History      |--->|   Dashboard    |  |
|   +----------------+    +----------------+    +----------------+  |
|          |                                           |            |
|          v                                           v            |
|   +----------------+                         +----------------+   |
|   | Configuration  |                         | Config Rules   |   |
|   | Snapshots      |                         | (Compliance)   |   |
|   +----------------+                         +----------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

### Config Features

| Feature | Description |
|---------|-------------|
| Configuration Recording | Track all resource configurations |
| Configuration History | View past configurations |
| Config Rules | Evaluate compliance of resources |
| Conformance Packs | Collections of Config rules |
| Aggregator | Multi-account, multi-region view |
| Remediation | Auto-fix non-compliant resources |

### AWS Config Rules

| Rule Type | Description | Example |
|-----------|-------------|---------|
| AWS Managed | Pre-built by AWS | s3-bucket-public-read-prohibited |
| Custom | Lambda-based custom rules | Check for specific tags |

### Popular Config Rules

| Rule | What It Checks |
|------|----------------|
| encrypted-volumes | EBS volumes are encrypted |
| s3-bucket-versioning-enabled | S3 buckets have versioning |
| restricted-ssh | SSH not open to 0.0.0.0/0 |
| root-account-mfa-enabled | MFA on root account |
| rds-instance-public-access-check | RDS not publicly accessible |

## AWS Audit Manager

### Overview

AWS Audit Manager helps continuously audit AWS usage to simplify risk assessment and compliance with regulations.

| Feature | Description |
|---------|-------------|
| Prebuilt Frameworks | CIS, PCI DSS, SOC 2, GDPR, HIPAA |
| Evidence Collection | Automatic evidence gathering |
| Assessment Reports | Generate audit-ready reports |
| Custom Frameworks | Build your own frameworks |
| Control Mapping | Map controls to evidence |

### Audit Manager Process

```
+------------------------------------------------------------------+
|                     AWS AUDIT MANAGER                             |
+------------------------------------------------------------------+
|                                                                   |
|  1. Select Framework     2. Collect Evidence    3. Generate Report|
|  +----------------+     +----------------+     +----------------+  |
|  | • CIS          |     | • CloudTrail   |     | • PDF Reports  |  |
|  | • PCI DSS      | --> | • Config       | --> | • Evidence     |  |
|  | • SOC 2        |     | • Security Hub |     | • Compliance   |  |
|  | • Custom       |     | • Manual       |     |   Status       |  |
|  +----------------+     +----------------+     +----------------+  |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Organizations

### Governance with Organizations

| Feature | Description |
|---------|-------------|
| Service Control Policies (SCPs) | Restrict services/actions |
| Organizational Units (OUs) | Group accounts |
| Consolidated Billing | Single payment method |
| Tag Policies | Enforce tagging standards |
| Backup Policies | Centralized backup rules |
| AI Services Opt-out Policies | Control AI data usage |

### SCP Example Use Cases

| Use Case | SCP Implementation |
|----------|-------------------|
| Prevent leaving org | Deny organizations:LeaveOrganization |
| Require encryption | Deny s3:PutObject without encryption |
| Region restriction | Allow only specific regions |
| Prevent root usage | Deny actions with root user |

## AWS Systems Manager

### Governance Features

| Feature | Description |
|---------|-------------|
| Parameter Store | Secure configuration storage |
| Patch Manager | Automate patching |
| Compliance | Track patch/configuration compliance |
| Inventory | Collect software/configuration data |
| State Manager | Maintain consistent config |

## Service Comparison

| Service | Primary Use | Key Feature |
|---------|-------------|-------------|
| CloudTrail | Activity logging | API call history |
| Config | Configuration tracking | Resource compliance |
| Audit Manager | Compliance reporting | Audit-ready reports |
| Organizations | Account governance | SCPs, OUs |
| Systems Manager | Operations management | Patching, inventory |

## 🎯 Exam Tips

- **CloudTrail** = records API calls (who did what, when)
- **Config** = tracks resource configurations and compliance
- **CloudTrail** stores 90 days free; use trails for longer storage
- **Config Rules** evaluate if resources are compliant
- **Audit Manager** generates compliance reports for auditors
- **SCPs** in Organizations restrict what accounts can do
- Know that CloudTrail and Config are different:
  - CloudTrail = activity (API calls)
  - Config = state (configuration)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| CloudTrail | API activity logging service |
| Trail | Long-term CloudTrail storage configuration |
| AWS Config | Resource configuration tracking service |
| Config Rule | Compliance evaluation for resources |
| Audit Manager | Compliance audit automation service |
| SCP | Service Control Policy (Organizations) |
| Conformance Pack | Collection of Config rules |

## 💡 Key Takeaways

1. CloudTrail records all API calls and can store logs in S3
2. AWS Config tracks resource configurations and evaluates compliance
3. Config Rules check if resources meet compliance requirements
4. Audit Manager automates compliance evidence collection and reporting
5. Organizations SCPs provide preventive guardrails across accounts
6. CloudTrail = activity logging; Config = configuration tracking

---

*Next: [Lesson 07 - AWS Access Management](../../lesson-07-aws-access-management/01-aws-iam-overview/readme.md)*

# 📝 Infrastructure as Code (IaC)

## File Structure

```
lesson-09-deploying-and-operating-in-aws/
└── 02-infrastructure-as-code/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Infrastructure as Code (IaC) is the practice of managing and provisioning infrastructure through machine-readable definition files rather than manual processes. AWS provides several IaC tools that enable consistent, repeatable, and automated infrastructure deployment.

## What is Infrastructure as Code?

```
+------------------------------------------------------------------+
|                  INFRASTRUCTURE AS CODE                           |
+------------------------------------------------------------------+
|                                                                   |
|   TRADITIONAL                          IaC APPROACH               |
|   +------------------+                 +------------------+       |
|   |  Manual Setup    |                 |  Code Template   |       |
|   |  - Click console |                 |  - YAML/JSON     |       |
|   |  - Run commands  |                 |  - Version ctrl  |       |
|   |  - Document steps|                 |  - Automated     |       |
|   +------------------+                 +------------------+       |
|          |                                    |                   |
|          v                                    v                   |
|   +------------------+                 +------------------+       |
|   |  Inconsistent    |                 |  Consistent      |       |
|   |  Error-prone     |                 |  Repeatable      |       |
|   |  Hard to repeat  |                 |  Auditable       |       |
|   +------------------+                 +------------------+       |
|                                                                   |
+------------------------------------------------------------------+
```

## Benefits of Infrastructure as Code

| Benefit | Description |
|---------|-------------|
| Consistency | Same result every deployment |
| Repeatability | Deploy identical environments |
| Version control | Track changes, rollback |
| Automation | Reduce manual effort |
| Speed | Faster deployments |
| Documentation | Code is the documentation |
| Cost savings | Reduce human error |

## AWS CloudFormation

The primary AWS IaC service for provisioning resources.

| Feature | Description |
|---------|-------------|
| Template format | JSON or YAML |
| Stacks | Collection of resources |
| Change sets | Preview changes before applying |
| Drift detection | Detect manual changes |
| Rollback | Automatic on failure |
| Cross-region | StackSets for multi-region |

### CloudFormation Concepts

| Concept | Description |
|---------|-------------|
| Template | Blueprint describing resources |
| Stack | Deployed instance of a template |
| Stack Set | Stacks across accounts/regions |
| Change Set | Preview of proposed changes |
| Drift | Differences from template |

### CloudFormation Template Structure

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Example template

Parameters:
  # Input parameters

Resources:
  # AWS resources to create

Outputs:
  # Values to return
```

## AWS Cloud Development Kit (CDK)

Define infrastructure using familiar programming languages.

| Feature | Description |
|---------|-------------|
| Languages | TypeScript, Python, Java, C#, Go |
| Constructs | Reusable cloud components |
| Synthesis | Generates CloudFormation |
| Testing | Unit test infrastructure |
| IDE support | Code completion, type checking |

### CDK vs CloudFormation

| Aspect | CDK | CloudFormation |
|--------|-----|----------------|
| Language | Programming languages | YAML/JSON |
| Abstraction | Higher-level constructs | Resource-level |
| Learning curve | Developers: easier | Ops: easier |
| Output | Generates CF templates | Native |

## AWS SAM (Serverless Application Model)

Simplified IaC for serverless applications.

| Feature | Description |
|---------|-------------|
| Focus | Lambda, API Gateway, DynamoDB |
| Template | Extension of CloudFormation |
| CLI | Local testing and deployment |
| Transform | SAM macro for simplification |

## Terraform on AWS

Third-party IaC tool with multi-cloud support.

| Feature | Description |
|---------|-------------|
| Provider | AWS provider available |
| Language | HCL (HashiCorp Configuration Language) |
| State | Tracks resource state |
| Multi-cloud | Same tool for multiple clouds |

## IaC Tools Comparison

| Tool | Best For | Language |
|------|----------|----------|
| CloudFormation | AWS-native IaC | YAML/JSON |
| CDK | Developers, complex logic | Programming languages |
| SAM | Serverless applications | YAML |
| Terraform | Multi-cloud | HCL |

## CloudFormation Stack Lifecycle

```
+------------------------------------------------------------------+
|                CLOUDFORMATION STACK LIFECYCLE                     |
+------------------------------------------------------------------+
|                                                                   |
|   CREATE              UPDATE              DELETE                  |
|   +--------+         +--------+         +--------+               |
|   |Template| ------> |Change  | ------> |Delete  |               |
|   |Upload  |         |Set     |         |Stack   |               |
|   +--------+         +--------+         +--------+               |
|       |                  |                  |                     |
|       v                  v                  v                     |
|   +--------+         +--------+         +--------+               |
|   |Create  |         |Execute |         |Remove  |               |
|   |Stack   |         |Changes |         |Resources               |
|   +--------+         +--------+         +--------+               |
|       |                  |                  |                     |
|       v                  v                  v                     |
|   +--------+         +--------+         +--------+               |
|   |Resources|        |Updated |         |Stack   |               |
|   |Deployed|         |Stack   |         |Deleted |               |
|   +--------+         +--------+         +--------+               |
|                                                                   |
+------------------------------------------------------------------+
```

## IaC Best Practices

| Practice | Description |
|----------|-------------|
| Version control | Store templates in Git |
| Modular design | Create reusable components |
| Parameter usage | Make templates flexible |
| Nested stacks | Organize complex deployments |
| Change sets | Preview before updating |
| Drift detection | Check for manual changes |

## When to Use Each Tool

| Scenario | Recommended Tool |
|----------|------------------|
| AWS-only, ops team | CloudFormation |
| Complex logic, developers | CDK |
| Serverless apps | SAM |
| Multi-cloud | Terraform |
| Quick prototyping | Console (then convert to IaC) |

## 🎯 Exam Tips

- **CloudFormation** = AWS-native IaC, uses JSON/YAML templates
- **CDK** = write infrastructure in programming languages
- **SAM** = simplified IaC for serverless applications
- **Terraform** = multi-cloud IaC (third-party)
- **Stacks** = collection of AWS resources from a template
- **Change sets** = preview changes before applying
- **Drift detection** = find manual changes to stack resources
- IaC enables **consistency** and **repeatability**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| IaC | Infrastructure as Code |
| CloudFormation | AWS IaC service |
| Template | Blueprint for resources |
| Stack | Deployed template resources |
| CDK | Cloud Development Kit |
| SAM | Serverless Application Model |
| Drift | Changes outside of template |

## 💡 Key Takeaways

1. IaC enables consistent, repeatable infrastructure deployments
2. CloudFormation is AWS's native IaC service using YAML/JSON
3. CDK allows infrastructure definition in programming languages
4. SAM simplifies serverless application deployment
5. Templates can be version-controlled like application code
6. Change sets allow previewing changes before applying
7. Drift detection identifies manual changes to resources

---

*Next: [03 - Cloud Deployment Models](../03-cloud-deployment-models/readme.md)*

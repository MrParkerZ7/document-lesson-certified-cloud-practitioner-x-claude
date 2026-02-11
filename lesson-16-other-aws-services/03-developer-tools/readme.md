# 💻 AWS Developer Tools

## Introduction

AWS provides a comprehensive suite of developer tools that enable teams to build, test, deploy, and monitor applications in the cloud. These services support DevOps practices including continuous integration (CI), continuous delivery (CD), and infrastructure as code. Understanding these tools is essential for the AWS Cloud Practitioner exam as they represent how modern applications are developed and deployed on AWS.

## DevOps and CI/CD Overview

```
+------------------------------------------------------------------+
|                    CONTINUOUS INTEGRATION / DELIVERY              |
+------------------------------------------------------------------+
|                                                                   |
|   TRADITIONAL DEVELOPMENT          CI/CD PIPELINE                 |
|   ┌─────────────────────────┐     ┌─────────────────────────┐     |
|   │                         │     │                         │     |
|   │  Code ──▶ Test ──▶ Deploy    │  Code ──▶ Build ──▶ Test │     |
|   │  (Manual)   (Manual)         │    │                     │     |
|   │                         │     │    ▼                     │     |
|   │  Problems:              │     │  Deploy ──▶ Release     │     |
|   │  • Slow releases        │     │  (Automated Pipeline)   │     |
|   │  • Error-prone          │     │                         │     |
|   │  • Inconsistent         │     │  Benefits:              │     |
|   │                         │     │  • Fast releases        │     |
|   │                         │     │  • Consistent           │     |
|   │                         │     │  • Automated testing    │     |
|   └─────────────────────────┘     └─────────────────────────┘     |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Developer Tools Ecosystem

```
+------------------------------------------------------------------+
|                   AWS DEVELOPER TOOLS ECOSYSTEM                   |
+------------------------------------------------------------------+
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                    AWS CodePipeline                          │ |
|   │              (Orchestrates the entire CI/CD)                 │ |
|   └─────────────────────────────────────────────────────────────┘ |
|        │               │                │                         |
|        ▼               ▼                ▼                         |
|   ┌─────────┐    ┌─────────┐     ┌─────────────┐                  |
|   │CodeCommit│──▶│CodeBuild│──▶  │ CodeDeploy  │                  |
|   │ (Source) │   │ (Build) │     │  (Deploy)   │                  |
|   └─────────┘    └─────────┘     └─────────────┘                  |
|                                                                   |
|   ┌─────────┐    ┌─────────┐     ┌─────────────┐                  |
|   │ Cloud9  │    │ X-Ray   │     │ CodeArtifact│                  |
|   │  (IDE)  │    │(Tracing)│     │ (Packages)  │                  |
|   └─────────┘    └─────────┘     └─────────────┘                  |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS CodeCommit

AWS CodeCommit is a fully managed source control service that hosts secure Git-based repositories.

```
+------------------------------------------------------------------+
|                       AWS CODECOMMIT                              |
+------------------------------------------------------------------+
|                                                                   |
|   DEVELOPERS                     CODECOMMIT REPOSITORY            |
|   ┌─────────┐                   ┌─────────────────────────┐       |
|   │  Dev 1  │ ──▶ push         │                         │       |
|   └─────────┘                   │    ┌─────────────────┐  │       |
|   ┌─────────┐                   │    │   main branch   │  │       |
|   │  Dev 2  │ ──▶ push/pull    │    └─────────────────┘  │       |
|   └─────────┘                   │    ┌─────────────────┐  │       |
|   ┌─────────┐                   │    │ feature branch  │  │       |
|   │  Dev 3  │ ◀── pull         │    └─────────────────┘  │       |
|   └─────────┘                   │                         │       |
|                                 │  • Unlimited repos      │       |
|   Features:                     │  • Automatic encryption │       |
|   • Git commands                │  • IAM integration      │       |
|   • Pull requests               │  • Trigger support      │       |
|   • Code review                 └─────────────────────────┘       |
|                                                                   |
+------------------------------------------------------------------+
```

### CodeCommit Features

| Feature | Description |
|---------|-------------|
| Git-Based | Standard Git commands and workflows |
| Encryption | Automatic encryption at rest and in transit |
| Unlimited Repos | No limit on number of repositories |
| Large Files | Support for large files with Git LFS |
| Pull Requests | Code review workflows |
| Triggers | Integrate with Lambda, SNS, CodePipeline |
| Access Control | IAM policies and repository policies |

### CodeCommit vs GitHub/GitLab

| Feature | CodeCommit | GitHub/GitLab |
|---------|------------|---------------|
| Hosting | AWS managed | Cloud or self-hosted |
| IAM Integration | Native | Requires setup |
| Pricing | Pay per user | Per user subscription |
| Ecosystem | AWS services | Broader community |
| Features | Basic Git | Advanced (CI/CD built-in) |

## AWS CodeBuild

AWS CodeBuild is a fully managed build service that compiles source code, runs tests, and produces software packages.

```
+------------------------------------------------------------------+
|                       AWS CODEBUILD                               |
+------------------------------------------------------------------+
|                                                                   |
|   SOURCE                 BUILD                      OUTPUT        |
|   ┌─────────┐           ┌─────────────────────┐   ┌─────────┐    |
|   │CodeCommit│          │                     │   │   S3    │    |
|   │ GitHub  │  ──▶      │   Build Container   │──▶│ Bucket  │    |
|   │ S3      │           │   ┌─────────────┐   │   │         │    |
|   │Bitbucket│           │   │ buildspec.yml   │   │ ECR     │    |
|   └─────────┘           │   │             │   │   │ Image   │    |
|                         │   │ • Install   │   │   │         │    |
|                         │   │ • Pre-build │   │   │Artifacts│    |
|                         │   │ • Build     │   │   └─────────┘    |
|                         │   │ • Post-build│   │                  |
|                         │   └─────────────┘   │                  |
|                         │                     │                  |
|                         └─────────────────────┘                  |
|                                                                   |
|   Supported: Java, Python, Node.js, Ruby, Go, .NET, Docker, etc. |
|                                                                   |
+------------------------------------------------------------------+
```

### CodeBuild Features

| Feature | Description |
|---------|-------------|
| Build Environments | Pre-configured or custom Docker images |
| buildspec.yml | Build commands and settings file |
| Scalable | Automatically scales to handle multiple builds |
| Pay Per Use | Pay only for build minutes used |
| Caching | S3 and local caching for faster builds |
| VPC Support | Run builds in your VPC for private resources |
| Reports | Test reports, code coverage reports |

### buildspec.yml Phases

| Phase | Description |
|-------|-------------|
| install | Install build dependencies |
| pre_build | Commands before build (login to ECR, etc.) |
| build | Main build commands |
| post_build | Commands after build (notifications, etc.) |

## AWS CodeDeploy

AWS CodeDeploy is a fully managed deployment service that automates software deployments to various compute services.

```
+------------------------------------------------------------------+
|                       AWS CODEDEPLOY                              |
+------------------------------------------------------------------+
|                                                                   |
|   DEPLOYMENT SOURCE          CODEDEPLOY          COMPUTE TARGETS  |
|   ┌─────────────┐           ┌─────────┐        ┌─────────────┐    |
|   │     S3     │           │         │        │    EC2      │    |
|   │   Bucket   │  ──▶      │ Deploy- │  ──▶   │  Instances  │    |
|   └─────────────┘           │  ment   │        └─────────────┘    |
|   ┌─────────────┐           │  Group  │        ┌─────────────┐    |
|   │   GitHub   │  ──▶      │         │  ──▶   │   Lambda    │    |
|   │            │           │         │        │  Functions  │    |
|   └─────────────┘           └─────────┘        └─────────────┘    |
|                                  │             ┌─────────────┐    |
|                                  └──────────▶  │     ECS     │    |
|   appspec.yml defines                          │   Services  │    |
|   deployment actions                           └─────────────┘    |
|                                                                   |
+------------------------------------------------------------------+
```

### CodeDeploy Deployment Types

| Type | Description | Use Case |
|------|-------------|----------|
| **In-Place** | Update instances one at a time | EC2, on-premises |
| **Blue/Green** | Deploy to new environment, then switch | EC2, ECS, Lambda |
| **Canary** | Deploy to small % first, then rest | Lambda, ECS |
| **Linear** | Deploy in equal increments | Lambda, ECS |

### CodeDeploy Deployment Configurations

| Configuration | Description |
|---------------|-------------|
| AllAtOnce | Deploy to all instances simultaneously |
| HalfAtATime | Deploy to half, then the other half |
| OneAtATime | Deploy to one instance at a time |
| Custom | Define your own percentage/count |

### CodeDeploy Features

| Feature | Description |
|---------|-------------|
| appspec.yml | Deployment specification file |
| Hooks | Scripts at various deployment stages |
| Rollback | Automatic rollback on failure |
| Health Checks | Verify deployment success |
| Deployment Groups | Target sets of instances |

## AWS CodePipeline

AWS CodePipeline is a fully managed continuous delivery service that automates release pipelines for fast and reliable updates.

```
+------------------------------------------------------------------+
|                      AWS CODEPIPELINE                             |
+------------------------------------------------------------------+
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                      PIPELINE STAGES                         │ |
|   │                                                              │ |
|   │  SOURCE          BUILD           TEST           DEPLOY       │ |
|   │  ┌──────┐       ┌──────┐       ┌──────┐       ┌──────┐      │ |
|   │  │Code- │  ──▶  │Code- │  ──▶  │Code- │  ──▶  │Code- │      │ |
|   │  │Commit│       │Build │       │Build │       │Deploy│      │ |
|   │  │GitHub│       │      │       │Tests │       │ECS   │      │ |
|   │  │S3    │       │      │       │      │       │Lambda│      │ |
|   │  └──────┘       └──────┘       └──────┘       └──────┘      │ |
|   │                                                              │ |
|   │  ┌─────────────────────────────────────────────────────────┐ │ |
|   │  │          Optional: Manual Approval Stage                │ │ |
|   │  └─────────────────────────────────────────────────────────┘ │ |
|   │                                                              │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
|   Integrates: Jenkins, GitHub Actions, CloudFormation, and more  |
|                                                                   |
+------------------------------------------------------------------+
```

### CodePipeline Features

| Feature | Description |
|---------|-------------|
| Visual Editor | Drag-and-drop pipeline creation |
| Stages | Logical grouping of actions |
| Actions | Tasks within stages (source, build, deploy) |
| Parallel Actions | Run actions simultaneously |
| Manual Approval | Human approval gates |
| Artifact Store | S3 bucket for pipeline artifacts |
| Cross-Account | Deploy to multiple AWS accounts |
| Cross-Region | Deploy to multiple regions |

### CodePipeline Action Providers

| Stage | Action Providers |
|-------|-----------------|
| Source | CodeCommit, GitHub, S3, Bitbucket, ECR |
| Build | CodeBuild, Jenkins, TeamCity |
| Test | CodeBuild, Device Farm, Jenkins |
| Deploy | CodeDeploy, CloudFormation, ECS, S3, Lambda |
| Approval | Manual approval, SNS notification |

## AWS Cloud9

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug code with just a browser.

```
+------------------------------------------------------------------+
|                        AWS CLOUD9                                 |
+------------------------------------------------------------------+
|                                                                   |
|   WEB BROWSER                                                     |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                    Cloud9 IDE                                │ |
|   │  ┌─────────────────────────────────────────────────────────┐│ |
|   │  │ File Browser │        Code Editor                       ││ |
|   │  │  ┌──────────┐│  ┌───────────────────────────────────────┐││ |
|   │  │  │ /project ││  │ const AWS = require('aws-sdk');       │││ |
|   │  │  │  ├─ src  ││  │ const s3 = new AWS.S3();              │││ |
|   │  │  │  ├─ test ││  │ // Your code here                     │││ |
|   │  │  │  └─ pkg  ││  │                                       │││ |
|   │  │  └──────────┘│  └───────────────────────────────────────┘││ |
|   │  │              │  ┌───────────────────────────────────────┐││ |
|   │  │              │  │ $ Terminal (Bash)                     │││ |
|   │  │              │  │ > npm install                         │││ |
|   │  │              │  │ > sam local invoke                    │││ |
|   │  │              │  └───────────────────────────────────────┘││ |
|   │  └─────────────────────────────────────────────────────────┘│ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
|   Features: Code editor, terminal, debugger, pair programming     |
|                                                                   |
+------------------------------------------------------------------+
```

### Cloud9 Features

| Feature | Description |
|---------|-------------|
| Browser-Based | No local installation required |
| Pre-configured | AWS CLI, SAM CLI pre-installed |
| Terminal | Full Linux terminal |
| Debugging | Built-in debugger |
| Pair Programming | Real-time collaboration |
| AWS Integration | Direct access to AWS services |
| Language Support | 40+ programming languages |

### Cloud9 Environment Types

| Type | Description | Use Case |
|------|-------------|----------|
| EC2 | Managed EC2 instance | Standard development |
| SSH | Connect to existing server | On-premises, hybrid |

## AWS X-Ray

AWS X-Ray helps developers analyze and debug distributed applications by tracing requests through the system.

```
+------------------------------------------------------------------+
|                         AWS X-RAY                                 |
+------------------------------------------------------------------+
|                                                                   |
|   DISTRIBUTED APPLICATION TRACING                                 |
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                    Request Flow                              │ |
|   │                                                              │ |
|   │  Client ──▶ API GW ──▶ Lambda ──▶ DynamoDB                   │ |
|   │     │         │          │           │                       │ |
|   │     └─────────┴──────────┴───────────┘                       │ |
|   │              │                                               │ |
|   │              ▼ X-Ray Trace                                   │ |
|   │     ┌─────────────────────────────────────────────────┐     │ |
|   │     │ Trace ID: 1-abc123                               │     │ |
|   │     │ ├─ API Gateway: 5ms                              │     │ |
|   │     │ │  └─ Lambda: 100ms                              │     │ |
|   │     │ │     ├─ DynamoDB Query: 20ms                    │     │ |
|   │     │ │     └─ DynamoDB Put: 15ms                      │     │ |
|   │     │ Total: 140ms                                     │     │ |
|   │     └─────────────────────────────────────────────────┘     │ |
|   │                                                              │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

### X-Ray Features

| Feature | Description |
|---------|-------------|
| Service Map | Visual representation of application architecture |
| Traces | End-to-end request tracking |
| Segments | Data about work done by services |
| Subsegments | Detailed information within segments |
| Annotations | Key-value pairs for filtering |
| Metadata | Additional data for debugging |
| Sampling | Control volume of traces collected |

### X-Ray Integrations

| Service | Integration |
|---------|-------------|
| Lambda | Automatic tracing |
| API Gateway | Tracing header propagation |
| EC2 | X-Ray daemon |
| ECS/EKS | X-Ray daemon container |
| Elastic Beanstalk | Built-in X-Ray support |

## Developer Tools Comparison

| Service | Purpose | Key Feature |
|---------|---------|-------------|
| CodeCommit | Source control | Git repositories |
| CodeBuild | Build | Compile and test |
| CodeDeploy | Deployment | Deploy to compute |
| CodePipeline | CI/CD orchestration | Automate pipeline |
| Cloud9 | IDE | Browser-based development |
| X-Ray | Debugging | Distributed tracing |

## Complete CI/CD Pipeline Example

```
+------------------------------------------------------------------+
|                    COMPLETE CI/CD PIPELINE                        |
+------------------------------------------------------------------+
|                                                                   |
|   1. Developer pushes code to CodeCommit                          |
|   2. CodePipeline detects change, triggers pipeline               |
|   3. CodeBuild compiles code, runs unit tests                     |
|   4. CodeBuild creates Docker image, pushes to ECR                |
|   5. Manual approval for production deployment                    |
|   6. CodeDeploy deploys to ECS cluster                            |
|   7. X-Ray traces requests through application                    |
|                                                                   |
|   ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐ |
|   │Code │──▶│Build│──▶│Test │──▶│Approve──▶│Deploy──▶│Monitor │ |
|   │Push │   │     │   │     │   │     │   │     │   │(X-Ray)│ |
|   └─────┘    └─────┘    └─────┘    └─────┘    └─────┘    └─────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **CodeCommit** = Git repository service (like GitHub but AWS-managed)
- **CodeBuild** = Build and test code (compiles, creates artifacts)
- **CodeDeploy** = Deploy applications to EC2, Lambda, ECS
- **CodePipeline** = Orchestrates entire CI/CD pipeline
- **Cloud9** = Browser-based IDE (no local installation needed)
- **X-Ray** = Trace and debug distributed applications
- **CodePipeline** integrates with all other Code services plus third-party tools
- **buildspec.yml** = CodeBuild configuration; **appspec.yml** = CodeDeploy configuration
- CodeDeploy supports **In-Place** and **Blue/Green** deployments
- X-Ray creates a **service map** showing application architecture
- All Code services are **fully managed** with pay-as-you-go pricing
- Remember the flow: **Source → Build → Test → Deploy** (CodePipeline orchestrates)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| CI/CD | Continuous Integration / Continuous Delivery - automated build and deploy |
| Pipeline | Automated workflow for releasing software |
| Build | Process of compiling code and creating deployable artifacts |
| Artifact | Output of a build process (JAR, ZIP, Docker image) |
| Deployment | Process of releasing code to production environments |
| Blue/Green | Deployment strategy using two identical environments |
| Rollback | Reverting to a previous version after failed deployment |
| Trace | Record of a request as it travels through services |
| Service Map | Visual diagram of application architecture and dependencies |
| IDE | Integrated Development Environment |

## 💡 Key Takeaways

1. AWS CodeCommit is a fully managed Git repository service
2. AWS CodeBuild compiles code, runs tests, and produces deployable artifacts
3. AWS CodeDeploy automates deployments to EC2, Lambda, and ECS
4. AWS CodePipeline orchestrates the entire CI/CD pipeline
5. CodePipeline integrates with CodeCommit, CodeBuild, and CodeDeploy
6. AWS Cloud9 is a browser-based IDE with AWS tools pre-installed
7. AWS X-Ray traces requests through distributed applications
8. X-Ray provides service maps and performance insights
9. buildspec.yml configures CodeBuild; appspec.yml configures CodeDeploy
10. All developer tools are fully managed with no servers to maintain
11. These tools enable DevOps practices and automated software delivery

---

[Previous: 02 - Business Applications](../02-business-applications/readme.md) | [Next: 04 - End User Computing](../04-end-user-computing/readme.md)

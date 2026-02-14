# 🔄 One-Time vs Repeatable Processes

## File Structure

```
lesson-09-deploying-and-operating-in-aws/
└── 04-one-time-vs-repeatable-processes/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Understanding the difference between one-time and repeatable processes is crucial for effective cloud operations. AWS provides tools and services that help automate and standardize processes, reducing manual effort and ensuring consistency across deployments.

## Understanding the Difference

```
+------------------------------------------------------------------+
|          ONE-TIME VS REPEATABLE PROCESSES                         |
+------------------------------------------------------------------+
|                                                                   |
|   ONE-TIME (Manual)                 REPEATABLE (Automated)        |
|   +----------------------+          +----------------------+      |
|   | • Click through      |          | • Infrastructure     |      |
|   |   console            |          |   as Code            |      |
|   | • Run commands       |          | • CI/CD pipelines    |      |
|   |   manually           |          | • Auto Scaling       |      |
|   | • Document steps     |          | • Templates          |      |
|   | • Hard to reproduce  |          | • Easy to reproduce  |      |
|   +----------------------+          +----------------------+      |
|                                                                   |
|   Use for:                          Use for:                      |
|   • Initial exploration             • Production deployments      |
|   • Quick prototypes                • Multiple environments       |
|   • Learning                        • Disaster recovery           |
|                                                                   |
+------------------------------------------------------------------+
```

## One-Time Processes

Actions performed manually, typically once.

| Characteristic | Description |
|----------------|-------------|
| Manual | Requires human intervention |
| Ad-hoc | Done as needed |
| Undocumented | Often not captured formally |
| Variable | Results may differ each time |
| Time-consuming | Slow to reproduce |

### When One-Time is Appropriate

| Scenario | Example |
|----------|---------|
| Initial setup | First-time account configuration |
| Exploration | Learning a new service |
| Prototyping | Testing an idea quickly |
| Emergency fixes | Urgent production issues |
| Unique tasks | One-off data migrations |

## Repeatable Processes

Automated, consistent processes that can be executed multiple times.

| Characteristic | Description |
|----------------|-------------|
| Automated | Minimal human intervention |
| Consistent | Same result every time |
| Documented | Code is documentation |
| Version controlled | Track changes over time |
| Fast | Quick to execute |

### AWS Tools for Repeatable Processes

| Tool | Use Case |
|------|----------|
| CloudFormation | Infrastructure deployment |
| CDK | Infrastructure as code |
| CodePipeline | CI/CD automation |
| Lambda | Event-driven automation |
| Systems Manager | Operational automation |
| EventBridge | Event-driven workflows |
| Step Functions | Workflow orchestration |

## Converting One-Time to Repeatable

```
+------------------------------------------------------------------+
|            FROM MANUAL TO AUTOMATED                               |
+------------------------------------------------------------------+
|                                                                   |
|   Step 1           Step 2           Step 3           Step 4      |
|   +--------+       +--------+       +--------+       +--------+  |
|   | Manual |  -->  | Document|  --> | Script |  -->  | Automate| |
|   | Process|       | Steps   |      | It     |       | It      | |
|   +--------+       +--------+       +--------+       +--------+  |
|                                                                   |
|   Click            Write down       Create           Deploy via  |
|   console          procedures       IaC/scripts      CI/CD       |
|                                                                   |
+------------------------------------------------------------------+
```

## Infrastructure as Code (IaC)

Converts manual infrastructure setup to repeatable deployments.

| Manual (One-Time) | IaC (Repeatable) |
|-------------------|------------------|
| Click "Create VPC" | CloudFormation template |
| Configure settings | Parameters in code |
| Launch EC2 manually | Auto-created resources |
| Document after | Code is documentation |

## CI/CD Pipelines

Automate software deployment processes.

| Component | Description |
|-----------|-------------|
| Source | Code repository (CodeCommit, GitHub) |
| Build | Compile and package (CodeBuild) |
| Test | Automated testing |
| Deploy | Deploy to environments (CodeDeploy) |

### AWS CI/CD Services

| Service | Purpose |
|---------|---------|
| CodeCommit | Source code repository |
| CodeBuild | Build and test code |
| CodeDeploy | Deploy applications |
| CodePipeline | Orchestrate CI/CD |

## Auto Scaling

Automates capacity management.

| Manual | Auto Scaling |
|--------|--------------|
| Monitor manually | CloudWatch alarms |
| Launch instances | Auto launch/terminate |
| Estimate capacity | Scale based on demand |
| Reactive response | Proactive scaling |

## Automation Benefits

| Benefit | Description |
|---------|-------------|
| Consistency | Same result every time |
| Speed | Faster deployments |
| Reliability | Fewer human errors |
| Scalability | Handle growth easily |
| Auditability | Track all changes |
| Cost savings | Reduce manual effort |

## AWS Systems Manager Automation

Automate operational tasks.

| Feature | Description |
|---------|-------------|
| Runbooks | Pre-defined automation |
| Run Command | Execute commands at scale |
| Patch Manager | Automated patching |
| State Manager | Maintain configuration state |
| Automation | Multi-step workflows |

## Event-Driven Automation

```
+------------------------------------------------------------------+
|                EVENT-DRIVEN AUTOMATION                            |
+------------------------------------------------------------------+
|                                                                   |
|   Event Source          EventBridge         Target Action         |
|   +-----------+        +-----------+        +-----------+         |
|   | S3 Upload | -----> | Event     | -----> | Lambda    |         |
|   | EC2 Change|        | Rules     |        | SNS       |         |
|   | Schedule  |        | Patterns  |        | Step Func |         |
|   +-----------+        +-----------+        +-----------+         |
|                                                                   |
+------------------------------------------------------------------+
```

## Operational Best Practices

| Practice | Description |
|----------|-------------|
| Automate everything | If done twice, automate it |
| Use version control | Track all changes |
| Test automation | Validate before production |
| Document processes | Even automated ones |
| Monitor and alert | Know when things fail |
| Review regularly | Improve over time |

## Comparison Table

| Aspect | One-Time | Repeatable |
|--------|----------|------------|
| Effort | High each time | High initially, low ongoing |
| Consistency | Low | High |
| Speed | Slow | Fast |
| Errors | More likely | Less likely |
| Documentation | Manual | Automatic (code) |
| Scalability | Limited | High |
| Auditability | Difficult | Easy |

## 🎯 Exam Tips

- **Repeatable processes** = automated, consistent, documented
- **CloudFormation** = repeatable infrastructure deployment
- **CI/CD** = repeatable application deployment
- **Auto Scaling** = automated capacity management
- **Systems Manager** = operational automation
- One-time is OK for **prototyping** and **learning**
- Production should use **repeatable processes**
- **Infrastructure as Code** converts manual to repeatable

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| One-Time Process | Manual, ad-hoc procedure |
| Repeatable Process | Automated, consistent procedure |
| CI/CD | Continuous Integration/Continuous Deployment |
| Automation | Reducing manual intervention |
| Runbook | Documented procedures for operations |
| Event-Driven | Actions triggered by events |

## 💡 Key Takeaways

1. One-time processes are manual and difficult to reproduce consistently
2. Repeatable processes are automated, documented, and consistent
3. Use one-time for prototyping, repeatable for production
4. CloudFormation enables repeatable infrastructure deployment
5. CI/CD pipelines automate application deployment
6. Auto Scaling automates capacity management
7. Converting to repeatable processes reduces errors and increases speed

---

*Next: [Lesson 10 - AWS Global Infrastructure](../../lesson-10-aws-global-infrastructure/01-aws-regions-and-availability-zones/readme.md)*

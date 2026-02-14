# ✅ Reliability Pillar

## File Structure

```
lesson-02-aws-well-architected-framework/
└── 04-reliability-pillar/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Overview

The **Reliability** pillar focuses on ensuring a workload performs its intended function correctly and consistently when it's expected to. This includes the ability to operate and test the workload through its total lifecycle, recover from failures, and meet demand.

## Definition

> Reliability is the ability of a workload to perform its intended function correctly and consistently when it's expected to. This includes the ability to operate and test the workload through its total lifecycle.

## Design Principles

| Principle | Description |
|-----------|-------------|
| **Automatically recover from failure** | Monitor and automatically trigger recovery |
| **Test recovery procedures** | Test how your workload fails and validate procedures |
| **Scale horizontally** | Replace one large resource with multiple small ones |
| **Stop guessing capacity** | Use auto-scaling to meet demand |
| **Manage change in automation** | Use automation for infrastructure changes |

## Key Focus Areas

```
┌─────────────────────────────────────────────────────────────────────┐
│                       Reliability Pillar                             │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐ │
│   │   Foundations   │    │ Workload Arch   │    │ Change Mgmt     │ │
│   │                 │    │                 │    │                 │ │
│   │ • Service Quotas│    │ • Service Arch  │    │ • Monitor       │ │
│   │ • Network Design│    │ • Distributed   │    │ • Automation    │ │
│   │ • Account Limits│    │   Systems       │    │ • Testing       │ │
│   └─────────────────┘    └─────────────────┘    └─────────────────┘ │
│                                                                      │
│   ┌───────────────────────────────────────────────────────────────┐ │
│   │                    Failure Management                          │ │
│   │                                                                │ │
│   │  • Backup & Restore  •  High Availability  •  Disaster Recovery│ │
│   └───────────────────────────────────────────────────────────────┘ │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

## Best Practices

### 1. Foundations
- Understand **service quotas** (formerly called limits)
- Design proper **network topology**
- Plan for **account structure**

### 2. Workload Architecture
- Design for **distributed systems**
- Implement **loose coupling**
- Use **service-oriented architecture**

### 3. Change Management
- Monitor resources and changes
- Use **automation** for changes
- Implement proper **testing** strategies

### 4. Failure Management
- **Backup data** regularly
- Design for **fault isolation**
- Implement **disaster recovery** strategies

## Fault Tolerance vs High Availability

| Concept | Definition | Example |
|---------|------------|---------|
| **High Availability** | System remains operational | Multi-AZ deployment |
| **Fault Tolerance** | System continues without degradation | Active-active clusters |
| **Disaster Recovery** | Recover from major events | Multi-region backup |

## AWS Services for Reliability

| Category | Services |
|----------|----------|
| **Compute** | Auto Scaling, EC2 Auto Recovery |
| **Database** | RDS Multi-AZ, Aurora, DynamoDB Global Tables |
| **Storage** | S3 (11 9's durability), EBS snapshots |
| **Networking** | Route 53, Elastic Load Balancing, Global Accelerator |
| **Monitoring** | CloudWatch, Health Dashboard |
| **Backup** | AWS Backup, S3 Glacier |

## Recovery Strategies

```
                     RPO                        RTO
          (Recovery Point Objective)    (Recovery Time Objective)
                    │                           │
    ◄───────────────┼───────────────────────────┼───────────────►
                    │                           │
              Last Backup                   Recovery
                Point                       Complete
                    │                           │
    ────────────────┼───────────────────────────┼────────────────
                    │         Disaster          │
                    │◄─────────────────────────►│
                    │       Data Loss &         │
                    │       Downtime            │


    Strategy               RPO          RTO         Cost
    ─────────────────────────────────────────────────────────
    Backup & Restore       Hours        24+ hrs     $
    Pilot Light            Minutes      Hours       $$
    Warm Standby           Minutes      Minutes     $$$
    Multi-Site Active      Near Zero    Near Zero   $$$$
```

## Recovery Strategies Explained

| Strategy | Description | Use Case |
|----------|-------------|----------|
| **Backup & Restore** | Restore from backups | Non-critical systems |
| **Pilot Light** | Core components always running | Important systems |
| **Warm Standby** | Scaled-down version running | Business critical |
| **Multi-Site Active** | Full capacity in multiple regions | Mission critical |

## Key Reliability Metrics

- **MTBF** (Mean Time Between Failures) - Average time between failures
- **MTTR** (Mean Time To Recovery) - Average time to recover
- **RPO** (Recovery Point Objective) - Maximum acceptable data loss
- **RTO** (Recovery Time Objective) - Maximum acceptable downtime

## 🎯 Exam Tips

- **Multi-AZ** deployments provide **High Availability**
- **S3** offers 99.999999999% (11 9's) **durability**
- **Auto Scaling** helps handle capacity automatically
- Know the difference between **RPO** and **RTO**
- **Backup** strategies vary by cost and recovery speed
- **Service Quotas** can limit your deployments

## 💡 Key Takeaways

1. **Automate recovery** - Use health checks and auto-recovery
2. **Test failures** - Regular game days and chaos engineering
3. **Scale horizontally** - Prefer many small over few large
4. **Design for failure** - Assume everything can fail
5. **Multiple Availability Zones** - Basic requirement for reliability
6. **Backup everything** - Use AWS Backup for centralized management

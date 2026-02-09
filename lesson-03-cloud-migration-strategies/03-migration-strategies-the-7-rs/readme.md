# Migration Strategies - The 7 R's

## Overview

AWS defines **7 migration strategies** (commonly called the "7 R's") for moving applications to the cloud. Each strategy has different use cases, benefits, and trade-offs. Understanding these strategies is essential for the Cloud Practitioner exam.

## The 7 R's of Migration

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    The 7 R's of Cloud Migration                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Easiest                                               Most Effort     │
│      │                                                        │         │
│      ▼                                                        ▼         │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐    │
│  │Retire  │ │Retain  │ │Rehost  │ │Relocate│ │Replatform│ │Refactor│   │
│  │        │ │        │ │        │ │        │ │         │ │        │    │
│  │Sunset  │ │Keep    │ │Lift &  │ │VM Move │ │Lift,    │ │Re-     │    │
│  │        │ │on-prem │ │Shift   │ │        │ │Tinker,  │ │architect│   │
│  │        │ │        │ │        │ │        │ │Shift    │ │        │    │
│  └────────┘ └────────┘ └────────┘ └────────┘ └─────────┘ └────────┘    │
│                                                                          │
│  ┌────────────────────────────────────────────────────────────────┐     │
│  │                        Repurchase                               │     │
│  │               (Move to a different product - SaaS)              │     │
│  └────────────────────────────────────────────────────────────────┘     │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Detailed Strategy Breakdown

### 1. Retire (Decommission)
**What**: Identify applications that are no longer needed and turn them off.

| Aspect | Details |
|--------|---------|
| **Effort** | Very Low |
| **Use Case** | Redundant, unused, or end-of-life applications |
| **Benefits** | Reduces cost, simplifies portfolio |
| **Example** | Legacy application no longer in use |

### 2. Retain (Revisit)
**What**: Keep some applications on-premises. Not everything needs to move to cloud.

| Aspect | Details |
|--------|---------|
| **Effort** | None (for now) |
| **Use Case** | Recent upgrades, compliance restrictions, not ready for cloud |
| **Benefits** | Defer migration costs, focus on higher-priority apps |
| **Example** | Recently upgraded mainframe, regulatory constraints |

### 3. Rehost (Lift and Shift)
**What**: Move applications to the cloud without changes. Simply "lift" from on-premises and "shift" to cloud.

| Aspect | Details |
|--------|---------|
| **Effort** | Low to Medium |
| **Use Case** | Large-scale migrations, quick wins |
| **Benefits** | Fast migration, minimal changes, immediate cost savings |
| **Tools** | AWS Application Migration Service, VM Import/Export |
| **Example** | Move VMs directly to EC2 |

### 4. Relocate (Hypervisor-Level Lift and Shift)
**What**: Move VMware workloads to VMware Cloud on AWS without changes.

| Aspect | Details |
|--------|---------|
| **Effort** | Low |
| **Use Case** | VMware environments, vSphere workloads |
| **Benefits** | Use familiar tools, quick migration |
| **Tools** | VMware Cloud on AWS |
| **Example** | Move VMware VMs to VMware Cloud on AWS |

### 5. Repurchase (Drop and Shop)
**What**: Move to a different product, typically a SaaS solution.

| Aspect | Details |
|--------|---------|
| **Effort** | Medium |
| **Use Case** | Replace with cloud-native/SaaS solution |
| **Benefits** | Fully managed, modern features |
| **Examples** | CRM → Salesforce, Email → Amazon WorkMail, HR → Workday |

### 6. Replatform (Lift, Tinker, and Shift)
**What**: Make some cloud optimizations during migration without changing core architecture.

| Aspect | Details |
|--------|---------|
| **Effort** | Medium |
| **Use Case** | Leverage managed services with minimal changes |
| **Benefits** | Cloud benefits with limited refactoring |
| **Examples** | Database → RDS, MySQL → Aurora |

### 7. Refactor / Re-architect
**What**: Reimagine how the application is built using cloud-native features.

| Aspect | Details |
|--------|---------|
| **Effort** | High |
| **Use Case** | Need for agility, scalability, or cloud-native features |
| **Benefits** | Maximum cloud benefits, scalability, flexibility |
| **Examples** | Monolith → Microservices, Serverless architecture |

## Strategy Comparison

| Strategy | Effort | Time | Cost | Cloud Benefits |
|----------|--------|------|------|----------------|
| **Retire** | ⭐ | Fast | Save | N/A |
| **Retain** | ⭐ | None | Same | None |
| **Rehost** | ⭐⭐ | Fast | Medium | Basic |
| **Relocate** | ⭐⭐ | Fast | Medium | Basic |
| **Repurchase** | ⭐⭐⭐ | Medium | Variable | High |
| **Replatform** | ⭐⭐⭐ | Medium | Medium | Medium |
| **Refactor** | ⭐⭐⭐⭐⭐ | Slow | High | Maximum |

## Decision Framework

```
┌─────────────────────────────────────────────────────────────────────────┐
│              How to Choose a Migration Strategy                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  Question 1: Is this application still needed?                          │
│              NO  → RETIRE                                               │
│              YES → Continue                                             │
│                                                                          │
│  Question 2: Should it stay on-premises for now?                        │
│              YES → RETAIN                                               │
│              NO  → Continue                                             │
│                                                                          │
│  Question 3: Is there a SaaS alternative you want to use?               │
│              YES → REPURCHASE                                           │
│              NO  → Continue                                             │
│                                                                          │
│  Question 4: Is it a VMware environment?                                │
│              YES → Consider RELOCATE                                    │
│              NO  → Continue                                             │
│                                                                          │
│  Question 5: Do you need cloud-native features/scalability?             │
│              YES → REFACTOR                                             │
│              NO  → Continue                                             │
│                                                                          │
│  Question 6: Can you benefit from managed services with minimal change? │
│              YES → REPLATFORM                                           │
│              NO  → REHOST                                               │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## AWS Migration Tools by Strategy

| Strategy | AWS Tools |
|----------|-----------|
| **Rehost** | AWS Application Migration Service (MGN), VM Import/Export |
| **Relocate** | VMware Cloud on AWS |
| **Replatform** | AWS DMS (Database Migration Service), AWS Schema Conversion Tool |
| **Refactor** | AWS Microservice Extractor, AWS App2Container |

## Exam Tips

- **Remember all 7 R's**: Retire, Retain, Rehost, Relocate, Repurchase, Replatform, Refactor
- **Rehost** = Lift and Shift (most common for quick migrations)
- **Replatform** = Lift, Tinker, and Shift (some optimization)
- **Refactor** = Re-architect (most cloud benefits, most effort)
- **Repurchase** = Move to SaaS (like Salesforce)
- **Retire** and **Retain** reduce scope of migration
- Know the **AWS Application Migration Service** for rehost migrations

## Key Takeaways

1. **7 R's** provide a framework for migration decisions
2. **Rehost** is fastest but provides fewest cloud benefits
3. **Refactor** provides most benefits but requires most effort
4. **Most migrations** use a combination of strategies
5. **Retire** can significantly reduce migration scope
6. Choose strategy based on **business goals**, **timeline**, and **resources**

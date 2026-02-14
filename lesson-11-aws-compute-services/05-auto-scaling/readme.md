# 📈 AWS Auto Scaling

## File Structure

```
lesson-11-aws-compute-services/
└── 05-auto-scaling/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Auto Scaling automatically adjusts the number of compute resources to maintain application performance at the lowest possible cost. It ensures you have the right amount of capacity to handle your application's current demand.

## What is Auto Scaling?

```
+------------------------------------------------------------------+
|                      AUTO SCALING                                 |
+------------------------------------------------------------------+
|                                                                   |
|   Automatically adjusts capacity based on demand                  |
|                                                                   |
|   Low Demand                 Peak Demand                          |
|   +--------+                 +--------+--------+--------+         |
|   |  EC2   |                 |  EC2   |  EC2   |  EC2   |         |
|   | (min)  |    SCALES UP    | (max)  |        |        |         |
|   +--------+   ---------->   +--------+--------+--------+         |
|                                                                   |
|   +--------+--------+--------+                                    |
|   |  EC2   |  EC2   |  EC2   |    SCALES DOWN                     |
|   | (max)  |        |        |   ---------->   +--------+         |
|   +--------+--------+--------+                 |  EC2   |         |
|                                                | (min)  |         |
|                                                +--------+         |
|                                                                   |
+------------------------------------------------------------------+
```

## Auto Scaling Benefits

| Benefit | Description |
|---------|-------------|
| High availability | Automatically replaces unhealthy instances |
| Better cost management | Scale down when demand drops |
| Better performance | Scale up to meet demand |
| Automatic | No manual intervention needed |
| Predictive | Can anticipate traffic patterns |

## EC2 Auto Scaling Components

```
+------------------------------------------------------------------+
|                  EC2 AUTO SCALING COMPONENTS                      |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+                                            |
|   | LAUNCH TEMPLATE  |  What to launch                            |
|   | - AMI            |  (instance configuration)                   |
|   | - Instance type  |                                            |
|   | - Key pair       |                                            |
|   | - Security group |                                            |
|   +------------------+                                            |
|           |                                                       |
|           v                                                       |
|   +------------------+                                            |
|   | AUTO SCALING     |  Where to launch                           |
|   | GROUP (ASG)      |  (VPC, subnets, AZs)                       |
|   | - Min size       |                                            |
|   | - Max size       |  How many to launch                        |
|   | - Desired        |  (capacity limits)                         |
|   +------------------+                                            |
|           |                                                       |
|           v                                                       |
|   +------------------+                                            |
|   | SCALING POLICIES |  When to scale                             |
|   | - Target tracking|  (scaling triggers)                        |
|   | - Step scaling   |                                            |
|   | - Scheduled      |                                            |
|   +------------------+                                            |
|                                                                   |
+------------------------------------------------------------------+
```

## Launch Template vs Launch Configuration

| Feature | Launch Template | Launch Configuration |
|---------|-----------------|---------------------|
| Status | Recommended | Legacy |
| Versioning | Supported | Not supported |
| Flexibility | More features | Limited |
| Instance types | Multiple | Single |
| Spot/On-Demand | Mix supported | Not supported |

## Auto Scaling Group Settings

| Setting | Description |
|---------|-------------|
| Minimum capacity | Minimum number of instances |
| Maximum capacity | Maximum number of instances |
| Desired capacity | Target number of instances |
| Availability Zones | AZs to distribute instances |
| Health checks | EC2 or ELB health checks |

## Scaling Policies

| Policy Type | Description | Use Case |
|-------------|-------------|----------|
| Target Tracking | Maintain a target metric value | Keep CPU at 50% |
| Step Scaling | Scale in steps based on alarm | Complex scaling needs |
| Simple Scaling | Single adjustment | Basic scaling |
| Scheduled Scaling | Scale at specific times | Predictable patterns |
| Predictive Scaling | ML-based forecasting | Recurring patterns |

## Target Tracking Scaling

```
+------------------------------------------------------------------+
|                   TARGET TRACKING SCALING                         |
+------------------------------------------------------------------+
|                                                                   |
|   "Keep average CPU utilization at 50%"                           |
|                                                                   |
|   CPU Usage                                                       |
|   100% |                                                          |
|        |     Scale Out                                            |
|    75% |     ↓                                                    |
|        |  --------                                                |
|    50% |====================  TARGET  ====================        |
|        |                                                          |
|    25% |     ↑                                                    |
|        |     Scale In                                             |
|     0% +------------------------------------------------------->  |
|                                  Time                             |
|                                                                   |
|   Automatically adds/removes instances to maintain target         |
|                                                                   |
+------------------------------------------------------------------+
```

## Common Target Metrics

| Metric | Description |
|--------|-------------|
| ASGAverageCPUUtilization | Average CPU across group |
| ASGAverageNetworkIn | Average bytes received |
| ASGAverageNetworkOut | Average bytes sent |
| ALBRequestCountPerTarget | Requests per instance |

## Scheduled Scaling

| Feature | Description |
|---------|-------------|
| Purpose | Scale at specific times |
| Use case | Predictable traffic patterns |
| Configuration | Start time, min/max/desired |
| Recurrence | One-time or recurring |

## Predictive Scaling

| Feature | Description |
|---------|-------------|
| Purpose | ML-based capacity forecasting |
| How it works | Analyzes historical patterns |
| Benefit | Proactive scaling before demand |
| Accuracy | Improves over time |

## Scaling Cooldown

| Feature | Description |
|---------|-------------|
| Purpose | Prevents rapid scaling |
| Default | 300 seconds (5 minutes) |
| Effect | Ignores scaling during cooldown |
| Customize | Can adjust per policy |

## Health Checks

| Type | Description |
|------|-------------|
| EC2 | Instance status checks |
| ELB | Load balancer health checks |
| Custom | Application-level checks |
| Grace period | Time before checks start |

## Auto Scaling with Load Balancer

```
+------------------------------------------------------------------+
|              AUTO SCALING + LOAD BALANCER                         |
+------------------------------------------------------------------+
|                                                                   |
|   Users                                                           |
|     |                                                             |
|     v                                                             |
|   +------------------+                                            |
|   | Load Balancer    |  Distributes traffic                       |
|   | (ELB/ALB/NLB)    |                                            |
|   +------------------+                                            |
|     |         |         |                                         |
|     v         v         v                                         |
|   +------+ +------+ +------+                                      |
|   | EC2  | | EC2  | | EC2  |  Auto Scaling Group                  |
|   +------+ +------+ +------+                                      |
|     AZ-1    AZ-2     AZ-3                                         |
|                                                                   |
|   Auto Scaling:                                                   |
|   - Registers new instances with LB                               |
|   - Deregisters terminated instances                              |
|   - Uses ELB health checks                                        |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Auto Scaling (Unified Service)

| Feature | Description |
|---------|-------------|
| Purpose | Scale multiple resources together |
| Resources | EC2, ECS, DynamoDB, Aurora, Spot Fleet |
| Scaling plans | Coordinate scaling across resources |
| Console | Unified scaling dashboard |

## Instance Refresh

| Feature | Description |
|---------|-------------|
| Purpose | Update instances with new config |
| How | Gradually replaces instances |
| Benefit | Rolling updates with no downtime |
| Control | Minimum healthy percentage |

## 🎯 Exam Tips

- **Auto Scaling Group (ASG)** = manages EC2 instance capacity
- **Launch Template** = what to launch (AMI, instance type, etc.)
- **Scaling Policy** = when to scale (target tracking, step, scheduled)
- **Target Tracking** = maintain a target metric (e.g., 50% CPU)
- **Scheduled Scaling** = scale at specific times
- **Predictive Scaling** = ML-based forecasting
- **Minimum/Maximum/Desired** = capacity limits for ASG
- Auto Scaling works with **ELB** for high availability
- **Cooldown period** = prevents rapid scaling
- Auto Scaling is **free** - you only pay for EC2 instances

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Auto Scaling Group | Collection of EC2 instances managed together |
| Launch Template | Configuration template for instances |
| Scaling Policy | Rules for when to add/remove instances |
| Target Tracking | Maintain a target metric value |
| Cooldown | Wait period between scaling actions |
| Desired Capacity | Target number of running instances |

## 💡 Key Takeaways

1. Auto Scaling adjusts capacity automatically based on demand
2. Launch Templates define what to launch (AMI, instance type)
3. Auto Scaling Groups define capacity limits (min/max/desired)
4. Scaling Policies define when to scale (target, step, scheduled)
5. Target Tracking is the simplest and most common scaling policy
6. Works seamlessly with Elastic Load Balancing
7. Auto Scaling service is free - you only pay for resources
8. Predictive Scaling uses ML to anticipate demand

---

*Next: [06 - Elastic Load Balancing](../06-elastic-load-balancing/readme.md)*

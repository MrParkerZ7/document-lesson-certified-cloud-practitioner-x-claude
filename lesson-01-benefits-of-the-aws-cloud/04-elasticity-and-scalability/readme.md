# 📈 Elasticity and Scalability

## File Structure

```
lesson-01-benefits-of-the-aws-cloud/
└── 04-elasticity-and-scalability/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Elasticity and scalability are two fundamental concepts that distinguish cloud computing from traditional IT infrastructure. Understanding the difference between these concepts and how AWS implements them is essential for the AWS Certified Cloud Practitioner exam.

## Definitions

### Scalability

The ability of a system to handle increased load by adding resources.

### Elasticity

The ability to **automatically** scale resources up or down based on demand, and **only pay for what you use**.

```
+------------------------------------------------------------------+
|              SCALABILITY vs ELASTICITY                            |
+------------------------------------------------------------------+
|                                                                   |
|   SCALABILITY                    ELASTICITY                      |
|   -----------                    ----------                      |
|   - Ability to grow              - Automatic scaling             |
|   - Manual or automatic          - Responds to demand            |
|   - Planned capacity             - Dynamic adjustment            |
|   - "Can it grow?"               - "Does it grow automatically?" |
|                                                                   |
+------------------------------------------------------------------+
```

## Types of Scaling

### Vertical Scaling (Scale Up/Down)

Increase or decrease the size of a single instance:

```
    VERTICAL SCALING

    Before:                 After:
    +---------+            +-------------+
    | t3.small|     -->    |  t3.xlarge  |
    | 2 vCPU  |            |   4 vCPU    |
    | 2 GB    |            |   16 GB     |
    +---------+            +-------------+

    Same instance, bigger size
```

**Characteristics:**
- Requires instance restart (downtime)
- Limited by largest instance size
- Simple to implement
- Good for databases

### Horizontal Scaling (Scale Out/In)

Add or remove instances:

```
    HORIZONTAL SCALING

    Before:                 After:
    +-------+              +-------+ +-------+ +-------+
    |  EC2  |       -->    |  EC2  | |  EC2  | |  EC2  |
    +-------+              +-------+ +-------+ +-------+

    1 instance             3 instances
```

**Characteristics:**
- No downtime required
- Theoretically unlimited scaling
- Requires load balancing
- Better for web applications

## Comparison: Vertical vs Horizontal

| Aspect | Vertical Scaling | Horizontal Scaling |
|--------|-----------------|-------------------|
| **Method** | Bigger instance | More instances |
| **Downtime** | Usually required | Not required |
| **Limit** | Max instance size | Virtually unlimited |
| **Complexity** | Simple | More complex |
| **Cost pattern** | Linear | Can be more efficient |
| **Best for** | Databases, legacy apps | Web apps, microservices |

## AWS Auto Scaling

AWS Auto Scaling automatically adjusts capacity to maintain performance and optimize costs.

### How Auto Scaling Works

```
+------------------------------------------------------------------+
|                    AUTO SCALING PROCESS                           |
+------------------------------------------------------------------+
|                                                                   |
|   1. Monitor          2. Evaluate         3. Act                 |
|   +---------+        +---------+        +---------+              |
|   |CloudWatch|------>| Scaling |------->|  Add/   |              |
|   | Metrics |        | Policy  |        | Remove  |              |
|   +---------+        +---------+        +---------+              |
|                                                                   |
|   CPU > 80%?         Scale out if       Launch new               |
|   Memory > 70%?      condition met      instances                |
|                                                                   |
+------------------------------------------------------------------+
```

### Auto Scaling Components

1. **Launch Template/Configuration**
   - AMI to use
   - Instance type
   - Security groups
   - Key pair

2. **Auto Scaling Group (ASG)**
   - Minimum capacity
   - Maximum capacity
   - Desired capacity
   - VPC and subnets

3. **Scaling Policies**
   - Target tracking (maintain CPU at 50%)
   - Step scaling (add 2 instances if CPU > 80%)
   - Scheduled (scale up at 9 AM)

### Scaling Policy Types

| Policy Type | Description | Example |
|-------------|-------------|---------|
| **Target Tracking** | Maintain a metric at target value | Keep CPU at 50% |
| **Step Scaling** | Scale based on alarm thresholds | Add 2 if CPU > 80% |
| **Scheduled** | Scale at specific times | Scale up before peak hours |
| **Predictive** | ML-based forecasting | Predict based on patterns |

## Elasticity in Action

### Scenario: E-commerce Website

```
                        Daily Traffic Pattern

    Capacity
       ^
       |         +----+
       |        /      \         Peak Hours
       |       /        \
       |      /          \
       |     /            \
       |----/              \----
       |   Night           Night
       +------------------------> Time
           6am   12pm   6pm   12am


    With Elasticity:
    +--------------------------------------+
    | Auto Scaling adjusts capacity to     |
    | match demand, saving costs during    |
    | low traffic and handling peaks       |
    +--------------------------------------+
```

### Cost Comparison

| Approach | Provisioned | Actual Need | Waste |
|----------|-------------|-------------|-------|
| Traditional (peak capacity) | 100% always | Varies 20-100% | Up to 80% |
| Elastic (auto scaling) | Matches demand | Varies 20-100% | ~0% |

## AWS Services with Built-in Elasticity

| Service | Elasticity Feature |
|---------|-------------------|
| **Amazon EC2 Auto Scaling** | Automatically adjust EC2 capacity |
| **AWS Lambda** | Automatic scaling to any load |
| **Amazon DynamoDB** | On-demand or auto scaling capacity |
| **Amazon Aurora** | Auto scaling storage and read replicas |
| **Amazon ECS** | Service auto scaling |
| **Amazon S3** | Unlimited storage, automatic scaling |
| **Elastic Load Balancing** | Scales automatically with traffic |

## Serverless = Ultimate Elasticity

Serverless services provide automatic elasticity without managing infrastructure:

```
+------------------------------------------------------------------+
|                    SERVERLESS ELASTICITY                          |
+------------------------------------------------------------------+
|                                                                   |
|   Request 1    -->  +--------+                                   |
|   Request 2    -->  | Lambda |  Automatically scales             |
|   Request 3    -->  |Function|  to handle any number             |
|   ...          -->  |        |  of concurrent requests           |
|   Request 1000 -->  +--------+                                   |
|                                                                   |
|   Pay only for actual execution time                             |
|                                                                   |
+------------------------------------------------------------------+
```

## Benefits of Elasticity

| Benefit | Description |
|---------|-------------|
| **Cost Optimization** | Pay only for resources you need |
| **Performance** | Always have enough capacity |
| **Availability** | Handle unexpected traffic spikes |
| **Automation** | No manual intervention needed |
| **Efficiency** | Resources match actual demand |

## 🎯 Exam Tips

- **Elasticity** = automatic + dynamic scaling
- **Scalability** = ability to handle growth
- Know **vertical** (up/down) vs **horizontal** (out/in) scaling
- **Auto Scaling** is the key AWS service for elasticity
- **Serverless** services provide maximum elasticity
- Elasticity helps with **cost optimization**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Elasticity | Automatic scaling based on demand |
| Scalability | Ability to handle increased load |
| Vertical Scaling | Changing instance size |
| Horizontal Scaling | Adding/removing instances |
| Auto Scaling Group | Collection of EC2 instances managed as a unit |

## Review Questions

1. What is the main difference between elasticity and scalability?
   - Answer: Elasticity is automatic and dynamic; scalability is the ability to grow

2. Which type of scaling adds more instances?
   - Answer: Horizontal scaling (scale out)

3. What AWS service provides automatic scaling for EC2?
   - Answer: Amazon EC2 Auto Scaling

---

*Previous: [03 - High Availability](../03-high-availability/readme.md)*

*Next: [05 - Agility and Flexibility](../05-agility-and-flexibility/readme.md)*

# ✅ High Availability

## File Structure

```
lesson-01-benefits-of-the-aws-cloud/
└── 03-high-availability/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

High Availability (HA) is the ability of a system to remain operational and accessible for a high percentage of time. AWS provides the infrastructure and services to build highly available applications that can withstand failures and continue serving users.

## What is High Availability?

High Availability measures the percentage of time a system is operational:

```
+------------------------------------------------------------------+
|                    AVAILABILITY LEVELS                            |
+------------------------------------------------------------------+
|                                                                   |
|   Availability    Downtime/Year    Common Name                   |
|   ------------    -------------    -----------                   |
|   99%             3.65 days        "Two nines"                   |
|   99.9%           8.76 hours       "Three nines"                 |
|   99.99%          52.56 minutes    "Four nines"                  |
|   99.999%         5.26 minutes     "Five nines"                  |
|                                                                   |
+------------------------------------------------------------------+
```

## High Availability vs. Fault Tolerance

| Concept | Definition | Goal |
|---------|------------|------|
| **High Availability** | System remains accessible most of the time | Minimize downtime |
| **Fault Tolerance** | System continues operating despite failures | Zero downtime |
| **Disaster Recovery** | System recovers after major failure | Restore operations |

## How AWS Enables High Availability

### 1. Multiple Availability Zones

```
                    HIGH AVAILABILITY ARCHITECTURE

    +-----------------------------------------------------+
    |                   REGION                             |
    |                                                      |
    |   +-------------+          +-------------+          |
    |   |    AZ-A     |          |    AZ-B     |          |
    |   |  +-------+  |          |  +-------+  |          |
    |   |  |  EC2  |  |          |  |  EC2  |  |          |
    |   |  +-------+  |          |  +-------+  |          |
    |   |  +-------+  |          |  +-------+  |          |
    |   |  |  RDS  |<-+----------+->|  RDS  |  |          |
    |   |  |Primary|  |   Sync   |  |Standby|  |          |
    |   |  +-------+  |   Repl.  |  +-------+  |          |
    |   +-------------+          +-------------+          |
    |          |                        |                 |
    |          +------------------------+                 |
    |                      |                              |
    |              +---------------+                      |
    |              | Load Balancer |                      |
    |              |    (ELB)      |                      |
    |              +---------------+                      |
    |                      |                              |
    +----------------------|------------------------------+
                           |
                       Users
```

**Key Points:**
- Deploy resources across **at least 2 AZs**
- AZs are **physically separated** (different buildings, power, networking)
- Connected via **high-bandwidth, low-latency** networking
- If one AZ fails, the other continues serving traffic

### 2. Elastic Load Balancing (ELB)

Load balancers distribute traffic and provide automatic failover:

| Load Balancer Type | Use Case |
|-------------------|----------|
| **Application LB (ALB)** | HTTP/HTTPS traffic, path-based routing |
| **Network LB (NLB)** | TCP/UDP traffic, ultra-low latency |
| **Gateway LB (GWLB)** | Third-party virtual appliances |

**Benefits for HA:**
- Health checks detect unhealthy instances
- Automatic traffic rerouting
- Cross-zone load balancing
- Integration with Auto Scaling

### 3. Auto Scaling

Automatically maintain application availability:

```
                    AUTO SCALING FOR HIGH AVAILABILITY

    Traffic Spike Detected
           |
           v
    +---------------------------------------------+
    |         AUTO SCALING GROUP                  |
    |                                             |
    |   Before:      After:                       |
    |   +---+        +---+ +---+ +---+            |
    |   |EC2|   -->  |EC2| |EC2| |EC2|            |
    |   +---+        +---+ +---+ +---+            |
    |                                             |
    |   Desired: 1    Desired: 3                  |
    |   Min: 1        Min: 1                      |
    |   Max: 5        Max: 5                      |
    |                                             |
    +---------------------------------------------+
```

### 4. Multi-Region Deployment

For even higher availability, deploy across multiple regions:

```
    +--------------+              +--------------+
    |  US-EAST-1   |              |  EU-WEST-1   |
    |  (Primary)   |              |  (Secondary) |
    |   +-----+    |              |   +-----+    |
    |   | App |    |<------------>|   | App |    |
    |   +-----+    |   Data       |   +-----+    |
    |   +-----+    |   Sync       |   +-----+    |
    |   | DB  |    |              |   | DB  |    |
    |   +-----+    |              |   +-----+    |
    +--------------+              +--------------+
            |                            |
            +------------+---------------+
                         |
                 +---------------+
                 |   Route 53    |
                 |  (DNS-based   |
                 |   failover)   |
                 +---------------+
```

## AWS Services for High Availability

| Service | HA Feature |
|---------|------------|
| **Amazon RDS** | Multi-AZ deployment, automatic failover |
| **Amazon S3** | 99.999999999% durability, cross-region replication |
| **Amazon DynamoDB** | Global tables, automatic replication |
| **Amazon EFS** | Multi-AZ file storage |
| **AWS Lambda** | Runs across multiple AZs automatically |
| **Amazon SQS** | Distributed message queuing |

## Design Principles for High Availability

### 1. Eliminate Single Points of Failure

```
    BAD (Single Point of Failure):

    Users --> Web Server --> Database
                   |
              (If this fails,
               everything fails)


    GOOD (No Single Point of Failure):

                    +--> Web Server 1 --+
    Users --> ELB --+                   +--> RDS Multi-AZ
                    +--> Web Server 2 --+
```

### 2. Implement Health Checks

- **ELB health checks** - Monitor instance health
- **Route 53 health checks** - Monitor endpoint availability
- **Auto Scaling health checks** - Replace unhealthy instances

### 3. Use Managed Services

AWS managed services handle HA automatically:

| Self-Managed | Managed Service |
|--------------|-----------------|
| MySQL on EC2 | Amazon RDS |
| Kubernetes on EC2 | Amazon EKS |
| Message queue on EC2 | Amazon SQS |
| File server on EC2 | Amazon EFS |

### 4. Design for Failure

> "Everything fails, all the time" - Werner Vogels, AWS CTO

- Assume components will fail
- Build redundancy into every layer
- Test failure scenarios regularly

## SLA Examples

| Service | Availability SLA |
|---------|-----------------|
| Amazon EC2 | 99.99% |
| Amazon RDS Multi-AZ | 99.95% |
| Amazon S3 | 99.99% |
| AWS Lambda | 99.95% |

## 🎯 Exam Tips

- **Multi-AZ** deployment is key for high availability
- Know that **ELB** distributes traffic and provides health checks
- Understand **Auto Scaling** maintains desired capacity
- **Managed services** often have built-in HA features
- Regions are **isolated**; AZs are **connected but separated**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| High Availability | System accessible for high percentage of time |
| Fault Tolerance | System operates despite component failures |
| Failover | Automatic switch to standby system |
| Health Check | Automated test of component status |
| SLA | Service Level Agreement (availability guarantee) |

## Review Questions

1. What is the minimum number of AZs recommended for high availability?
   - Answer: At least 2 Availability Zones

2. Which AWS service distributes traffic across multiple instances?
   - Answer: Elastic Load Balancing (ELB)

3. How does RDS achieve high availability?
   - Answer: Multi-AZ deployment with automatic failover

---

*Previous: [02 - Benefits of Global Infrastructure](../02-benefits-of-global-infrastructure/readme.md)*

*Next: [04 - Elasticity and Scalability](../04-elasticity-and-scalability/readme.md)*

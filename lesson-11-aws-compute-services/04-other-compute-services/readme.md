# 🖥️ Other AWS Compute Services

## File Structure

```
lesson-11-aws-compute-services/
└── 04-other-compute-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Beyond EC2, containers, and Lambda, AWS offers additional compute services for specialized use cases including batch processing, edge computing, high-performance computing, and hybrid environments.

## AWS Batch

```
+------------------------------------------------------------------+
|                         AWS BATCH                                 |
+------------------------------------------------------------------+
|                                                                   |
|   Run batch computing workloads at any scale                      |
|                                                                   |
|   +---------------+     +---------------+     +---------------+   |
|   |  Job Queue    | --> | Compute       | --> | Job Results   |   |
|   |               |     | Environment   |     |               |   |
|   | [Job 1]       |     |               |     | Output to S3  |   |
|   | [Job 2]       |     | EC2 / Fargate |     | DynamoDB      |   |
|   | [Job 3]       |     | Spot Instances|     | etc.          |   |
|   +---------------+     +---------------+     +---------------+   |
|                                                                   |
|   Automatically provisions and scales compute resources           |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Batch Features

| Feature | Description |
|---------|-------------|
| Job scheduling | Priority-based job scheduling |
| Compute environments | EC2, Fargate, or Spot Instances |
| Auto scaling | Scales based on job queue |
| Cost optimization | Use Spot Instances for savings |
| Integration | Works with Step Functions, EventBridge |

## AWS Batch Use Cases

| Use Case | Description |
|----------|-------------|
| Financial modeling | Risk analysis, simulations |
| Drug discovery | Molecular simulations |
| Visual effects | Rendering, transcoding |
| Data processing | ETL, log processing |
| Machine learning | Training data processing |

## AWS Lightsail

```
+------------------------------------------------------------------+
|                       AWS LIGHTSAIL                               |
+------------------------------------------------------------------+
|                                                                   |
|   Simple Virtual Private Servers - Easy to start!                 |
|                                                                   |
|   +-------------------+     +-------------------+                  |
|   | INSTANCE          |     | BUNDLED RESOURCES |                  |
|   | Pre-configured    |     |                   |                  |
|   | applications      |     | • Compute         |                  |
|   | • WordPress       |     | • Storage (SSD)   |                  |
|   | • Drupal          |     | • Data transfer   |                  |
|   | • Node.js         |     | • Static IP       |                  |
|   | • LAMP Stack      |     | • DNS management  |                  |
|   | • Windows Server  |     |                   |                  |
|   +-------------------+     +-------------------+                  |
|                                                                   |
|   Fixed monthly price - predictable costs!                        |
|                                                                   |
+------------------------------------------------------------------+
```

## Lightsail Features

| Feature | Description |
|---------|-------------|
| Simplicity | Pre-configured instances |
| Fixed pricing | Predictable monthly cost |
| Bundled resources | Compute, storage, transfer included |
| Blueprints | WordPress, LAMP, Node.js, and more |
| Containers | Container services available |
| Databases | Managed MySQL and PostgreSQL |

## Lightsail vs EC2

| Feature | Lightsail | EC2 |
|---------|-----------|-----|
| Complexity | Simple | Full control |
| Pricing | Fixed monthly | Variable |
| Target user | Beginners, simple workloads | Advanced users |
| Customization | Limited | Extensive |
| Best for | Small websites, dev environments | Production, complex apps |

## AWS Outposts (Compute)

```
+------------------------------------------------------------------+
|                      AWS OUTPOSTS                                 |
+------------------------------------------------------------------+
|                                                                   |
|   AWS infrastructure in YOUR data center                          |
|                                                                   |
|   Your Data Center                                                |
|   +----------------------------------------------------------+   |
|   |                                                           |   |
|   |   +---------------------+                                 |   |
|   |   | AWS OUTPOSTS RACK   |                                 |   |
|   |   |                     |                                 |   |
|   |   | Run EC2, EBS, ECS,  |  <--> Connected to AWS Region   |   |
|   |   | EKS, RDS locally    |                                 |   |
|   |   |                     |                                 |   |
|   |   +---------------------+                                 |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   Same AWS APIs on-premises!                                      |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Local Zones

| Feature | Description |
|---------|-------------|
| Purpose | Extend AWS regions closer to users |
| Latency | Single-digit millisecond latency |
| Services | EC2, EBS, VPC, and more |
| Use cases | Real-time gaming, media, ML inference |
| Location | Major metro areas |

## AWS Wavelength

| Feature | Description |
|---------|-------------|
| Purpose | AWS at 5G network edge |
| Latency | Ultra-low latency for 5G devices |
| Location | Within carrier 5G networks |
| Services | EC2, EBS, VPC |
| Use cases | Mobile apps, IoT, AR/VR |

## Edge Computing Comparison

| Service | Location | Use Case |
|---------|----------|----------|
| Local Zones | AWS facilities near cities | Low-latency for desktop users |
| Wavelength | 5G carrier networks | Ultra-low latency for mobile |
| Outposts | Your data center | On-premises AWS |
| CloudFront | Edge locations globally | Content delivery |

## AWS ParallelCluster

| Feature | Description |
|---------|-------------|
| Purpose | Deploy HPC clusters on AWS |
| Type | Open-source cluster management |
| Use cases | Scientific simulations, research |
| Integration | Works with AWS Batch |
| Networking | EFA for low-latency HPC |

## Elastic Fabric Adapter (EFA)

| Feature | Description |
|---------|-------------|
| Purpose | High-performance networking |
| Use case | HPC, machine learning training |
| Latency | Lower and more consistent |
| OS bypass | Direct hardware access |

## VMware Cloud on AWS

| Feature | Description |
|---------|-------------|
| Purpose | Run VMware workloads on AWS |
| Use case | Migrate VMware VMs to cloud |
| Benefits | Familiar tools, integrated with AWS |
| Management | VMware vCenter and vSphere |

## AWS Compute Optimizer

```
+------------------------------------------------------------------+
|                   AWS COMPUTE OPTIMIZER                           |
+------------------------------------------------------------------+
|                                                                   |
|   Analyzes your resources and recommends optimal configurations   |
|                                                                   |
|   +---------------+     +---------------+     +---------------+   |
|   | CloudWatch    | --> | Compute       | --> | Recommendations|  |
|   | Metrics       |     | Optimizer     |     |               |   |
|   | (14 days)     |     | Analysis      |     | Right-size EC2|   |
|   |               |     |               |     | Optimal types |   |
|   +---------------+     +---------------+     +---------------+   |
|                                                                   |
|   Supports: EC2, EBS, Lambda, ECS on Fargate                      |
|                                                                   |
+------------------------------------------------------------------+
```

## Compute Optimizer Features

| Feature | Description |
|---------|-------------|
| Purpose | Right-size recommendations |
| Resources | EC2, EBS, Lambda, ECS on Fargate |
| Data source | CloudWatch metrics (14+ days) |
| Recommendations | Instance types, sizes, configurations |
| Cost | Free service |

## Service Summary

| Service | Description | Best For |
|---------|-------------|----------|
| AWS Batch | Batch processing | Large-scale batch jobs |
| Lightsail | Simple VPS | Beginners, small workloads |
| Local Zones | Low-latency compute | Desktop application users |
| Wavelength | 5G edge compute | Mobile/IoT applications |
| Outposts | On-premises AWS | Data residency, hybrid |
| ParallelCluster | HPC clusters | Scientific computing |
| Compute Optimizer | Rightsizing | Cost optimization |

## 🎯 Exam Tips

- **AWS Batch** = managed batch processing, automatically scales
- **Lightsail** = simple, fixed-price VPS for beginners (like Heroku for AWS)
- **Local Zones** = AWS near cities for single-digit ms latency
- **Wavelength** = AWS in 5G networks for ultra-low mobile latency
- **Outposts** = AWS hardware in YOUR data center
- **Compute Optimizer** = recommends right-sized instances
- **VMware Cloud on AWS** = run VMware workloads on AWS
- **ParallelCluster** = HPC cluster management
- **EFA** = high-performance networking for HPC

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Batch Processing | Running jobs as a group |
| HPC | High-Performance Computing |
| VPS | Virtual Private Server |
| Edge Computing | Processing near end users |
| Right-sizing | Matching resources to workload |
| EFA | Elastic Fabric Adapter |

## 💡 Key Takeaways

1. AWS Batch manages batch computing with auto-scaling
2. Lightsail provides simple, fixed-price virtual servers for beginners
3. Local Zones bring AWS closer to metro areas for low latency
4. Wavelength puts AWS at the 5G edge for mobile applications
5. Outposts brings AWS infrastructure to your data center
6. Compute Optimizer helps right-size your compute resources
7. Different edge solutions for different use cases (Local Zones, Wavelength, Outposts)

---

*Next: [05 - Auto Scaling](../05-auto-scaling/readme.md)*

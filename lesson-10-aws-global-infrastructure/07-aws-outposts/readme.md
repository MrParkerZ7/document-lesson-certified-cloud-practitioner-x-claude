# 🏗️ AWS Outposts

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 07-aws-outposts/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Outposts brings native AWS services, infrastructure, and operating models to virtually any data center, co-location space, or on-premises facility. You can use the same AWS APIs, tools, and infrastructure on-premises as you use in the AWS cloud.

## What is AWS Outposts?

```
+------------------------------------------------------------------+
|                       AWS OUTPOSTS                                |
+------------------------------------------------------------------+
|                                                                   |
|   AWS Outposts extends AWS infrastructure to your data center    |
|   Run AWS services on-premises with the same experience          |
|                                                                   |
|   Your Data Center                        AWS Region              |
|   +---------------------------+          +-----------------+      |
|   |                           |          |                 |      |
|   |   +-----------------+     |          | AWS Cloud       |      |
|   |   | AWS OUTPOSTS    |     | <------> | Services        |      |
|   |   | (AWS Hardware)  |     |Connected |                 |      |
|   |   |                 |     |          | - S3            |      |
|   |   | - EC2           |     |          | - RDS           |      |
|   |   | - EBS           |     |          | - Lambda        |      |
|   |   | - S3            |     |          | - etc.          |      |
|   |   | - RDS           |     |          +-----------------+      |
|   |   | - EKS           |     |                                   |
|   |   +-----------------+     |                                   |
|   |                           |                                   |
|   +---------------------------+                                   |
|                                                                   |
+------------------------------------------------------------------+
```

## Outposts Characteristics

| Characteristic | Description |
|----------------|-------------|
| Location | Your data center or facility |
| Hardware | AWS-owned and managed |
| Connection | Dedicated connection to AWS |
| APIs | Same AWS APIs and tools |
| Management | AWS manages the hardware |

## Outposts Form Factors

| Type | Description | Use Case |
|------|-------------|----------|
| Outposts Racks | Full 42U racks | Large-scale deployments |
| Outposts Servers | 1U/2U servers | Smaller spaces, edge |

## Services on Outposts

| Category | Services |
|----------|----------|
| Compute | EC2, ECS, EKS |
| Storage | EBS, S3 on Outposts |
| Database | RDS, ElastiCache |
| Containers | ECS, EKS |
| Analytics | EMR |

## Outposts Use Cases

| Use Case | Reason |
|----------|--------|
| Low-latency processing | Data near applications |
| Local data processing | Data residency requirements |
| Data migration | Gradual cloud migration |
| Hybrid workloads | Mix of on-premises and cloud |
| Legacy integration | Connect with legacy systems |

## How Outposts Works

```
+------------------------------------------------------------------+
|                   OUTPOSTS ARCHITECTURE                           |
+------------------------------------------------------------------+
|                                                                   |
|   On-Premises (Your Data Center)                                  |
|   +----------------------------------------------------------+   |
|   |                                                           |   |
|   |   +------------------+     +------------------+           |   |
|   |   | AWS Outposts     |     | Local Systems    |           |   |
|   |   | Rack/Server      |<--->| Applications     |           |   |
|   |   |                  |     | Databases        |           |   |
|   |   | EC2, EBS, S3     |     +------------------+           |   |
|   |   | RDS, EKS         |                                    |   |
|   |   +------------------+                                    |   |
|   |          |                                                |   |
|   +----------|------------------------------------------------+   |
|              | AWS Direct Connect / VPN                           |
|              v                                                    |
|   +----------------------------------------------------------+   |
|   |                    AWS REGION                             |   |
|   |   Full AWS Services - Managed Control Plane               |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Outposts vs Other Options

| Feature | Outposts | Local Zones | Wavelength |
|---------|----------|-------------|------------|
| Location | Your DC | AWS near cities | 5G edge |
| Owner | You host, AWS manages | AWS | AWS + Carrier |
| Target | On-premises needs | Desktop users | Mobile users |
| Hardware | AWS hardware | AWS | AWS |

## Connectivity Options

| Option | Description |
|--------|-------------|
| AWS Direct Connect | Dedicated private connection |
| VPN | Encrypted over internet |
| Local Gateway | Local network access |

## Outposts Components

| Component | Description |
|-----------|-------------|
| Outposts rack/server | Physical AWS hardware |
| Service link | Connection to AWS region |
| Local gateway | On-premises network access |
| Control plane | Managed by AWS in region |

## Ordering and Setup

| Step | Description |
|------|-------------|
| 1. Order | Select configuration in console |
| 2. Delivery | AWS delivers hardware |
| 3. Installation | AWS or partner installs |
| 4. Activation | Connect to AWS region |
| 5. Use | Deploy workloads |

## Pricing

| Component | Pricing |
|-----------|---------|
| Hardware | Upfront or 3-year commitment |
| Services | Same as AWS region |
| Support | AWS manages hardware |
| Networking | Direct Connect charges |

## Benefits

| Benefit | Description |
|---------|-------------|
| Consistency | Same experience as cloud |
| Hybrid | Seamless hybrid architecture |
| Low latency | Process data locally |
| Data residency | Keep data on-premises |
| AWS managed | AWS maintains hardware |

## Limitations

| Limitation | Description |
|------------|-------------|
| Connection required | Need link to AWS region |
| Subset of services | Not all services available |
| Physical space | Requires data center space |
| Cost | Upfront commitment |

## 🎯 Exam Tips

- **Outposts** = AWS hardware in **your data center**
- AWS **owns and manages** the hardware
- Use the **same AWS APIs** on-premises
- Available as **racks** (42U) or **servers** (1U/2U)
- Requires connection to **AWS region** (Direct Connect/VPN)
- For **hybrid**, **low-latency**, **data residency** use cases
- Different from **Local Zones** (AWS locations near cities)
- Different from **Wavelength** (5G edge)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Outposts | AWS infrastructure on-premises |
| Outposts Rack | Full rack of AWS hardware |
| Outposts Server | Single server form factor |
| Service Link | Connection to AWS region |
| Local Gateway | On-premises network connection |

## 💡 Key Takeaways

1. Outposts brings AWS infrastructure to your data center
2. AWS owns, delivers, installs, and manages the hardware
3. Use the same AWS APIs and tools as in the cloud
4. Available as racks (42U) or servers (1U/2U)
5. Requires connectivity to parent AWS region
6. Ideal for hybrid, low-latency, and data residency needs
7. Different from Local Zones and Wavelength

---

*Next: [08 - Multi-Region Strategies](../08-multi-region-strategies/readme.md)*

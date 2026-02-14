# ☁️ Cloud Deployment Models

## File Structure

```
lesson-09-deploying-and-operating-in-aws/
└── 03-cloud-deployment-models/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Cloud deployment models describe how cloud infrastructure is deployed and managed, and who has access to it. Understanding these models is essential for choosing the right approach for your organization's needs, compliance requirements, and workload characteristics.

## Three Main Deployment Models

```
+------------------------------------------------------------------+
|                  CLOUD DEPLOYMENT MODELS                          |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |   PUBLIC CLOUD   |  |  PRIVATE CLOUD   |  |   HYBRID CLOUD   | |
|   +------------------+  +------------------+  +------------------+ |
|   |                  |  |                  |  |                  | |
|   |  AWS, Azure,     |  |  On-premises     |  |  Combination of  | |
|   |  Google Cloud    |  |  or dedicated    |  |  public + private| |
|   |                  |  |  hosting         |  |                  | |
|   +------------------+  +------------------+  +------------------+ |
|   |                  |  |                  |  |                  | |
|   |  Multi-tenant    |  |  Single-tenant   |  |  Connected       | |
|   |  Shared infra    |  |  Dedicated       |  |  Flexible        | |
|   |  Pay-as-you-go   |  |  Full control    |  |  Best of both    | |
|   |                  |  |                  |  |                  | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Public Cloud

Resources are owned and operated by a third-party cloud provider and delivered over the internet.

| Characteristic | Description |
|----------------|-------------|
| Ownership | Cloud provider (AWS, Azure, GCP) |
| Access | Shared among multiple tenants |
| Cost model | Pay-as-you-go, no upfront |
| Scalability | Virtually unlimited |
| Management | Provider manages infrastructure |

### Public Cloud Benefits

| Benefit | Description |
|---------|-------------|
| No capital expense | No hardware to purchase |
| Global reach | Deploy worldwide instantly |
| Elasticity | Scale up/down as needed |
| Lower costs | Economies of scale |
| Innovation | Access to latest services |

### AWS as Public Cloud

| Feature | Description |
|---------|-------------|
| Regions | 30+ regions worldwide |
| Services | 200+ services available |
| Pricing | Pay only for what you use |
| Security | Shared responsibility model |

## Private Cloud

Cloud infrastructure operated solely for a single organization.

| Characteristic | Description |
|----------------|-------------|
| Ownership | Organization or hosted provider |
| Access | Single organization only |
| Location | On-premises or dedicated |
| Control | Full control over infrastructure |
| Compliance | Easier to meet requirements |

### Private Cloud Options

| Option | Description |
|--------|-------------|
| On-premises | Traditional data center |
| AWS Outposts | AWS in your data center |
| VMware Cloud on AWS | VMware on AWS |
| Dedicated Hosts | Dedicated physical servers |

### Private Cloud Use Cases

| Use Case | Reason |
|----------|--------|
| Regulatory compliance | Data residency requirements |
| Legacy applications | Cannot migrate to public cloud |
| Custom hardware | Specific hardware needs |
| Complete control | Full infrastructure control |

## Hybrid Cloud

Combination of public and private cloud with orchestration between them.

| Characteristic | Description |
|----------------|-------------|
| Composition | Public + private cloud |
| Connection | Integrated and orchestrated |
| Flexibility | Choose where workloads run |
| Data movement | Move data between environments |

### Hybrid Cloud Architecture

```
+------------------------------------------------------------------+
|                    HYBRID CLOUD ARCHITECTURE                      |
+------------------------------------------------------------------+
|                                                                   |
|   On-Premises                              AWS Cloud              |
|   (Private)                                (Public)               |
|   +------------------+                     +------------------+   |
|   |  Data Center     |   <-- VPN/DX -->    |  AWS Region      |   |
|   |  - Legacy Apps   |                     |  - New Apps      |   |
|   |  - Databases     |                     |  - Burst Capacity|   |
|   |  - Sensitive Data|                     |  - DR Site       |   |
|   +------------------+                     +------------------+   |
|                                                                   |
|   AWS Outposts (AWS in your DC)                                   |
|   +------------------+                                            |
|   |  Same AWS APIs   |                                            |
|   |  Local processing|                                            |
|   |  Low latency     |                                            |
|   +------------------+                                            |
|                                                                   |
+------------------------------------------------------------------+
```

### Hybrid Cloud Connection Options

| Service | Description |
|---------|-------------|
| AWS VPN | Encrypted tunnel over internet |
| AWS Direct Connect | Dedicated private connection |
| AWS Transit Gateway | Central hub for connections |
| AWS Outposts | AWS hardware on-premises |

### Hybrid Cloud Use Cases

| Use Case | Description |
|----------|-------------|
| Cloud bursting | Scale to cloud during peaks |
| Disaster recovery | DR site in the cloud |
| Gradual migration | Migrate workloads over time |
| Data locality | Keep sensitive data on-prem |
| Compliance | Meet regulatory requirements |

## Deployment Model Comparison

| Factor | Public | Private | Hybrid |
|--------|--------|---------|--------|
| Cost | Lowest upfront | Highest upfront | Medium |
| Scalability | Highest | Limited | High |
| Control | Lowest | Highest | High |
| Security | Shared | Full control | Flexible |
| Compliance | Depends | Easier | Flexible |
| Speed to deploy | Fastest | Slowest | Medium |

## Multi-Cloud

Using multiple public cloud providers.

| Aspect | Description |
|--------|-------------|
| Definition | AWS + Azure + GCP, etc. |
| Purpose | Avoid vendor lock-in, best services |
| Complexity | Higher management overhead |
| Tools | Terraform, Kubernetes for portability |

## Choosing a Deployment Model

| Choose | When |
|--------|------|
| Public Cloud | Cost-effective, scalable, agile |
| Private Cloud | Compliance, control, legacy apps |
| Hybrid Cloud | Gradual migration, data locality |
| Multi-Cloud | Best of each provider, redundancy |

## 🎯 Exam Tips

- **Public Cloud** = AWS, shared infrastructure, multi-tenant
- **Private Cloud** = dedicated to single organization
- **Hybrid Cloud** = public + private connected together
- **AWS Outposts** = AWS infrastructure on-premises
- **Direct Connect** = dedicated private connection to AWS
- **VPN** = encrypted tunnel over public internet
- Know the **benefits and use cases** for each model
- AWS is a **public cloud** provider

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Public Cloud | Shared cloud resources from provider |
| Private Cloud | Dedicated cloud for one organization |
| Hybrid Cloud | Combination of public and private |
| Multi-Cloud | Multiple public cloud providers |
| Cloud Bursting | Scaling to public cloud during peaks |
| AWS Outposts | AWS infrastructure on-premises |

## 💡 Key Takeaways

1. Public cloud offers shared, multi-tenant resources with pay-as-you-go pricing
2. Private cloud provides dedicated resources for a single organization
3. Hybrid cloud combines public and private with connectivity between them
4. AWS is a public cloud provider offering global infrastructure
5. Hybrid connections include VPN, Direct Connect, and AWS Outposts
6. Choose the model based on cost, compliance, control, and scalability needs
7. Many organizations use hybrid approach for flexibility

---

*Next: [04 - One-Time vs Repeatable Processes](../04-one-time-vs-repeatable-processes/readme.md)*

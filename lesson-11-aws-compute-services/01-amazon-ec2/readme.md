# 🖥️ Amazon EC2 (Elastic Compute Cloud)

## File Structure

```
lesson-11-aws-compute-services/
└── 01-amazon-ec2/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Amazon EC2 provides secure, resizable compute capacity in the cloud. It is the backbone of AWS compute services, allowing you to launch virtual servers (instances) with your choice of operating systems, CPU, memory, storage, and networking capacity.

## What is Amazon EC2?

```
+------------------------------------------------------------------+
|                         AMAZON EC2                                |
+------------------------------------------------------------------+
|                                                                   |
|   EC2 = Virtual Servers in the Cloud                              |
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |  Instance 1      |  |  Instance 2      |  |  Instance 3      | |
|   |  (Web Server)    |  |  (App Server)    |  |  (Database)      | |
|   |  t3.medium       |  |  c5.xlarge       |  |  r5.2xlarge      | |
|   |  Linux           |  |  Windows         |  |  Linux           | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
|   You choose: Instance Type, OS, Storage, Networking, Security   |
|                                                                   |
+------------------------------------------------------------------+
```

## EC2 Instance Types

| Family | Optimized For | Use Cases |
|--------|---------------|-----------|
| General Purpose (T, M) | Balanced compute, memory, networking | Web servers, dev environments |
| Compute Optimized (C) | High-performance processors | Batch processing, gaming servers |
| Memory Optimized (R, X) | Fast performance for memory-intensive workloads | In-memory databases, real-time analytics |
| Storage Optimized (I, D) | High sequential read/write to local storage | Data warehousing, distributed file systems |
| Accelerated Computing (P, G) | Hardware accelerators (GPUs) | Machine learning, graphics rendering |

## Instance Naming Convention

```
+------------------------------------------------------------------+
|                   INSTANCE TYPE NAMING                            |
+------------------------------------------------------------------+
|                                                                   |
|                        c5.xlarge                                  |
|                        |  |  |                                    |
|                        |  |  +-- Size (nano to 24xlarge)          |
|                        |  +----- Generation (5th gen)             |
|                        +-------- Family (Compute optimized)       |
|                                                                   |
|   Examples:                                                       |
|   - t3.micro  = General purpose, 3rd gen, micro size              |
|   - m6i.large = General purpose, 6th gen Intel, large size        |
|   - r5.2xlarge = Memory optimized, 5th gen, 2xlarge size          |
|                                                                   |
+------------------------------------------------------------------+
```

## EC2 Purchasing Options

| Option | Description | Use Case | Savings |
|--------|-------------|----------|---------|
| On-Demand | Pay by the hour/second | Short-term, unpredictable workloads | None (baseline) |
| Reserved Instances | 1 or 3 year commitment | Steady-state workloads | Up to 72% |
| Savings Plans | Flexible 1 or 3 year commitment | Flexible compute usage | Up to 72% |
| Spot Instances | Bid on unused capacity | Fault-tolerant, flexible workloads | Up to 90% |
| Dedicated Hosts | Physical server for your use | Licensing, compliance | Varies |
| Dedicated Instances | Instance on dedicated hardware | Compliance requirements | Higher cost |

## Purchasing Options Comparison

```
+------------------------------------------------------------------+
|                    EC2 PRICING OPTIONS                            |
+------------------------------------------------------------------+
|                                                                   |
|   COST                                                            |
|   High |                                                          |
|        |  [On-Demand] $$$$ - Pay as you go, no commitment         |
|        |                                                          |
|        |  [Reserved]  $$   - 1-3 year commitment, up to 72% off   |
|        |                                                          |
|        |  [Spot]      $    - Up to 90% off, can be interrupted    |
|   Low  |                                                          |
|        +----------------------------------------------------->    |
|                           COMMITMENT                              |
|                                                                   |
+------------------------------------------------------------------+
```

## Reserved Instance Types

| Type | Description |
|------|-------------|
| Standard RI | Best discount, less flexibility |
| Convertible RI | Can change instance type, lower discount |
| Scheduled RI | Reserved for specific time windows |

## Spot Instances

| Feature | Description |
|---------|-------------|
| Price | Set by supply/demand, up to 90% off |
| Interruption | Can be terminated with 2-minute notice |
| Best for | Fault-tolerant, stateless workloads |
| Examples | Batch jobs, data analysis, CI/CD |

## EC2 Instance Lifecycle

| State | Description |
|-------|-------------|
| Pending | Instance is launching |
| Running | Instance is running and billed |
| Stopping | Instance is stopping |
| Stopped | Instance stopped, no compute charges |
| Terminated | Instance deleted |

## Amazon Machine Images (AMI)

| Component | Description |
|-----------|-------------|
| Definition | Template for launching instances |
| Contains | OS, applications, configurations |
| Types | AWS, Marketplace, Community, Custom |
| Region | AMIs are region-specific |

## EC2 Storage Options

| Type | Description | Persistence |
|------|-------------|-------------|
| Instance Store | Temporary block storage | Ephemeral (lost on stop) |
| EBS Volumes | Persistent block storage | Persistent |
| EFS | Shared file storage | Persistent |

## Security Groups

| Feature | Description |
|---------|-------------|
| Function | Virtual firewall for instances |
| Type | Stateful (return traffic allowed) |
| Rules | Inbound and outbound rules |
| Default | All inbound denied, all outbound allowed |

## Key Pairs

| Component | Description |
|-----------|-------------|
| Purpose | Secure SSH/RDP access to instances |
| Private Key | You keep this, never share |
| Public Key | AWS stores on the instance |

## User Data

| Feature | Description |
|---------|-------------|
| Purpose | Run scripts at instance launch |
| Use Cases | Install software, configure settings |
| Runs | Only at first boot (by default) |

## EC2 Placement Groups

| Type | Description | Use Case |
|------|-------------|----------|
| Cluster | Instances in single AZ, low latency | HPC, big data |
| Spread | Instances on distinct hardware | Critical applications |
| Partition | Groups of instances on separate racks | Distributed databases |

## 🎯 Exam Tips

- **Instance types** start with a letter (family), followed by generation number and size
- **On-Demand** = pay as you go, no commitment, highest flexibility
- **Reserved** = 1-3 year commitment, up to 72% discount
- **Spot** = up to 90% discount, can be interrupted, good for fault-tolerant workloads
- **Dedicated Hosts** = for licensing requirements (per-socket, per-core licenses)
- **Security Groups** = stateful firewall, attached to instances
- **AMI** = template for launching instances (OS + software)
- **EBS** = persistent storage, **Instance Store** = ephemeral storage
- **User Data** = bootstrap scripts run at instance launch

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Instance | Virtual server in EC2 |
| AMI | Amazon Machine Image, launch template |
| Instance Type | Hardware configuration (CPU, memory, etc.) |
| Security Group | Virtual firewall for instances |
| Key Pair | SSH/RDP authentication mechanism |
| EBS | Elastic Block Store, persistent storage |
| Spot Instance | Discounted unused EC2 capacity |

## 💡 Key Takeaways

1. EC2 provides resizable virtual servers in the cloud
2. Instance types are categorized by family (compute, memory, storage, etc.)
3. On-Demand is flexible but most expensive; Reserved and Spot offer savings
4. Spot Instances offer up to 90% discount but can be interrupted
5. Security Groups act as stateful firewalls for instances
6. AMIs are templates containing OS and application configurations
7. Choose the right purchasing option based on workload characteristics

---

*Next: [02 - Container Services](../02-container-services/readme.md)*

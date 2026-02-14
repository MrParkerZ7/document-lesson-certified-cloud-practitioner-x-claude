# 🔗 Amazon VPC (Virtual Private Cloud)

## File Structure

```
lesson-13-aws-networking-services/
└── 01-amazon-vpc/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Amazon VPC is the networking layer of AWS that lets you create your own isolated, private network within the AWS Cloud. It provides complete control over your virtual networking environment, including IP address ranges, subnets, route tables, and network gateways.

## What is Amazon VPC?

```
+------------------------------------------------------------------+
|                         AMAZON VPC                                |
+------------------------------------------------------------------+
|                                                                   |
|   VPC = Your Own Private Network in AWS                           |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                     VPC (10.0.0.0/16)                     |   |
|   |                                                           |   |
|   |   +---------------+          +---------------+            |   |
|   |   | Public Subnet |          | Private Subnet|            |   |
|   |   | 10.0.1.0/24   |          | 10.0.2.0/24   |            |   |
|   |   |               |          |               |            |   |
|   |   | [Web Server]  |          | [Database]    |            |   |
|   |   +-------+-------+          +-------+-------+            |   |
|   |           |                          |                    |   |
|   +-----------|--------------------------|--------------------+   |
|               |                          |                        |
|               v                          v                        |
|        Internet Gateway             NAT Gateway                   |
|               |                          |                        |
|               v                          |                        |
|           INTERNET <---------------------+                        |
|                                                                   |
+------------------------------------------------------------------+
```

## VPC Key Components

| Component | Description | Purpose |
|-----------|-------------|---------|
| VPC | Isolated virtual network | Contains all your AWS resources |
| Subnet | Segment of VPC IP range | Organizes resources by function |
| Internet Gateway | VPC to Internet connection | Enables public internet access |
| NAT Gateway | Private to Internet (outbound) | Allows private resources to reach internet |
| Route Table | Network traffic rules | Directs traffic between subnets |
| CIDR Block | IP address range | Defines available IP addresses |

## Understanding CIDR Notation

```
+------------------------------------------------------------------+
|                      CIDR NOTATION                                |
+------------------------------------------------------------------+
|                                                                   |
|   CIDR = Classless Inter-Domain Routing                           |
|                                                                   |
|   Example: 10.0.0.0/16                                            |
|            --------  --                                           |
|               |       |                                           |
|               |       +-- Prefix length (network bits)            |
|               +---------- Network address                         |
|                                                                   |
|   /16 = 65,536 IP addresses (10.0.0.0 - 10.0.255.255)            |
|   /24 = 256 IP addresses    (10.0.1.0 - 10.0.1.255)              |
|   /28 = 16 IP addresses     (smallest subnet in AWS)             |
|                                                                   |
+------------------------------------------------------------------+
```

## CIDR Block Sizes

| CIDR | Available IPs | Common Use |
|------|---------------|------------|
| /16 | 65,536 | Large VPC |
| /20 | 4,096 | Medium VPC |
| /24 | 256 | Single subnet |
| /28 | 16 | Smallest AWS subnet |

**Note:** AWS reserves 5 IP addresses in each subnet for internal use.

## Public vs. Private Subnets

| Feature | Public Subnet | Private Subnet |
|---------|---------------|----------------|
| Internet Access | Direct via Internet Gateway | Via NAT Gateway (outbound only) |
| Public IP | Can have public/Elastic IPs | No public IPs |
| Route Table | Route to Internet Gateway | Route to NAT Gateway |
| Use Cases | Web servers, bastion hosts | Databases, application servers |
| Accessibility | Reachable from internet | Not directly reachable |

## Subnet Architecture

```
+------------------------------------------------------------------+
|                    VPC SUBNET DESIGN                              |
+------------------------------------------------------------------+
|                                                                   |
|                        VPC (10.0.0.0/16)                          |
|   +---------------------------+---------------------------+       |
|   |     Availability Zone A   |     Availability Zone B   |       |
|   +---------------------------+---------------------------+       |
|   |                           |                           |       |
|   |   +-------------------+   |   +-------------------+   |       |
|   |   | PUBLIC SUBNET     |   |   | PUBLIC SUBNET     |   |       |
|   |   | 10.0.1.0/24       |   |   | 10.0.2.0/24       |   |       |
|   |   | [Web Server]      |   |   | [Web Server]      |   |       |
|   |   +-------------------+   |   +-------------------+   |       |
|   |                           |                           |       |
|   |   +-------------------+   |   +-------------------+   |       |
|   |   | PRIVATE SUBNET    |   |   | PRIVATE SUBNET    |   |       |
|   |   | 10.0.3.0/24       |   |   | 10.0.4.0/24       |   |       |
|   |   | [Database]        |   |   | [Database]        |   |       |
|   |   +-------------------+   |   +-------------------+   |       |
|   |                           |                           |       |
|   +---------------------------+---------------------------+       |
|                                                                   |
+------------------------------------------------------------------+
```

## Internet Gateway (IGW)

| Feature | Description |
|---------|-------------|
| Purpose | Connect VPC to the internet |
| Attachment | One IGW per VPC |
| Availability | Highly available, redundant |
| Cost | Free (pay for data transfer) |
| Requirement | Must update route table |

## NAT Gateway

| Feature | Description |
|---------|-------------|
| Purpose | Allow private subnets outbound internet access |
| Direction | Outbound only (no inbound from internet) |
| Placement | Must be in a public subnet |
| Availability | Single AZ (deploy in each AZ for HA) |
| Cost | Hourly charge + data processing |
| Managed | Fully managed by AWS |

## NAT Gateway vs. NAT Instance

| Feature | NAT Gateway | NAT Instance |
|---------|-------------|--------------|
| Managed | AWS managed | You manage |
| Availability | Highly available in AZ | Single instance |
| Bandwidth | Up to 100 Gbps | Depends on instance type |
| Maintenance | No patching needed | You patch/maintain |
| Cost | More expensive | Cheaper but more work |
| Security Groups | Not supported | Supported |

## Route Tables

```
+------------------------------------------------------------------+
|                     ROUTE TABLE EXAMPLE                           |
+------------------------------------------------------------------+
|                                                                   |
|   PUBLIC SUBNET ROUTE TABLE:                                      |
|   +-------------------+-------------------+                       |
|   | Destination       | Target            |                       |
|   +-------------------+-------------------+                       |
|   | 10.0.0.0/16       | local             | <-- VPC internal      |
|   | 0.0.0.0/0         | igw-xxxxx         | <-- Internet Gateway  |
|   +-------------------+-------------------+                       |
|                                                                   |
|   PRIVATE SUBNET ROUTE TABLE:                                     |
|   +-------------------+-------------------+                       |
|   | Destination       | Target            |                       |
|   +-------------------+-------------------+                       |
|   | 10.0.0.0/16       | local             | <-- VPC internal      |
|   | 0.0.0.0/0         | nat-xxxxx         | <-- NAT Gateway       |
|   +-------------------+-------------------+                       |
|                                                                   |
+------------------------------------------------------------------+
```

## Default VPC

| Feature | Description |
|---------|-------------|
| Created | Automatically in each region |
| CIDR | 172.31.0.0/16 |
| Subnets | One public subnet per AZ |
| Internet Gateway | Pre-configured |
| Use Case | Quick start, testing |

## Custom VPC Features

| Feature | Description |
|---------|-------------|
| CIDR Range | You define (e.g., 10.0.0.0/16) |
| Subnets | You create and configure |
| Route Tables | You customize |
| Gateways | You attach as needed |
| Use Case | Production, security requirements |

## VPC Endpoints

| Type | Description | Use Case |
|------|-------------|----------|
| Gateway Endpoint | Free, for S3 and DynamoDB | Access S3/DynamoDB privately |
| Interface Endpoint | Uses PrivateLink, costs money | Access other AWS services privately |

```
+------------------------------------------------------------------+
|                      VPC ENDPOINTS                                |
+------------------------------------------------------------------+
|                                                                   |
|   Without Endpoint:                                               |
|   [Private Instance] --> NAT GW --> Internet --> S3               |
|                                                                   |
|   With Gateway Endpoint:                                          |
|   [Private Instance] --> VPC Endpoint --> S3 (stays in AWS)       |
|                                                                   |
|   Benefits: More secure, lower latency, reduced NAT costs         |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **VPC** is a logically isolated network within AWS - you control everything
- **CIDR blocks** define IP ranges; /16 is largest VPC, /28 is smallest subnet
- **Public subnets** have routes to Internet Gateway; **Private subnets** do not
- **Internet Gateway** enables internet access for public subnets (free, HA)
- **NAT Gateway** allows private subnets to access internet (outbound only, costs money)
- **Route tables** control traffic flow between subnets and gateways
- **Default VPC** is created automatically; use **custom VPC** for production
- **VPC Endpoints** allow private access to AWS services without internet
- AWS reserves **5 IP addresses** in each subnet

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| VPC | Virtual Private Cloud, isolated network in AWS |
| Subnet | Segment of VPC with its own IP range |
| CIDR | IP addressing notation (e.g., 10.0.0.0/16) |
| Internet Gateway | Connects VPC to the internet |
| NAT Gateway | Allows private subnet outbound internet access |
| Route Table | Rules determining network traffic destinations |
| VPC Endpoint | Private connection to AWS services |

## 💡 Key Takeaways

1. Amazon VPC provides an isolated, customizable network within AWS
2. CIDR notation defines IP address ranges; smaller prefix = more IPs
3. Public subnets have routes to Internet Gateway; private subnets do not
4. NAT Gateway enables private resources to access internet (outbound only)
5. Route tables control how traffic flows between subnets and gateways
6. VPC Endpoints provide private access to AWS services without traversing internet
7. Design VPCs with subnets across multiple AZs for high availability

---

*Next: [02 - VPC Security](../02-vpc-security/readme.md)*

# ☁️ AWS Responsibilities - Security OF the Cloud

## File Structure

```
lesson-05-aws-shared-responsibility-model/
└── 02-aws-responsibilities/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Overview

AWS is responsible for **"Security OF the Cloud"** - this encompasses protecting the infrastructure that runs all services offered in the AWS Cloud. This includes hardware, software, networking, and facilities that run AWS Cloud services.

## AWS Responsibility Categories

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        AWS RESPONSIBILITY LAYERS                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  MANAGED SERVICES SECURITY                                            │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐     │  │
│  │  │     RDS     │ │   Lambda    │ │  DynamoDB   │ │   Aurora    │     │  │
│  │  │   Engine    │ │   Runtime   │ │   Engine    │ │   Engine    │     │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  SOFTWARE INFRASTRUCTURE                                              │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐     │  │
│  │  │  Hypervisor │ │     Host    │ │  Networking │ │   Storage   │     │  │
│  │  │   (Nitro)   │ │      OS     │ │   Software  │ │   Software  │     │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  HARDWARE INFRASTRUCTURE                                              │  │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐     │  │
│  │  │   Servers   │ │   Storage   │ │  Network    │ │  Proprietary│     │  │
│  │  │             │ │   Devices   │ │  Equipment  │ │   Hardware  │     │  │
│  │  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  GLOBAL INFRASTRUCTURE                                                │  │
│  │  ┌────────────────────┐ ┌────────────────────┐ ┌──────────────────┐  │  │
│  │  │      Regions       │ │ Availability Zones │ │  Edge Locations  │  │  │
│  │  │     (30+)          │ │      (100+)        │ │    (400+)        │  │  │
│  │  └────────────────────┘ └────────────────────┘ └──────────────────┘  │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  PHYSICAL SECURITY                                                    │  │
│  │  ┌────────────────────┐ ┌────────────────────┐ ┌──────────────────┐  │  │
│  │  │   Access Control   │ │    Surveillance    │ │   Environmental  │  │  │
│  │  │   Biometrics, MFA  │ │   24/7 Monitoring  │ │   Power, Cooling │  │  │
│  │  └────────────────────┘ └────────────────────┘ └──────────────────┘  │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

## 1. Physical Security

AWS operates and maintains the physical security of data centers worldwide.

### Data Center Security Measures

| Security Layer | Implementation |
|---------------|----------------|
| **Perimeter Control** | Fencing, security guards, vehicle barriers |
| **Building Access** | Biometric scanners, access cards, mantraps |
| **Surveillance** | 24/7 CCTV monitoring, motion detection |
| **Personnel** | Background checks, escort requirements for visitors |
| **Access Logging** | All access attempts logged and audited |

### Environmental Controls

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENVIRONMENTAL CONTROLS                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐         │
│  │   POWER     │    │   COOLING   │    │    FIRE     │         │
│  ├─────────────┤    ├─────────────┤    ├─────────────┤         │
│  │ • UPS       │    │ • HVAC      │    │ • Detection │         │
│  │ • Generators│    │ • Hot/Cold  │    │ • Suppresn  │         │
│  │ • Redundant │    │   Aisles    │    │ • Sprinklers│         │
│  │   Feeds     │    │ • Monitoring│    │             │         │
│  └─────────────┘    └─────────────┘    └─────────────┘         │
│                                                                 │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐         │
│  │   FLOOD     │    │  SEISMIC    │    │   BACKUP    │         │
│  ├─────────────┤    ├─────────────┤    ├─────────────┤         │
│  │ • Elevation │    │ • Building  │    │ • Multiple  │         │
│  │ • Drainage  │    │   Design    │    │   AZs       │         │
│  │ • Sensors   │    │ • Location  │    │ • Failover  │         │
│  │             │    │   Selection │    │   Systems   │         │
│  └─────────────┘    └─────────────┘    └─────────────┘         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### What AWS Protects Physically

- Server hardware and storage devices
- Networking equipment (routers, switches, cables)
- Physical access points to data centers
- Power and cooling infrastructure
- Facility perimeter and building structure

## 2. Hardware Infrastructure

AWS is responsible for all hardware that powers the cloud.

### Hardware Components

| Component | AWS Responsibility |
|-----------|-------------------|
| **Compute** | Physical servers, CPUs, memory, storage |
| **Networking** | Routers, switches, firewalls, load balancers |
| **Storage** | HDDs, SSDs, storage arrays |
| **Proprietary** | AWS Nitro chips, Graviton processors |

### AWS Nitro System

AWS developed the Nitro System to provide enhanced security:

```
┌─────────────────────────────────────────────────────────────────┐
│                     AWS NITRO SYSTEM                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │              NITRO SECURITY CHIP                        │   │
│  │  • Prevents unauthorized access to hardware             │   │
│  │  • Continuously monitors and protects system            │   │
│  │  • Hardware-based root of trust                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                            │                                    │
│                            ▼                                    │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │              NITRO HYPERVISOR                           │   │
│  │  • Minimal attack surface                               │   │
│  │  • Strong isolation between instances                   │   │
│  │  • No admin access to underlying host                   │   │
│  └─────────────────────────────────────────────────────────┘   │
│                            │                                    │
│                            ▼                                    │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │              NITRO CARDS                                │   │
│  │  • Offload I/O for networking and storage               │   │
│  │  • Hardware-accelerated encryption                      │   │
│  │  • Improved performance and security                    │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 3. Network Infrastructure

AWS manages the global network infrastructure.

### Network Security Measures

| Security Measure | Description |
|-----------------|-------------|
| **DDoS Protection** | Built-in protection against DDoS attacks (AWS Shield Standard) |
| **Network Isolation** | Physical and logical separation of customer networks |
| **Encryption** | TLS/SSL for data in transit |
| **Monitoring** | 24/7 network monitoring and threat detection |
| **Redundancy** | Multiple network paths and automatic failover |

### AWS Global Network

```
                    AWS GLOBAL NETWORK ARCHITECTURE

                    ┌─────────────────────────────┐
                    │      AWS BACKBONE           │
                    │  (Private Global Network)   │
                    └─────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│    REGION     │    │    REGION     │    │    REGION     │
│   us-east-1   │    │   eu-west-1   │    │ ap-southeast-1│
├───────────────┤    ├───────────────┤    ├───────────────┤
│ ┌───┐ ┌───┐  │    │ ┌───┐ ┌───┐  │    │ ┌───┐ ┌───┐  │
│ │AZ1│ │AZ2│  │    │ │AZ1│ │AZ2│  │    │ │AZ1│ │AZ2│  │
│ └───┘ └───┘  │    │ └───┘ └───┘  │    │ └───┘ └───┘  │
│    ┌───┐     │    │    ┌───┐     │    │    ┌───┐     │
│    │AZ3│     │    │    │AZ3│     │    │    │AZ3│     │
│    └───┘     │    │    └───┘     │    │    └───┘     │
└───────────────┘    └───────────────┘    └───────────────┘
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                    ┌─────────────────────────────┐
                    │      EDGE LOCATIONS         │
                    │   (400+ Global Locations)   │
                    └─────────────────────────────┘
```

## 4. Software Infrastructure

AWS maintains all foundational software.

### Hypervisor Security

- **AWS Nitro Hypervisor**: Minimal, security-focused hypervisor
- **Instance Isolation**: Strong boundaries between customer instances
- **No AWS Operator Access**: AWS employees cannot access customer instances

### Host Operating System

- **Regular Patching**: AWS patches host OS automatically
- **Security Hardening**: OS stripped to essential components only
- **Continuous Monitoring**: Automated security scanning

## 5. Managed Services Security

For managed services, AWS takes on additional responsibilities.

### AWS Managed Service Examples

| Service | AWS Manages |
|---------|-------------|
| **RDS** | Database engine patching, backups, failover |
| **Lambda** | Runtime environment, scaling, execution environment |
| **DynamoDB** | Database engine, storage, replication |
| **ECS/EKS** | Control plane, orchestration |
| **S3** | Storage infrastructure, durability, availability |

### Managed vs. Unmanaged Comparison

```
┌─────────────────────────────────────────────────────────────────┐
│                 MANAGED VS UNMANAGED                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  EC2 (UNMANAGED - IaaS)         RDS (MANAGED - PaaS)           │
│  ┌─────────────────────┐        ┌─────────────────────┐        │
│  │ Customer Manages:   │        │ AWS Manages:        │        │
│  │ • Guest OS          │        │ • Database engine   │        │
│  │ • Applications      │        │ • OS patching       │        │
│  │ • Patching          │        │ • Backups           │        │
│  │ • Backups           │        │ • High availability │        │
│  ├─────────────────────┤        ├─────────────────────┤        │
│  │ AWS Manages:        │        │ Customer Manages:   │        │
│  │ • Hardware          │        │ • Data              │        │
│  │ • Hypervisor        │        │ • Schema            │        │
│  │ • Physical security │        │ • Access control    │        │
│  └─────────────────────┘        └─────────────────────┘        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Compliance and Certifications

AWS maintains numerous compliance certifications for their responsibilities.

### Key Compliance Programs

| Certification | Description |
|--------------|-------------|
| **SOC 1/2/3** | Service Organization Controls reports |
| **ISO 27001** | Information security management |
| **ISO 27017** | Cloud-specific security controls |
| **ISO 27018** | Personal data protection in cloud |
| **PCI DSS Level 1** | Payment card industry compliance |
| **HIPAA** | Healthcare data protection |
| **FedRAMP** | US government cloud security |
| **CSA STAR** | Cloud Security Alliance certification |

### AWS Artifact

AWS provides compliance reports through **AWS Artifact**:

```
┌─────────────────────────────────────────────────────────────────┐
│                      AWS ARTIFACT                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                 COMPLIANCE REPORTS                       │   │
│  │  • SOC Reports (1, 2, 3)                                │   │
│  │  • PCI DSS Attestation of Compliance                    │   │
│  │  • ISO Certifications                                   │   │
│  │  • Service Organization Controls                        │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                 AGREEMENTS                               │   │
│  │  • Business Associate Agreement (BAA) for HIPAA         │   │
│  │  • Non-Disclosure Agreements                            │   │
│  │  • Data Processing Agreements                           │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Access: AWS Console → AWS Artifact → Download Reports         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## AWS Security Investments

AWS continuously invests in security:

- **Billions of dollars** invested annually in security infrastructure
- **Thousands of security personnel** dedicated to cloud security
- **Continuous security research** and threat intelligence
- **Regular third-party audits** and penetration testing
- **Security automation** at massive scale

## 🎯 Exam Tips

> **Tip 1**: Physical security is 100% AWS responsibility - customers never access data centers

> **Tip 2**: AWS Artifact is where you get compliance reports and agreements

> **Tip 3**: The Nitro System provides hardware-based security isolation

> **Tip 4**: Managed services shift MORE responsibility to AWS (like RDS patches the DB engine)

> **Tip 5**: AWS Shield Standard provides FREE DDoS protection at the infrastructure level

> **Tip 6**: Host OS and hypervisor are always AWS responsibility, Guest OS varies by service

## Key Exam Scenarios

### Scenario 1: Compliance Audit
**Question**: Where do you get AWS's SOC 2 report for a compliance audit?
**Answer**: **AWS Artifact** - provides on-demand access to compliance reports

### Scenario 2: Physical Security Incident
**Question**: Who investigates if someone attempts unauthorized data center access?
**Answer**: **AWS** - all physical security is AWS responsibility

### Scenario 3: Hardware Failure
**Question**: A hard drive fails containing customer data. Who replaces it?
**Answer**: **AWS** - hardware maintenance is AWS responsibility

### Scenario 4: DDoS Attack
**Question**: Who provides protection against infrastructure-level DDoS attacks?
**Answer**: **AWS** via **AWS Shield Standard** (free, automatic protection)

## 💡 Key Takeaways

1. **AWS secures all physical infrastructure** - data centers, hardware, networking
2. **AWS maintains the hypervisor and host OS** - customers cannot access these
3. **AWS provides compliance certifications** - available via AWS Artifact
4. **Managed services shift more responsibility to AWS** - like RDS, Lambda, DynamoDB
5. **AWS invests billions in security** - customers benefit from economies of scale
6. **AWS Shield Standard is free** - protects against infrastructure DDoS
7. **Physical security is never customer responsibility** - no data center access

## Quick Reference

```
╔═══════════════════════════════════════════════════════════════╗
║               AWS RESPONSIBILITIES SUMMARY                     ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║  ALWAYS AWS RESPONSIBILITY:                                   ║
║  ├─ Physical data center security                             ║
║  ├─ Hardware maintenance and replacement                      ║
║  ├─ Network infrastructure                                    ║
║  ├─ Hypervisor and host OS                                    ║
║  ├─ Global infrastructure (Regions, AZs, Edge)                ║
║  └─ DDoS protection at infrastructure level                   ║
║                                                               ║
║  FOR MANAGED SERVICES, AWS ALSO HANDLES:                      ║
║  ├─ Database engine patching (RDS)                            ║
║  ├─ Runtime environment (Lambda)                              ║
║  ├─ Operating system updates                                  ║
║  └─ Automatic backups and replication                         ║
║                                                               ║
║  GET PROOF OF COMPLIANCE:                                     ║
║  └─ AWS Artifact for reports and certifications               ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

## Next Steps

Continue to the next section to learn about **Customer Responsibilities** - what YOU need to secure when using AWS services.

# 🖥️ AWS End User Computing

## File Structure

```
lesson-16-other-aws-services/
└── 04-end-user-computing/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS End User Computing services enable organizations to provide secure, managed desktop and application experiences to their users from anywhere. These services eliminate the need for traditional on-premises desktop infrastructure while providing the flexibility, security, and scalability of the cloud. For the AWS Cloud Practitioner exam, understanding the differences between these services and their use cases is important.

## End User Computing Overview

```
+------------------------------------------------------------------+
|                    END USER COMPUTING SERVICES                    |
+------------------------------------------------------------------+
|                                                                   |
|   TRADITIONAL IT                    AWS END USER COMPUTING        |
|   ┌──────────────────────────┐     ┌──────────────────────────┐   |
|   │                          │     │                          │   |
|   │  Physical PCs            │     │  WorkSpaces (VDI)        │   |
|   │  • Hardware management   │     │  • Cloud desktops        │   |
|   │  • Software updates      │     │  • No hardware to manage │   |
|   │  • Security patches      │     │  • Centralized security  │   |
|   │  • Physical security     │     │  • Access from anywhere  │   |
|   │                          │     │                          │   |
|   │  Installed Applications  │     │  AppStream 2.0           │   |
|   │  • License management    │     │  • Stream applications   │   |
|   │  • Compatibility issues  │     │  • No installation       │   |
|   │  • Version control       │     │  • Browser-based access  │   |
|   │                          │     │                          │   |
|   └──────────────────────────┘     └──────────────────────────┘   |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon WorkSpaces

Amazon WorkSpaces is a fully managed, persistent Desktop-as-a-Service (DaaS) solution that provides users with virtual Windows or Linux desktops.

```
+------------------------------------------------------------------+
|                      AMAZON WORKSPACES                            |
+------------------------------------------------------------------+
|                                                                   |
|   USER DEVICES                    AWS CLOUD                       |
|                                   ┌─────────────────────────────┐ |
|   ┌─────────┐                     │       WorkSpaces            │ |
|   │ Windows │                     │  ┌─────────────────────┐    │ |
|   │ Laptop  │ ────┐               │  │  ┌─────┐  ┌─────┐   │    │ |
|   └─────────┘     │               │  │  │ WS1 │  │ WS2 │   │    │ |
|   ┌─────────┐     │               │  │  │Win11│  │Linux│   │    │ |
|   │   Mac   │ ────┤               │  │  └─────┘  └─────┘   │    │ |
|   │         │     │   Internet    │  │        ▼            │    │ |
|   └─────────┘     │──────────────▶│  │  ┌───────────┐      │    │ |
|   ┌─────────┐     │               │  │  │ User Data │      │    │ |
|   │  iPad   │ ────┤               │  │  │(Persistent│      │    │ |
|   │         │     │               │  │  │   EBS)    │      │    │ |
|   └─────────┘     │               │  │  └───────────┘      │    │ |
|   ┌─────────┐     │               │  └─────────────────────┘    │ |
|   │ Browser │ ────┘               │                             │ |
|   │(Web App)│                     │  Directory Service          │ |
|   └─────────┘                     │  (AD / Simple AD)           │ |
|                                   └─────────────────────────────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

### WorkSpaces Key Features

| Feature | Description |
|---------|-------------|
| Persistent Desktop | User data and settings saved between sessions |
| Operating Systems | Windows 10/11, Amazon Linux 2, Ubuntu |
| Directory Integration | AWS Directory Service, Microsoft AD, AD Connector |
| Client Applications | Windows, Mac, Linux, iOS, Android, Web |
| Streaming Protocol | PCoIP or WSP (WorkSpaces Streaming Protocol) |
| Auto-Start/Stop | Start when user connects, stop when idle |
| Multi-Factor Auth | MFA support with RADIUS integration |

### WorkSpaces Bundle Options

| Bundle Type | vCPU | Memory | Root | User | Use Case |
|-------------|------|--------|------|------|----------|
| Value | 1 | 2 GB | 80 GB | 10 GB | Light tasks |
| Standard | 2 | 4 GB | 80 GB | 50 GB | Office productivity |
| Performance | 2 | 8 GB | 80 GB | 100 GB | Development |
| Power | 4 | 16 GB | 175 GB | 100 GB | Power users |
| PowerPro | 8 | 32 GB | 175 GB | 100 GB | Data analysis |
| Graphics.g4dn | 4 | 16 GB | 100 GB | 100 GB | Graphics, CAD |
| GraphicsPro.g4dn | 16 | 128 GB | 100 GB | 100 GB | 3D rendering |

### WorkSpaces Pricing Models

| Model | Description | Best For |
|-------|-------------|----------|
| **AlwaysOn** | Fixed monthly fee | Full-time employees, heavy users |
| **AutoStop** | Monthly fee + hourly usage | Part-time, occasional users |

```
+------------------------------------------------------------------+
|                   WORKSPACES PRICING COMPARISON                   |
+------------------------------------------------------------------+
|                                                                   |
|   AlwaysOn (Monthly)              AutoStop (Hourly)               |
|   ┌─────────────────────┐        ┌─────────────────────┐          |
|   │                     │        │                     │          |
|   │  Fixed Monthly Fee  │        │  Base Fee +         │          |
|   │  $XX/month          │        │  Hourly Usage       │          |
|   │                     │        │  $X/month +         │          |
|   │  24/7 Access        │        │  $0.XX/hour         │          |
|   │                     │        │                     │          |
|   │  Best for: 80+      │        │  Best for: <80      │          |
|   │  hours/month        │        │  hours/month        │          |
|   │                     │        │                     │          |
|   └─────────────────────┘        └─────────────────────┘          |
|                                                                   |
+------------------------------------------------------------------+
```

### WorkSpaces Use Cases

| Use Case | Description |
|----------|-------------|
| Remote Workers | Provide secure desktops to work-from-home employees |
| Contractors | Temporary access without provisioning hardware |
| BYOD | Secure access from personal devices |
| Mergers & Acquisitions | Quick desktop provisioning for new employees |
| Call Centers | Standardized environments for agents |
| Compliance | Centralized data, meets regulatory requirements |

## Amazon AppStream 2.0

Amazon AppStream 2.0 is a fully managed application streaming service that provides users with instant access to desktop applications from anywhere.

```
+------------------------------------------------------------------+
|                     AMAZON APPSTREAM 2.0                          |
+------------------------------------------------------------------+
|                                                                   |
|   APPLICATION STREAMING (Not a full desktop)                      |
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                       AWS CLOUD                              │ |
|   │  ┌───────────────────────────────────────────────────────┐  │ |
|   │  │                  AppStream Fleet                       │  │ |
|   │  │  ┌─────────────────────────────────────────────────┐  │  │ |
|   │  │  │  Image (Applications installed)                  │  │  │ |
|   │  │  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐│  │  │ |
|   │  │  │  │ AutoCAD │ │ Matlab  │ │ SPSS    │ │ Custom  ││  │  │ |
|   │  │  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘│  │  │ |
|   │  │  └─────────────────────────────────────────────────┘  │  │ |
|   │  └───────────────────────────────────────────────────────┘  │ |
|   │                           │                                  │ |
|   │                           │ Stream                           │ |
|   │                           ▼                                  │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                               │                                   |
|              ┌────────────────┼────────────────┐                  |
|              ▼                ▼                ▼                  |
|         ┌─────────┐     ┌─────────┐     ┌─────────┐               |
|         │ Browser │     │ Browser │     │ Browser │               |
|         │(Laptop) │     │(Tablet) │     │ (Any)   │               |
|         └─────────┘     └─────────┘     └─────────┘               |
|                                                                   |
|   Only need: HTML5-compatible web browser                         |
|                                                                   |
+------------------------------------------------------------------+
```

### AppStream 2.0 Key Features

| Feature | Description |
|---------|-------------|
| Browser Access | HTML5 browser, no plugins required |
| Non-Persistent | Sessions are stateless (unless home folders enabled) |
| Fleet Types | Always-On, On-Demand, Elastic fleets |
| SAML 2.0 | Federated authentication support |
| Home Folders | Optional persistent storage in S3 |
| Application Catalog | Present applications in a portal |

### AppStream 2.0 Components

| Component | Description |
|-----------|-------------|
| Image | Contains installed applications |
| Image Builder | EC2 instance to create custom images |
| Fleet | Group of streaming instances |
| Stack | Configuration (fleet + settings + access) |
| User Pool | Manage users and authentication |

### AppStream 2.0 Fleet Types

| Fleet Type | Description | Use Case |
|------------|-------------|----------|
| **Always-On** | Instances always running | Instant access, predictable usage |
| **On-Demand** | Start when user connects | Cost savings, variable usage |
| **Elastic** | Auto-scale based on demand | Variable workloads |

### AppStream 2.0 Use Cases

| Use Case | Description |
|----------|-------------|
| Software Trials | Provide trial access to applications |
| Training | Deliver training environments |
| Design & Engineering | Stream CAD and graphics applications |
| Healthcare | HIPAA-compliant application access |
| Education | Deliver software to students |
| Legacy Applications | Run apps incompatible with modern OS |

## WorkSpaces vs AppStream 2.0 Comparison

```
+------------------------------------------------------------------+
|              WORKSPACES VS APPSTREAM 2.0                          |
+------------------------------------------------------------------+
|                                                                   |
|   WORKSPACES                        APPSTREAM 2.0                 |
|   ┌─────────────────────────┐      ┌─────────────────────────┐    |
|   │                         │      │                         │    |
|   │   Full Desktop          │      │   Application Only      │    |
|   │   ┌─────────────────┐   │      │   ┌─────────────────┐   │    |
|   │   │  Windows/Linux  │   │      │   │     App Icon    │   │    |
|   │   │  ┌─────┐┌─────┐ │   │      │   │                 │   │    |
|   │   │  │Word ││Excel│ │   │      │   │  Single App or  │   │    |
|   │   │  └─────┘└─────┘ │   │      │   │  App Catalog    │   │    |
|   │   │  Desktop Icons  │   │      │   │                 │   │    |
|   │   │  Settings       │   │      │   └─────────────────┘   │    |
|   │   │  Files          │   │      │                         │    |
|   │   └─────────────────┘   │      │   No OS, No Desktop     │    |
|   │                         │      │                         │    |
|   │   Persistent            │      │   Non-Persistent        │    |
|   │   1:1 User:Desktop      │      │   N:1 Users:Instances   │    |
|   │                         │      │                         │    |
|   └─────────────────────────┘      └─────────────────────────┘    |
|                                                                   |
+------------------------------------------------------------------+
```

### Detailed Feature Comparison

| Feature | WorkSpaces | AppStream 2.0 |
|---------|------------|---------------|
| **Type** | Full virtual desktop (VDI) | Application streaming |
| **Persistence** | Persistent (data saved) | Non-persistent (stateless) |
| **Access** | Native clients + Web | Web browser only |
| **User Mapping** | 1 user = 1 WorkSpace | Multiple users share fleet |
| **OS Experience** | Full Windows/Linux | Application window only |
| **Storage** | EBS volumes (root + user) | S3 home folders (optional) |
| **Use Case** | Replace physical desktops | Deliver specific applications |
| **Client Install** | Client app or browser | No install needed |

### When to Choose Which Service

| Choose WorkSpaces When | Choose AppStream 2.0 When |
|------------------------|---------------------------|
| Users need full desktop experience | Users need specific applications only |
| Persistent data and settings required | Sessions can be stateless |
| Users work in the OS environment | Browser-only access preferred |
| 1:1 user-to-desktop ratio needed | Applications are resource-intensive |
| Replace traditional VDI | Deliver trials or training |

## Security Features

| Feature | WorkSpaces | AppStream 2.0 |
|---------|------------|---------------|
| Encryption at Rest | EBS encryption | S3 encryption |
| Encryption in Transit | PCoIP/WSP | HTTPS |
| MFA | RADIUS integration | SAML 2.0 |
| Network | VPC deployment | VPC deployment |
| Compliance | HIPAA, PCI, SOC | HIPAA, PCI, SOC |

## Cost Optimization Tips

```
+------------------------------------------------------------------+
|                    COST OPTIMIZATION TIPS                         |
+------------------------------------------------------------------+
|                                                                   |
|   WORKSPACES:                                                     |
|   • Use AutoStop for users with <80 hours/month usage             |
|   • Right-size bundles based on actual needs                      |
|   • Use Bring Your Own License (BYOL) for Windows                 |
|   • Auto-stop idle WorkSpaces                                     |
|                                                                   |
|   APPSTREAM 2.0:                                                  |
|   • Use On-Demand fleets for variable usage                       |
|   • Use Elastic fleets for unpredictable demand                   |
|   • Schedule fleet scaling based on business hours                |
|   • Share instances across users (N:1 ratio)                      |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **WorkSpaces** = Full virtual desktop (VDI), persistent, like having a cloud PC
- **AppStream 2.0** = Application streaming, non-persistent, browser-only access
- WorkSpaces users get **dedicated desktops**; AppStream users **share fleet instances**
- WorkSpaces data is **persistent** (EBS); AppStream is **stateless** (optional S3)
- WorkSpaces has **native clients** + web; AppStream is **browser-only**
- WorkSpaces = replace physical desktops; AppStream = deliver specific applications
- Both support **VPC deployment** for network security
- Both are **HIPAA, PCI, SOC compliant**
- WorkSpaces pricing: **AlwaysOn** (monthly) or **AutoStop** (hourly)
- AppStream pricing: **Always-On**, **On-Demand**, or **Elastic** fleets
- Remember: WorkSpaces = **Desktops**, AppStream = **Applications**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| VDI | Virtual Desktop Infrastructure - running desktops in a data center |
| DaaS | Desktop as a Service - cloud-hosted virtual desktops |
| Persistent | Data and settings saved between sessions |
| Non-Persistent | Session data discarded after logout |
| Fleet | Group of streaming instances in AppStream |
| Bundle | Pre-configured hardware for WorkSpaces |
| PCoIP | PC-over-IP protocol for remote desktop streaming |
| WSP | WorkSpaces Streaming Protocol - AWS proprietary protocol |
| BYOD | Bring Your Own Device - using personal devices for work |
| Image Builder | Tool to create custom AppStream images |

## 💡 Key Takeaways

1. Amazon WorkSpaces provides fully managed, persistent virtual desktops
2. WorkSpaces supports Windows and Linux with various hardware bundles
3. WorkSpaces is accessed via native clients or web browser
4. Amazon AppStream 2.0 streams applications through a web browser only
5. AppStream 2.0 is non-persistent by default (stateless sessions)
6. WorkSpaces assigns one desktop per user; AppStream shares fleet instances
7. Choose WorkSpaces when users need a full desktop experience
8. Choose AppStream when delivering specific applications
9. Both services support VPC deployment and encryption
10. Both are compliant with HIPAA, PCI, and SOC standards
11. Cost optimization involves right-sizing and appropriate pricing models

---

[Previous: 03 - Developer Tools](../03-developer-tools/readme.md) | [Next: 05 - Frontend Web and Mobile](../05-frontend-web-and-mobile/readme.md)

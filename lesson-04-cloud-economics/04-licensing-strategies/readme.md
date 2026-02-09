# Licensing Strategies in AWS

## Overview

Software licensing in the cloud differs significantly from traditional on-premises licensing. AWS offers multiple licensing options that can help organizations **optimize costs** and **maintain compliance** when migrating or running workloads in the cloud.

## Licensing Models

| Model | Description | Cost Impact |
|-------|-------------|-------------|
| **BYOL** | Bring Your Own License | Use existing licenses, potentially lower AWS costs |
| **License Included** | License bundled with AWS service | Simpler management, pay-as-you-go |
| **AWS License Manager** | Centralized license management | Visibility and control |
| **License Mobility** | Move licenses to AWS | Maximize existing investments |

## Bring Your Own License (BYOL)

### What is BYOL?

BYOL allows you to use your existing software licenses on AWS infrastructure, rather than purchasing new licenses.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         BYOL Model                                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ┌───────────────┐          ┌───────────────────────────────┐          │
│   │  Existing     │          │         AWS Cloud             │          │
│   │  Licenses     │ ──────►  │  ┌───────────────────────┐   │          │
│   │               │          │  │   EC2 Instance        │   │          │
│   │  • Windows    │  BYOL    │  │   ┌─────────────────┐ │   │          │
│   │  • SQL Server │ ──────►  │  │   │ Your Software   │ │   │          │
│   │  • Oracle     │          │  │   │ (Your License)  │ │   │          │
│   │               │          │  │   └─────────────────┘ │   │          │
│   └───────────────┘          │  └───────────────────────┘   │          │
│                              └───────────────────────────────┘          │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### BYOL Requirements

| Requirement | Description |
|-------------|-------------|
| **Software Assurance** | Often required for Microsoft products |
| **Dedicated Hosts/Instances** | May be required for license compliance |
| **License Agreement** | Must allow cloud deployment |
| **Tracking** | Customer responsible for compliance |

### Common BYOL Scenarios

- **Microsoft Windows Server** with Software Assurance
- **Microsoft SQL Server** licenses
- **Oracle Database** licenses
- **SAP** licenses
- **VMware** licenses

## License Included Model

### What is License Included?

AWS includes the software license in the hourly/per-second pricing of the service.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    License Included Model                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   AWS Service Pricing = Compute Cost + License Cost                     │
│                                                                          │
│   ┌────────────────────────────────────────────────────────────┐        │
│   │                                                             │        │
│   │   EC2 with Windows Server                                   │        │
│   │   ────────────────────────                                  │        │
│   │   $0.10/hr (compute) + $0.05/hr (Windows) = $0.15/hr       │        │
│   │                                                             │        │
│   │   RDS with SQL Server                                       │        │
│   │   ─────────────────────                                     │        │
│   │   $0.20/hr (compute) + $0.15/hr (SQL license) = $0.35/hr   │        │
│   │                                                             │        │
│   └────────────────────────────────────────────────────────────┘        │
│                                                                          │
│   Benefits: Simple, No tracking, Pay-as-you-go, No upfront              │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### License Included Advantages

1. **Simplified management** - No license tracking required
2. **Pay-as-you-go** - Only pay when using the software
3. **Always compliant** - AWS handles licensing
4. **No upfront costs** - No license purchases needed
5. **Flexibility** - Scale up/down without license concerns

## AWS License Manager

### What is AWS License Manager?

AWS License Manager is a service that helps you manage software licenses across AWS and on-premises environments.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    AWS License Manager                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│              ┌─────────────────────────────────┐                        │
│              │      AWS License Manager        │                        │
│              │                                 │                        │
│              │   • Track license usage         │                        │
│              │   • Enforce limits              │                        │
│              │   • Prevent violations          │                        │
│              │   • Centralized dashboard       │                        │
│              └─────────────────────────────────┘                        │
│                           │                                              │
│         ┌─────────────────┼─────────────────┐                          │
│         ▼                 ▼                 ▼                           │
│   ┌───────────┐    ┌───────────┐    ┌───────────┐                      │
│   │  EC2      │    │   RDS     │    │On-Premises│                      │
│   │ Instances │    │ Databases │    │  Servers  │                      │
│   └───────────┘    └───────────┘    └───────────┘                      │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Key Features

| Feature | Description |
|---------|-------------|
| **License Rules** | Define licensing terms and conditions |
| **Automated Discovery** | Find software across your environment |
| **Usage Tracking** | Monitor license consumption |
| **Alerts** | Notify when approaching limits |
| **Reporting** | Compliance and audit reports |
| **Cross-Account** | Manage licenses across AWS Organizations |

### Use Cases

- Track Windows Server licenses across EC2 instances
- Manage Oracle license compliance
- Monitor SQL Server deployment
- Control software deployment limits
- Audit license usage for compliance

## License Mobility

### What is License Mobility?

License Mobility allows customers to move their existing on-premises server application licenses to AWS without additional licensing fees.

```
┌─────────────────────────────────────────────────────────────────────────┐
│                       License Mobility                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   On-Premises                              AWS Cloud                     │
│   ────────────────                         ──────────────                │
│                                                                          │
│   ┌─────────────────┐                     ┌─────────────────┐           │
│   │                 │                     │                 │           │
│   │  SQL Server     │    ──────────►      │  SQL Server     │           │
│   │  (Licensed)     │    License          │  on EC2         │           │
│   │                 │    Mobility         │  (Same License) │           │
│   └─────────────────┘                     └─────────────────┘           │
│                                                                          │
│   Requirements:                                                          │
│   • Active Software Assurance                                           │
│   • Eligible products (most server apps)                                │
│   • License Mobility verification                                        │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

### Eligible Products

Microsoft License Mobility through Software Assurance covers:

- SQL Server
- Exchange Server
- SharePoint Server
- Skype for Business Server
- System Center servers
- Dynamics applications

**Note**: Windows Server and Windows Desktop are NOT eligible for License Mobility (requires Dedicated Host for BYOL).

## Licensing Comparison

| Aspect | BYOL | License Included | License Mobility |
|--------|------|------------------|------------------|
| **Use Existing License** | Yes | No | Yes |
| **AWS Manages License** | No | Yes | No |
| **Compliance Tracking** | Customer | AWS | Customer |
| **Upfront Investment** | Already made | None | Already made |
| **Flexibility** | Lower | Higher | Lower |
| **Best For** | Large existing investments | New deployments | Migration scenarios |

## Dedicated Hosts for Licensing

### Why Dedicated Hosts?

Some software licenses require physical server visibility (socket/core counting). **Amazon EC2 Dedicated Hosts** provide:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    EC2 Dedicated Hosts                                   │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Standard EC2                      Dedicated Host                       │
│   ─────────────                     ─────────────────                   │
│                                                                          │
│   ┌─────────────────┐              ┌─────────────────┐                  │
│   │ Shared Physical │              │ Your Physical   │                  │
│   │ Server          │              │ Server          │                  │
│   │                 │              │                 │                  │
│   │  ┌───┐ ┌───┐   │              │  ┌───┐ ┌───┐   │                  │
│   │  │VM │ │VM │   │              │  │VM │ │VM │   │                  │
│   │  │You│ │Oth│   │              │  │You│ │You│   │                  │
│   │  └───┘ └───┘   │              │  └───┘ └───┘   │                  │
│   └─────────────────┘              └─────────────────┘                  │
│                                                                          │
│   Dedicated Host Benefits:                                              │
│   • Socket/core visibility for licensing                                │
│   • Consistent placement                                                │
│   • Required for Windows Server BYOL                                    │
│   • Required for some Oracle/SQL licenses                               │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Cost Optimization Strategies

### Choosing the Right Model

```
┌─────────────────────────────────────────────────────────────────────────┐
│                 Licensing Decision Matrix                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   Do you have existing licenses?                                        │
│         │                                                                │
│         ├── NO ──► Use License Included (simplest)                      │
│         │                                                                │
│         └── YES ─┬─► Are they transferable?                             │
│                  │         │                                             │
│                  │         ├── NO ──► Use License Included              │
│                  │         │                                             │
│                  │         └── YES ─┬─► Is BYOL cheaper?                │
│                  │                  │         │                          │
│                  │                  │         ├── YES ──► Use BYOL      │
│                  │                  │         │                          │
│                  │                  │         └── NO ──► License Incl.  │
│                  │                                                       │
└─────────────────────────────────────────────────────────────────────────┘
```

### Cost Considerations

| Factor | BYOL | License Included |
|--------|------|------------------|
| **EC2 hourly cost** | Lower (no license) | Higher (includes license) |
| **Dedicated Host** | May be required | Not required |
| **Management overhead** | Higher | Lower |
| **Total Cost** | Calculate carefully | Straightforward |

## Exam Tips

- **BYOL** = Bring Your Own License - use existing licenses on AWS
- **License Included** = AWS includes license in service price
- **AWS License Manager** = centralized license tracking and compliance
- **License Mobility** = Microsoft program to move licenses to AWS
- **Dedicated Hosts** = physical servers for socket/core-based licensing
- **Software Assurance** = often required for BYOL Microsoft products
- Know that **Windows Server BYOL requires Dedicated Hosts**
- **License Manager** works across AWS and on-premises

## Key Takeaways

1. **BYOL** allows using existing licenses on AWS to reduce costs
2. **License Included** simplifies management with pay-as-you-go licensing
3. **AWS License Manager** provides centralized license management and compliance
4. **License Mobility** through Software Assurance enables migration scenarios
5. **Dedicated Hosts** required for certain BYOL scenarios (socket/core licensing)
6. Choose licensing model based on **existing investments** and **total cost**
7. **License Manager** helps prevent compliance violations

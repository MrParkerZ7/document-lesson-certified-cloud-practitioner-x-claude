# AWS Cloud Adoption Framework (AWS CAF)

## Overview

The **AWS Cloud Adoption Framework (AWS CAF)** provides guidance that supports each unit in your organization as you digitally transform and accelerate your cloud journey. It helps you understand how cloud adoption transforms the way you work and provides structure to identify and address gaps in skills and processes.

## What is AWS CAF?

AWS CAF organizes guidance into six areas of focus, called **Perspectives**. Each Perspective covers distinct responsibilities owned or managed by functionally related stakeholders.

## The Six Perspectives

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    AWS Cloud Adoption Framework                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   BUSINESS CAPABILITIES                    TECHNICAL CAPABILITIES        │
│   ┌──────────────────────┐                ┌──────────────────────┐      │
│   │      Business        │                │      Platform        │      │
│   │                      │                │                      │      │
│   │  CxO, Finance,       │                │  CTO, Architects,    │      │
│   │  Business Managers   │                │  Engineers           │      │
│   └──────────────────────┘                └──────────────────────┘      │
│                                                                          │
│   ┌──────────────────────┐                ┌──────────────────────┐      │
│   │       People         │                │      Security        │      │
│   │                      │                │                      │      │
│   │  HR, Training,       │                │  CISO, Security      │      │
│   │  Org Change          │                │  Analysts            │      │
│   └──────────────────────┘                └──────────────────────┘      │
│                                                                          │
│   ┌──────────────────────┐                ┌──────────────────────┐      │
│   │     Governance       │                │     Operations       │      │
│   │                      │                │                      │      │
│   │  CIO, Program Mgrs,  │                │  IT Ops, Support,    │      │
│   │  Enterprise Arch     │                │  Incident Response   │      │
│   └──────────────────────┘                └──────────────────────┘      │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Detailed Perspective Breakdown

### Business Perspectives (Left Side)

| Perspective | Stakeholders | Focus Areas |
|-------------|--------------|-------------|
| **Business** | CxO, Finance, Business Managers | Strategy, outcomes, financial management |
| **People** | HR, Training, Organizational Change | Culture, leadership, workforce transformation |
| **Governance** | CIO, Program Managers, Enterprise Architects | Governance, risk, compliance, program management |

### Technical Perspectives (Right Side)

| Perspective | Stakeholders | Focus Areas |
|-------------|--------------|-------------|
| **Platform** | CTO, Architects, Engineers | Infrastructure, CI/CD, provisioning |
| **Security** | CISO, Security Analysts | Security operations, identity, compliance |
| **Operations** | IT Ops, Support Teams | Observability, incident management, AIOps |

## CAF Foundational Capabilities

### Business Perspective Capabilities
- **Strategy Management** - Align cloud strategy with business objectives
- **Portfolio Management** - Manage product and service portfolios
- **Innovation Management** - Foster innovation culture
- **Product Management** - Product development and management
- **Strategic Partnership** - Manage partner relationships
- **Data Monetization** - Extract value from data assets
- **Business Insight** - Data-driven decision making
- **Data Science** - Analytics and ML capabilities

### People Perspective Capabilities
- **Culture Evolution** - Shift organizational culture
- **Transformational Leadership** - Leadership development
- **Cloud Fluency** - Cloud skills across organization
- **Workforce Transformation** - Upskilling and reskilling
- **Change Acceleration** - Manage change effectively
- **Organization Design** - Align structure with strategy
- **Organizational Alignment** - Cross-team collaboration

### Governance Perspective Capabilities
- **Program and Project Management** - Delivery management
- **Benefits Management** - Track and realize benefits
- **Risk Management** - Identify and mitigate risks
- **Cloud Financial Management** - Cost optimization
- **Application Portfolio Management** - App inventory and prioritization
- **Data Governance** - Data quality and compliance
- **Data Curation** - Data lifecycle management

### Platform Perspective Capabilities
- **Platform Architecture** - Design scalable platforms
- **Data Architecture** - Design data solutions
- **Platform Engineering** - Build and maintain platforms
- **Data Engineering** - Build data pipelines
- **Provisioning and Orchestration** - Automate deployments
- **Modern Application Development** - Cloud-native development
- **CI/CD** - Continuous integration and delivery

### Security Perspective Capabilities
- **Security Governance** - Security policies and procedures
- **Security Assurance** - Compliance and audit
- **Identity and Access Management** - IAM controls
- **Threat Detection** - Security monitoring
- **Vulnerability Management** - Patch and remediate
- **Infrastructure Protection** - Network and endpoint security
- **Data Protection** - Encryption and data security
- **Application Security** - Secure development
- **Incident Response** - Security event management

### Operations Perspective Capabilities
- **Observability** - Monitoring and logging
- **Event Management (AIOps)** - AI-powered operations
- **Incident and Problem Management** - Issue resolution
- **Change and Release Management** - Safe deployments
- **Performance and Capacity Management** - Resource optimization
- **Configuration Management** - Maintain configurations
- **Patch Management** - Keep systems updated
- **Availability and Continuity Management** - Uptime assurance
- **Application Management** - App lifecycle management

## CAF Transformation Domains

```
┌────────────────────────────────────────────────────────────────────────┐
│                    Four Transformation Domains                          │
├────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ┌─────────────────────┐    ┌─────────────────────┐                  │
│   │    Technology       │    │      Process        │                  │
│   │   Transformation    │    │   Transformation    │                  │
│   │                     │    │                     │                  │
│   │ Migrate & modernize │    │ Digitize & automate │                  │
│   │ infrastructure      │    │ business operations │                  │
│   └─────────────────────┘    └─────────────────────┘                  │
│                                                                         │
│   ┌─────────────────────┐    ┌─────────────────────┐                  │
│   │   Organization      │    │      Product        │                  │
│   │   Transformation    │    │   Transformation    │                  │
│   │                     │    │                     │                  │
│   │ Reimagine operating │    │ Reimagine business  │                  │
│   │ model               │    │ model               │                  │
│   └─────────────────────┘    └─────────────────────┘                  │
│                                                                         │
└────────────────────────────────────────────────────────────────────────┘
```

## Cloud Transformation Journey Phases

| Phase | Description |
|-------|-------------|
| **Envision** | Demonstrate how cloud accelerates business outcomes |
| **Align** | Identify capability gaps and stakeholder concerns |
| **Launch** | Deliver pilot initiatives with value |
| **Scale** | Expand production pilots and business value |

## Exam Tips

- AWS CAF has **6 Perspectives**: Business, People, Governance, Platform, Security, Operations
- **Business capabilities** (left): Business, People, Governance
- **Technical capabilities** (right): Platform, Security, Operations
- Each perspective has specific **stakeholders** (know who owns what)
- **4 transformation domains**: Technology, Process, Organization, Product
- **4 transformation phases**: Envision, Align, Launch, Scale

## Key Takeaways

1. AWS CAF helps organizations **structure their cloud adoption** journey
2. **Six Perspectives** cover both business and technical considerations
3. Each perspective has distinct **stakeholders and capabilities**
4. Use CAF to identify **skill and process gaps**
5. The framework supports **digital transformation** holistically
6. **Governance** perspective covers compliance and risk management

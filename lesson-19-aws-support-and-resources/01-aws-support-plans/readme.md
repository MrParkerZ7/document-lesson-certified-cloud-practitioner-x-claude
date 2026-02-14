# 🆘 AWS Support Plans

## File Structure

```
lesson-19-aws-support-and-resources/
└── 01-aws-support-plans/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS offers five different support plans designed to meet various customer needs, from individual developers to large enterprises running mission-critical workloads. Understanding the differences between these plans, including features, response times, and pricing, is essential for the AWS Certified Cloud Practitioner exam.

## Overview of AWS Support Plans

AWS provides five tiers of support:

```
┌────────────────────────────────────────────────────────────────────────────┐
│                         AWS SUPPORT PLANS TIERS                            │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│   ┌─────────────┐                                                          │
│   │ ENTERPRISE  │ ◄── Mission-critical workloads (TAM, 15 min response)   │
│   ├─────────────┤                                                          │
│   │ ENTERPRISE  │ ◄── Production workloads (TAM pool, 30 min response)    │
│   │  ON-RAMP    │                                                          │
│   ├─────────────┤                                                          │
│   │  BUSINESS   │ ◄── Production workloads (1 hour response)              │
│   ├─────────────┤                                                          │
│   │  DEVELOPER  │ ◄── Development/testing (12-24 hour response)           │
│   ├─────────────┤                                                          │
│   │   BASIC     │ ◄── Free tier (no technical support)                    │
│   └─────────────┘                                                          │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## Detailed Plan Comparison

### 1. Basic Support (Free)

**Included with all AWS accounts at no additional cost.**

| Feature | Availability |
|---------|--------------|
| 24/7 Customer Service | Account and billing questions only |
| Documentation & Whitepapers | Full access |
| AWS Trusted Advisor | 7 core checks only |
| AWS Personal Health Dashboard | Full access |
| Technical Support | Not included |

### 2. Developer Support

**Ideal for testing and development environments.**

| Feature | Availability |
|---------|--------------|
| Everything in Basic | Yes |
| Business Hours Email Support | Cloud Support Associates |
| General Guidance | < 24 business hours |
| System Impaired | < 12 business hours |
| Number of Contacts | 1 primary contact |
| AWS Trusted Advisor | 7 core checks only |

**Pricing:** Greater of $29/month OR 3% of monthly AWS usage

### 3. Business Support

**Recommended for production workloads.**

| Feature | Availability |
|---------|--------------|
| Everything in Developer | Yes |
| 24/7 Phone, Email, Chat | Cloud Support Engineers |
| Production System Impaired | < 4 hours |
| Production System Down | < 1 hour |
| Unlimited Contacts | Via IAM |
| AWS Trusted Advisor | Full checks |
| Third-party Software Support | Interoperability guidance |
| Infrastructure Event Management | Additional fee |

**Pricing:** Greater of $100/month OR tiered percentage (10%-3%)

### 4. Enterprise On-Ramp Support

**For businesses with production and/or business critical workloads.**

| Feature | Availability |
|---------|--------------|
| Everything in Business | Yes |
| Business-Critical System Down | < 30 minutes |
| Technical Account Manager (TAM) | Pool of TAMs |
| Concierge Support Team | Billing and account experts |
| Infrastructure Event Management | One per year (included) |
| Proactive Support Programs | Partial access |

**Pricing:** Greater of $5,500/month OR tiered percentage

### 5. Enterprise Support

**For mission-critical workloads.**

| Feature | Availability |
|---------|--------------|
| Everything in Enterprise On-Ramp | Yes |
| Business-Critical System Down | < 15 minutes |
| Designated TAM | Dedicated Technical Account Manager |
| Infrastructure Event Management | Unlimited (included) |
| Proactive Support Programs | Full access |
| Training | Self-paced labs |
| Operations Reviews | Well-Architected reviews |

**Pricing:** Greater of $15,000/month OR tiered percentage

## Response Time Comparison

| Severity Level | Basic | Developer | Business | Enterprise On-Ramp | Enterprise |
|----------------|-------|-----------|----------|-------------------|------------|
| General Guidance | N/A | < 24 hours | < 24 hours | < 24 hours | < 24 hours |
| System Impaired | N/A | < 12 hours | < 12 hours | < 12 hours | < 12 hours |
| Production System Impaired | N/A | N/A | < 4 hours | < 4 hours | < 4 hours |
| Production System Down | N/A | N/A | < 1 hour | < 1 hour | < 1 hour |
| Business-Critical System Down | N/A | N/A | N/A | < 30 minutes | < 15 minutes |

## Key Features by Plan

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    KEY FEATURES AVAILABILITY MATRIX                          │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Feature               Basic  Developer  Business  EntOnRamp  Enterprise    │
│  ──────────────────────────────────────────────────────────────────────────  │
│  24/7 Tech Support       ✗       ✗          ✓          ✓          ✓         │
│  Phone Support           ✗       ✗          ✓          ✓          ✓         │
│  Full Trusted Advisor    ✗       ✗          ✓          ✓          ✓         │
│  TAM                     ✗       ✗          ✗          Pool       Dedicated │
│  Concierge Support       ✗       ✗          ✗          ✓          ✓         │
│  Infrastructure Event    ✗       ✗          $$$        1/year     Unlimited │
│  Proactive Reviews       ✗       ✗          ✗          Partial    Full      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Technical Account Manager (TAM)

The TAM is a designated technical point of contact who provides:

- **Proactive guidance** on AWS best practices
- **Advocacy** within AWS on your behalf
- **Architectural reviews** and optimization recommendations
- **Coordination** with AWS service teams
- **Incident management** support
- **Training** and education

**Available in:** Enterprise On-Ramp (pool) and Enterprise (dedicated)

## AWS Concierge Support Team

Available for Enterprise On-Ramp and Enterprise customers:

- **Billing and account expertise**
- **Help with payment inquiries**
- **Service limit increases**
- **Reserved Instance purchasing assistance**
- **Account consolidation guidance**

## Trusted Advisor Access

| Plan | Trusted Advisor Access |
|------|----------------------|
| Basic | 7 core security checks |
| Developer | 7 core security checks |
| Business | All checks (5 categories) |
| Enterprise On-Ramp | All checks + API access |
| Enterprise | All checks + API access |

## Pricing Structure

| Plan | Minimum Monthly | Percentage Calculation |
|------|-----------------|----------------------|
| Basic | $0 | N/A |
| Developer | $29 | 3% of monthly usage |
| Business | $100 | 10% (first $10K) → 3% (over $500K) |
| Enterprise On-Ramp | $5,500 | Tiered percentage |
| Enterprise | $15,000 | Tiered percentage |

## Choosing the Right Plan

```
┌────────────────────────────────────────────────────────────────────────────┐
│                     SUPPORT PLAN DECISION GUIDE                            │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Learning/Experimenting?                                                   │
│         │                                                                  │
│         └──► BASIC (Free)                                                  │
│                                                                            │
│  Development/Testing Environment?                                          │
│         │                                                                  │
│         └──► DEVELOPER ($29+)                                              │
│                                                                            │
│  Production Workloads?                                                     │
│         │                                                                  │
│         └──► BUSINESS ($100+)                                              │
│                                                                            │
│  Business-Critical + Need TAM?                                             │
│         │                                                                  │
│         └──► ENTERPRISE ON-RAMP ($5,500+)                                  │
│                                                                            │
│  Mission-Critical + Dedicated Support?                                     │
│         │                                                                  │
│         └──► ENTERPRISE ($15,000+)                                         │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

## 🎯 Exam Tips

- **Basic Support** is included FREE with all AWS accounts
- **Developer Support** offers business hours email support only (no phone)
- **Business Support** is the MINIMUM plan for 24/7 phone support
- **Business Support** unlocks FULL AWS Trusted Advisor checks
- **TAM (Technical Account Manager)** is only available in Enterprise plans
- Enterprise On-Ramp has a **pool of TAMs**, Enterprise has a **dedicated TAM**
- **Concierge Support Team** is available in Enterprise On-Ramp and Enterprise
- Response times: Enterprise = 15 min, Enterprise On-Ramp = 30 min, Business = 1 hour
- Know the **pricing minimums**: Developer=$29, Business=$100, EntOnRamp=$5,500, Enterprise=$15,000

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| TAM | Technical Account Manager - dedicated AWS expert for Enterprise customers |
| Concierge Support | Billing and account experts for Enterprise tier customers |
| Trusted Advisor | Automated service that provides best practice recommendations |
| Infrastructure Event Management | AWS support for planned events (launches, migrations) |
| Severity Level | Classification of support cases based on business impact |
| Response Time | Maximum time AWS commits to responding to a support case |

## 💡 Key Takeaways

1. **AWS offers 5 support plans**: Basic (free), Developer, Business, Enterprise On-Ramp, and Enterprise
2. **Basic Support** includes documentation access and 7 Trusted Advisor checks but NO technical support
3. **Business Support** is the minimum tier for 24/7 technical support and full Trusted Advisor access
4. **Enterprise plans** include a Technical Account Manager (TAM) for proactive support
5. **Response times decrease** as you move to higher support tiers (15 min fastest)
6. **Pricing** is based on the greater of a minimum fee or percentage of AWS usage
7. **Enterprise On-Ramp** bridges the gap between Business and Enterprise with a TAM pool

---

*Next: [02 - AWS Support Center](../02-aws-support-center/readme.md)*

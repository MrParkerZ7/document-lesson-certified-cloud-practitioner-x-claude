# 🌱 Sustainability Pillar

## File Structure

```
lesson-02-aws-well-architected-framework/
└── 07-sustainability-pillar/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Overview

The **Sustainability** pillar focuses on minimizing the environmental impacts of running cloud workloads. This includes understanding impact, establishing goals, maximizing utilization, and adopting more efficient hardware and software.

## Definition

> Sustainability is the ability to continually improve sustainability impacts by reducing energy consumption and increasing efficiency across all components of a workload by maximizing the benefits from the provisioned resources and minimizing the total resources required.

## Design Principles

| Principle | Description |
|-----------|-------------|
| **Understand your impact** | Measure the impact of your cloud workload |
| **Establish sustainability goals** | Set long-term goals for each workload |
| **Maximize utilization** | Right-size workloads to maximize efficiency |
| **Anticipate and adopt more efficient offerings** | Use efficient hardware and services |
| **Use managed services** | Share services across customers to reduce impact |
| **Reduce downstream impact** | Reduce energy required by customers to use your services |

## Key Focus Areas

```
┌────────────────────────────────────────────────────────────────────────┐
│                       Sustainability Pillar                             │
├────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐       │
│   │     Region      │  │     Compute     │  │     Storage     │       │
│   │    Selection    │  │   Efficiency    │  │   Efficiency    │       │
│   │                 │  │                 │  │                 │       │
│   └─────────────────┘  └─────────────────┘  └─────────────────┘       │
│                                                                         │
│   ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐       │
│   │      Data       │  │    Hardware     │  │   Development   │       │
│   │    Management   │  │    & Software   │  │    & Deploy     │       │
│   │                 │  │    Patterns     │  │    Process      │       │
│   └─────────────────┘  └─────────────────┘  └─────────────────┘       │
│                                                                         │
└────────────────────────────────────────────────────────────────────────┘
```

## Best Practices

### 1. Region Selection
- Choose regions with **lower carbon intensity**
- Consider regions powered by **renewable energy**
- Use AWS regions with sustainability programs

### 2. Compute Efficiency
- Use **right-sizing** to avoid over-provisioning
- Implement **Auto Scaling** to match demand
- Use **Spot Instances** to consume spare capacity
- Consider **Graviton processors** (more efficient)

### 3. Storage Efficiency
- Use appropriate **storage tiers**
- Implement **lifecycle policies**
- **Compress** and **deduplicate** data
- Delete unnecessary data

### 4. Data Management
- Minimize data **movement** across regions
- Use efficient **data formats**
- Archive or delete **cold data**

### 5. Hardware and Software Patterns
- Use **managed services** (shared infrastructure)
- Choose efficient **instance types**
- Optimize code for efficiency

### 6. Development and Deployment
- Use **efficient development practices**
- Implement **CI/CD** to reduce waste
- Test at appropriate scale

## AWS Sustainability Initiatives

```
┌────────────────────────────────────────────────────────────────────────┐
│                    AWS Sustainability Commitment                        │
├────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   🎯 Net-Zero Carbon by 2040                                           │
│                                                                         │
│   🔋 100% Renewable Energy by 2025                                     │
│                                                                         │
│   🌊 Water Stewardship (Water+)                                        │
│                                                                         │
│   ⚡ Custom Chips (Graviton - more efficient)                          │
│                                                                         │
│   📊 Customer Carbon Footprint Tool                                    │
│                                                                         │
└────────────────────────────────────────────────────────────────────────┘
```

## Sustainability Tools and Features

| Tool/Feature | Purpose |
|-------------|---------|
| **Customer Carbon Footprint Tool** | Track carbon emissions from AWS usage |
| **EC2 Graviton Instances** | More energy-efficient ARM processors |
| **S3 Intelligent-Tiering** | Automatically moves data to efficient tiers |
| **Auto Scaling** | Reduces idle resources |
| **Spot Instances** | Uses spare EC2 capacity |
| **Lambda** | Scales to zero when not in use |

## Sustainability Metrics

| Metric | Description |
|--------|-------------|
| **Carbon Emissions** | CO2 equivalent from workload |
| **Resource Utilization** | Percentage of provisioned resources used |
| **Data Storage Growth** | Rate of data growth over time |
| **Idle Resources** | Resources provisioned but not used |

## Practical Sustainability Actions

```
Immediate Actions:
┌─────────────────────────────────────────────────────────┐
│                                                          │
│  ✓ Right-size instances (use Compute Optimizer)         │
│  ✓ Enable Auto Scaling                                  │
│  ✓ Use S3 Lifecycle policies                            │
│  ✓ Delete unused resources (EBS, snapshots, AMIs)       │
│  ✓ Use Graviton instances where possible                │
│  ✓ Consider serverless (Lambda, Fargate)                │
│                                                          │
└─────────────────────────────────────────────────────────┘

Long-term Strategy:
┌─────────────────────────────────────────────────────────┐
│                                                          │
│  ✓ Set sustainability KPIs                              │
│  ✓ Monitor with Carbon Footprint Tool                   │
│  ✓ Choose sustainable regions                           │
│  ✓ Optimize application code                            │
│  ✓ Use efficient data formats                           │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

## Shared Responsibility for Sustainability

| AWS Responsibility | Customer Responsibility |
|--------------------|------------------------|
| Data center efficiency | Workload optimization |
| Renewable energy investments | Right-sizing resources |
| Efficient hardware design | Efficient application design |
| Cooling and power efficiency | Data lifecycle management |
| | Choosing sustainable options |

## 🎯 Exam Tips

- Sustainability is the **newest pillar** (added in 2021)
- **Right-sizing** and **Auto Scaling** reduce waste
- **Graviton processors** are more energy-efficient
- **Managed services** share resources across customers
- **S3 Intelligent-Tiering** automatically optimizes storage
- **Customer Carbon Footprint Tool** tracks emissions
- The goal is to **maximize utilization** and **minimize waste**

## 💡 Key Takeaways

1. **Understand impact** - Use Carbon Footprint Tool
2. **Right-size resources** - Don't over-provision
3. **Use efficient services** - Graviton, Lambda, managed services
4. **Optimize storage** - Lifecycle policies, compression
5. **Delete unused resources** - Reduce waste
6. **Choose efficient regions** - Consider renewable energy availability

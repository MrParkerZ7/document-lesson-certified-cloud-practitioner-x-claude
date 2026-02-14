# 📶 AWS Wavelength

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 06-aws-wavelength/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Wavelength brings AWS compute and storage services to the edge of 5G networks, minimizing latency to connect to applications from mobile devices. Wavelength Zones are AWS infrastructure deployments embedded within telecommunications providers' data centers at the edge of 5G networks.

## What is AWS Wavelength?

```
+------------------------------------------------------------------+
|                      AWS WAVELENGTH                               |
+------------------------------------------------------------------+
|                                                                   |
|   Wavelength embeds AWS services in 5G networks for              |
|   ultra-low latency mobile and connected device applications     |
|                                                                   |
|   5G Mobile Device                                                |
|   +----------+                                                    |
|   | Phone    |                                                    |
|   | IoT      |                                                    |
|   +----------+                                                    |
|        |                                                          |
|        v (5G Network)                                             |
|   +------------------+                                            |
|   | WAVELENGTH ZONE  |  <-- AWS inside carrier network           |
|   | (Carrier Edge)   |                                            |
|   | • EC2            |                                            |
|   | • EBS            |                                            |
|   +------------------+                                            |
|        |                                                          |
|        v (Connected)                                              |
|   +------------------+                                            |
|   | AWS REGION       |                                            |
|   +------------------+                                            |
|                                                                   |
+------------------------------------------------------------------+
```

## Wavelength Characteristics

| Characteristic | Description |
|----------------|-------------|
| Location | Inside 5G carrier networks |
| Latency | Single-digit milliseconds |
| Connection | To parent AWS region |
| Focus | Mobile and IoT applications |
| Partners | Verizon, Vodafone, KDDI, SK Telecom |

## Wavelength vs Other AWS Extensions

| Feature | Wavelength | Local Zones | Outposts |
|---------|------------|-------------|----------|
| Location | 5G network edge | Near cities | Your data center |
| Target | Mobile/IoT apps | Desktop users | On-premises |
| Latency | Ultra-low (5G) | < 10ms | Local |
| Network | Carrier | Internet | Your network |

## Wavelength Zone Components

| Component | Description |
|-----------|-------------|
| Wavelength Zone | AWS infrastructure in carrier network |
| Carrier Gateway | Connects to carrier network |
| VPC extension | Same VPC as parent region |
| Subnets | Wavelength-specific subnets |

## Available Services

| Service | Description |
|---------|-------------|
| EC2 | Compute instances |
| EBS | Block storage |
| VPC | Networking |
| Autoscaling | Scale capacity |

## Wavelength Use Cases

```
+------------------------------------------------------------------+
|                  WAVELENGTH USE CASES                             |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |  INTERACTIVE     |  |   REAL-TIME      |  |   CONNECTED      | |
|   |  GAMING          |  |   VIDEO          |  |   VEHICLES       | |
|   +------------------+  +------------------+  +------------------+ |
|   | Mobile gaming    |  | Live streaming   |  | Autonomous cars  | |
|   | Cloud gaming     |  | Video analytics  |  | V2X comms        | |
|   | AR/VR            |  | Security cameras |  | Fleet mgmt       | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |   SMART          |  |   HEALTHCARE     |  |   INDUSTRIAL     | |
|   |   CITIES         |  |                  |  |   IoT            | |
|   +------------------+  +------------------+  +------------------+ |
|   | Traffic mgmt     |  | Remote surgery   |  | Robotics         | |
|   | Public safety    |  | Telemedicine     |  | Automation       | |
|   | Utilities        |  | Diagnostics      |  | Monitoring       | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Wavelength Partners

| Carrier | Regions |
|---------|---------|
| Verizon | US |
| Vodafone | UK, Germany |
| KDDI | Japan |
| SK Telecom | South Korea |
| Bell Canada | Canada |

## How Wavelength Works

| Step | Description |
|------|-------------|
| 1 | 5G device connects to carrier network |
| 2 | Traffic routed to Wavelength Zone |
| 3 | Application processes at edge |
| 4 | Response sent back via 5G |
| 5 | Optional: Connect to AWS region |

## Wavelength Architecture

```
+------------------------------------------------------------------+
|                  WAVELENGTH ARCHITECTURE                          |
+------------------------------------------------------------------+
|                                                                   |
|   +----------+      +----------+      +-----------------+         |
|   | 5G       |      | Carrier  |      | AWS Region      |         |
|   | Device   | ---> | Network  | ---> | (Full Services) |         |
|   +----------+      +----------+      +-----------------+         |
|                          |                                        |
|                          v                                        |
|                    +------------------+                           |
|                    | WAVELENGTH ZONE  |                           |
|                    | +----------+     |                           |
|                    | | EC2      |     |                           |
|                    | +----------+     |                           |
|                    | +----------+     |                           |
|                    | | EBS      |     |                           |
|                    | +----------+     |                           |
|                    +------------------+                           |
|                    (Inside Carrier DC)                            |
|                                                                   |
+------------------------------------------------------------------+
```

## Benefits

| Benefit | Description |
|---------|-------------|
| Ultra-low latency | Process at network edge |
| 5G optimization | Built for 5G networks |
| Same APIs | Standard AWS APIs |
| VPC integration | Extend your VPC |
| Carrier support | Major carriers included |

## Limitations

| Limitation | Description |
|------------|-------------|
| Limited services | Only core compute/storage |
| Carrier dependent | Need carrier partnership |
| Regional | Specific metro areas only |
| Capacity | Smaller than regions |

## 🎯 Exam Tips

- **Wavelength** = AWS at the edge of **5G networks**
- For **mobile** and **IoT** applications
- Located in **carrier (telecom) data centers**
- Partners: **Verizon**, **Vodafone**, **KDDI**, etc.
- Use cases: **gaming**, **AR/VR**, **connected vehicles**, **smart cities**
- Different from **Local Zones** (near cities) and **Outposts** (on-premises)
- **Ultra-low latency** for 5G devices

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Wavelength Zone | AWS infrastructure in carrier network |
| 5G | Fifth generation mobile network |
| Carrier Gateway | Connection to carrier network |
| Edge Computing | Processing near data source |
| IoT | Internet of Things devices |

## 💡 Key Takeaways

1. Wavelength embeds AWS in 5G carrier networks
2. Designed for ultra-low latency mobile applications
3. Located inside telecom provider data centers
4. Partners include Verizon, Vodafone, KDDI, SK Telecom
5. Ideal for gaming, AR/VR, connected vehicles, IoT
6. Limited services (EC2, EBS) compared to full regions
7. Different from Local Zones and Outposts

---

*Next: [07 - AWS Outposts](../07-aws-outposts/readme.md)*

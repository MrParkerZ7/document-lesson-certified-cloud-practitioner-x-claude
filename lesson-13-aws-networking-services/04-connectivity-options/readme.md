# 🔗 AWS Connectivity Options

## Introduction

AWS provides multiple ways to connect your VPCs together, to on-premises networks, and to the internet. Understanding these connectivity options is crucial for designing hybrid architectures and multi-VPC environments. This lesson covers VPC Peering, Transit Gateway, VPN, and Direct Connect.

## Connectivity Overview

```
+------------------------------------------------------------------+
|                 AWS CONNECTIVITY OPTIONS                          |
+------------------------------------------------------------------+
|                                                                   |
|                       +-------------+                             |
|                       |  INTERNET   |                             |
|                       +------+------+                             |
|                              |                                    |
|   +------------+     +-------+--------+     +------------+        |
|   | On-Premises|     |                |     | VPC A      |        |
|   | Data Center|-----|  AWS Cloud     |-----|            |        |
|   +------------+     |                |     +------------+        |
|         |            |  +---------+   |            |              |
|         |            |  | Transit |   |            |              |
|   [VPN or            |  | Gateway |   |      [VPC Peering]        |
|    Direct Connect]   |  +---------+   |            |              |
|                      |                |     +------------+        |
|                      +----------------+     | VPC B      |        |
|                                             |            |        |
|                                             +------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## VPC Peering

| Feature | Description |
|---------|-------------|
| Purpose | Connect two VPCs privately |
| Traffic | Stays on AWS backbone network |
| Transitive | NOT supported (A-B, B-C does NOT mean A-C) |
| Cross-Region | Supported (inter-region peering) |
| Cross-Account | Supported |
| CIDR | Must not overlap |
| Cost | Data transfer charges only |

## VPC Peering Architecture

```
+------------------------------------------------------------------+
|                      VPC PEERING                                  |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------+                    +----------------+        |
|   |    VPC A       |    Peering         |    VPC B       |        |
|   |  10.0.0.0/16   |<------------------>|  172.16.0.0/16 |        |
|   |                |    Connection      |                |        |
|   +----------------+                    +----------------+        |
|                                                                   |
|   IMPORTANT: VPC Peering is NOT transitive!                       |
|                                                                   |
|   +-------+         +-------+         +-------+                   |
|   | VPC A |<------->| VPC B |<------->| VPC C |                   |
|   +-------+         +-------+         +-------+                   |
|       |                                   ^                       |
|       |     VPC A CANNOT reach VPC C      |                       |
|       +------------- X -------------------+                       |
|                                                                   |
|   Solution: Create direct peering between A and C                 |
|             OR use Transit Gateway                                |
|                                                                   |
+------------------------------------------------------------------+
```

## VPC Peering Limitations

| Limitation | Description |
|------------|-------------|
| No Transitive Routing | Must peer each VPC pair directly |
| No Overlapping CIDR | VPCs must have different IP ranges |
| Max Connections | Up to 125 peering connections per VPC |
| No Edge to Edge | Cannot route through peered VPC's gateway |

## AWS Transit Gateway

| Feature | Description |
|---------|-------------|
| Purpose | Hub-and-spoke network connectivity |
| Scale | Connect thousands of VPCs and on-premises |
| Transitive | Supports transitive routing |
| Cross-Region | Transit Gateway Peering available |
| Simplification | Reduces complex peering meshes |
| Attachments | VPCs, VPN, Direct Connect |

## Transit Gateway Architecture

```
+------------------------------------------------------------------+
|                    TRANSIT GATEWAY                                |
+------------------------------------------------------------------+
|                                                                   |
|                     +------------------+                          |
|                     | Transit Gateway  |                          |
|                     |   (Hub)          |                          |
|                     +--------+---------+                          |
|                              |                                    |
|         +--------------------+--------------------+               |
|         |          |         |         |          |               |
|         v          v         v         v          v               |
|   +---------+ +---------+ +---------+ +----+ +---------+          |
|   | VPC A   | | VPC B   | | VPC C   | |VPN | | Direct  |          |
|   |         | |         | |         | |    | | Connect |          |
|   +---------+ +---------+ +---------+ +----+ +---------+          |
|                                          |        |               |
|                              +-----------+--------+               |
|                              |                                    |
|                         +----v----+                               |
|                         |On-Prem  |                               |
|                         |Data Ctr |                               |
|                         +---------+                               |
|                                                                   |
|   All VPCs can communicate through Transit Gateway                |
|   On-premises can reach all VPCs through single connection        |
|                                                                   |
+------------------------------------------------------------------+
```

## VPC Peering vs. Transit Gateway

| Feature | VPC Peering | Transit Gateway |
|---------|-------------|-----------------|
| Topology | Point-to-point | Hub-and-spoke |
| Transitive Routing | No | Yes |
| Scale | Limited (mesh complexity) | Thousands of attachments |
| Cost | Data transfer only | Hourly + data transfer |
| Bandwidth | No limit | Up to 50 Gbps per attachment |
| Use Case | Few VPCs | Many VPCs, hybrid networks |

## AWS Site-to-Site VPN

| Feature | Description |
|---------|-------------|
| Purpose | Encrypted connection over internet |
| Encryption | IPsec VPN tunnels |
| Endpoints | Virtual Private Gateway (AWS) + Customer Gateway (on-prem) |
| Bandwidth | Up to 1.25 Gbps per tunnel |
| Redundancy | Two tunnels for high availability |
| Setup Time | Minutes to configure |
| Cost | Hourly + data transfer |

## Site-to-Site VPN Architecture

```
+------------------------------------------------------------------+
|                     SITE-TO-SITE VPN                              |
+------------------------------------------------------------------+
|                                                                   |
|   +-------------------+                  +-------------------+    |
|   |   ON-PREMISES     |                  |      AWS VPC      |    |
|   |                   |                  |                   |    |
|   |  +-------------+  |     INTERNET     |  +-------------+  |    |
|   |  | Customer    |  |                  |  | Virtual     |  |    |
|   |  | Gateway     |===============IPsec====| Private     |  |    |
|   |  | (Your       |  |    Encrypted     |  | Gateway     |  |    |
|   |  |  Router)    |===============Tunnel===| (VGW)       |  |    |
|   |  +-------------+  |                  |  +-------------+  |    |
|   |        |          |                  |        |          |    |
|   |  [Internal       ]|                  |  [EC2 Instances]  |    |
|   |  [Network        ]|                  |                   |    |
|   +-------------------+                  +-------------------+    |
|                                                                   |
|   Two tunnels for redundancy (both active or active-passive)      |
|                                                                   |
+------------------------------------------------------------------+
```

## VPN Components

| Component | Location | Description |
|-----------|----------|-------------|
| Virtual Private Gateway (VGW) | AWS | VPN endpoint on AWS side |
| Customer Gateway (CGW) | On-premises | VPN endpoint configuration in AWS |
| Customer Gateway Device | On-premises | Physical/software VPN router |
| VPN Connection | Both | The actual encrypted tunnels |

## AWS Direct Connect

| Feature | Description |
|---------|-------------|
| Purpose | Dedicated private connection to AWS |
| Path | Does NOT go over internet |
| Bandwidth | 1 Gbps, 10 Gbps, or 100 Gbps |
| Latency | Lower, more consistent than VPN |
| Setup Time | Weeks to months (physical installation) |
| Cost | Port hours + data transfer (lower egress) |

## Direct Connect Architecture

```
+------------------------------------------------------------------+
|                     DIRECT CONNECT                                |
+------------------------------------------------------------------+
|                                                                   |
|   +---------------+     +------------------+     +-------------+  |
|   | ON-PREMISES   |     | Direct Connect   |     | AWS Region  |  |
|   | DATA CENTER   |     | Location         |     |             |  |
|   |               |     |                  |     |  +-------+  |  |
|   | +----------+  |     | +-------------+  |     |  | VPC   |  |  |
|   | | Your     |========| | AWS Direct  |========|  +-------+  |  |
|   | | Router   |  |     | | Connect     |  |     |             |  |
|   | +----------+  |     | | Router      |  |     |  +-------+  |  |
|   |               |     | +-------------+  |     |  | VPC   |  |  |
|   +---------------+     +------------------+     |  +-------+  |  |
|         |                                        |             |  |
|    Cross-Connect                                 +-------------+  |
|    (Physical Cable)                                               |
|                                                                   |
|   Connection Types:                                               |
|   - Dedicated: 1, 10, or 100 Gbps physical port                   |
|   - Hosted: Sub-1 Gbps through AWS Partner                        |
|                                                                   |
+------------------------------------------------------------------+
```

## Direct Connect Virtual Interfaces

| VIF Type | Purpose | Connects To |
|----------|---------|-------------|
| Private VIF | Access VPC resources | Virtual Private Gateway |
| Public VIF | Access AWS public services | AWS public endpoints |
| Transit VIF | Access through Transit Gateway | Transit Gateway |

## VPN vs. Direct Connect

| Feature | VPN | Direct Connect |
|---------|-----|----------------|
| Path | Over internet | Private dedicated line |
| Encryption | IPsec (encrypted) | Not encrypted by default |
| Setup Time | Minutes | Weeks to months |
| Bandwidth | Up to 1.25 Gbps | Up to 100 Gbps |
| Latency | Variable | Consistent, lower |
| Cost | Lower upfront | Higher, but lower egress |
| Redundancy | Built-in (2 tunnels) | Requires second connection |
| Use Case | Quick setup, backup | High bandwidth, consistent latency |

## Hybrid Connectivity Patterns

```
+------------------------------------------------------------------+
|                 HYBRID CONNECTIVITY OPTIONS                       |
+------------------------------------------------------------------+
|                                                                   |
|   1. VPN Only (Quick, encrypted, lower bandwidth):                |
|      [On-Prem] ====VPN over Internet===> [AWS VPC]                |
|                                                                   |
|   2. Direct Connect Only (High bandwidth, consistent):            |
|      [On-Prem] ===Direct Connect=======> [AWS VPC]                |
|                                                                   |
|   3. Direct Connect + VPN Backup (Best of both):                  |
|      [On-Prem] ===Direct Connect=======> [AWS VPC]                |
|                 ===VPN (backup)========> [AWS VPC]                |
|                                                                   |
|   4. VPN over Direct Connect (Encrypted DC):                      |
|      [On-Prem] ===DC + IPsec encryption=> [AWS VPC]               |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Client VPN

| Feature | Description |
|---------|-------------|
| Purpose | Remote user VPN access |
| Type | OpenVPN-based |
| Use Case | Work-from-home, mobile access |
| Authentication | AD, SAML, certificates |
| Endpoint | Managed by AWS |

## 🎯 Exam Tips

- **VPC Peering** is NOT transitive - each VPC pair needs its own connection
- **Transit Gateway** enables transitive routing (hub-and-spoke model)
- **VPC Peering** is cheaper but complex with many VPCs; **Transit Gateway** simplifies
- **Site-to-Site VPN** goes over the internet but is encrypted (IPsec)
- **Direct Connect** is a private dedicated connection (does NOT use internet)
- Direct Connect takes weeks/months to set up; VPN is ready in minutes
- **Direct Connect** provides consistent latency; VPN latency varies
- Use **VPN as backup** for Direct Connect for high availability
- **Virtual Private Gateway (VGW)** is the AWS-side VPN endpoint
- **Customer Gateway (CGW)** represents your on-premises router in AWS
- Direct Connect is NOT encrypted by default - add VPN for encryption

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| VPC Peering | Private connection between two VPCs |
| Transit Gateway | Central hub for connecting multiple VPCs and on-premises |
| Site-to-Site VPN | Encrypted IPsec tunnel over the internet |
| Direct Connect | Dedicated private connection to AWS |
| Virtual Private Gateway | AWS-side VPN/Direct Connect endpoint |
| Customer Gateway | Represents on-premises router in AWS |
| IPsec | Protocol for encrypting VPN traffic |

## 💡 Key Takeaways

1. VPC Peering connects two VPCs directly but is not transitive
2. Transit Gateway simplifies connectivity for multiple VPCs (hub-and-spoke)
3. Site-to-Site VPN provides encrypted connectivity over the public internet
4. Direct Connect offers dedicated private connectivity with consistent performance
5. VPN sets up in minutes; Direct Connect takes weeks to months
6. Use VPN as a backup for Direct Connect for high availability
7. Choose connectivity based on bandwidth, latency, and setup time requirements

---

*Previous: [03 - Amazon Route 53](../03-amazon-route-53/readme.md) | Next: [05 - Content Delivery](../05-content-delivery/readme.md)*

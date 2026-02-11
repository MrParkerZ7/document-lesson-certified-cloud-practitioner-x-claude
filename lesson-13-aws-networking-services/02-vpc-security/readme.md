# 🔐 VPC Security

## Introduction

Securing your VPC is critical to protecting your AWS resources. AWS provides multiple layers of security including Security Groups, Network Access Control Lists (NACLs), and VPC Flow Logs. Understanding how these work together is essential for both the exam and real-world implementations.

## Defense in Depth

```
+------------------------------------------------------------------+
|                    VPC SECURITY LAYERS                            |
+------------------------------------------------------------------+
|                                                                   |
|   INTERNET                                                        |
|       |                                                           |
|       v                                                           |
|   +----------------------------------------------------------+   |
|   |                  NETWORK ACL (NACL)                       |   |
|   |              Stateless - Subnet Level                     |   |
|   |    Rules: Allow/Deny, Inbound + Outbound separately       |   |
|   +----------------------------------------------------------+   |
|       |                                                           |
|       v                                                           |
|   +----------------------------------------------------------+   |
|   |                   SECURITY GROUP                          |   |
|   |              Stateful - Instance Level                    |   |
|   |    Rules: Allow only, Return traffic auto-allowed         |   |
|   +----------------------------------------------------------+   |
|       |                                                           |
|       v                                                           |
|   +----------------------------------------------------------+   |
|   |                      EC2 INSTANCE                         |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Security Groups

| Feature | Description |
|---------|-------------|
| Level | Instance level (ENI) |
| State | Stateful |
| Rules | Allow rules only (no deny) |
| Default Inbound | All traffic denied |
| Default Outbound | All traffic allowed |
| Evaluation | All rules evaluated |

## Security Group Rules

```
+------------------------------------------------------------------+
|                  SECURITY GROUP EXAMPLE                           |
+------------------------------------------------------------------+
|                                                                   |
|   WEB SERVER SECURITY GROUP                                       |
|   +-------------------------------+                               |
|   | INBOUND RULES:                |                               |
|   +-------------------------------+                               |
|   | Type  | Port | Source         |                               |
|   +-------+------+----------------+                               |
|   | HTTP  | 80   | 0.0.0.0/0      |  <-- Allow from anywhere      |
|   | HTTPS | 443  | 0.0.0.0/0      |  <-- Allow from anywhere      |
|   | SSH   | 22   | 10.0.0.0/16    |  <-- Allow from VPC only      |
|   +-------------------------------+                               |
|                                                                   |
|   +-------------------------------+                               |
|   | OUTBOUND RULES:               |                               |
|   +-------------------------------+                               |
|   | Type  | Port | Destination    |                               |
|   +-------+------+----------------+                               |
|   | All   | All  | 0.0.0.0/0      |  <-- Allow all outbound       |
|   +-------------------------------+                               |
|                                                                   |
+------------------------------------------------------------------+
```

## Security Group Key Concepts

| Concept | Explanation |
|---------|-------------|
| Stateful | Return traffic automatically allowed |
| No Deny Rules | Can only allow, implicit deny for rest |
| Reference Other SGs | Use SG ID as source/destination |
| Multiple SGs | Instance can have multiple security groups |
| Changes | Take effect immediately |

## Network ACLs (NACLs)

| Feature | Description |
|---------|-------------|
| Level | Subnet level |
| State | Stateless |
| Rules | Allow AND Deny rules |
| Default | Allow all inbound/outbound |
| Evaluation | Rules processed in number order |
| Association | One NACL per subnet |

## NACL Rule Processing

```
+------------------------------------------------------------------+
|                    NACL RULE EVALUATION                           |
+------------------------------------------------------------------+
|                                                                   |
|   Rules are evaluated in ORDER by rule number (lowest first)      |
|                                                                   |
|   Example NACL:                                                   |
|   +-------+--------+----------+-------+--------+---------+        |
|   | Rule# | Type   | Protocol | Port  | Source | Allow?  |        |
|   +-------+--------+----------+-------+--------+---------+        |
|   | 100   | HTTP   | TCP      | 80    | 0.0.0.0| ALLOW   |        |
|   | 110   | HTTPS  | TCP      | 443   | 0.0.0.0| ALLOW   |        |
|   | 120   | SSH    | TCP      | 22    | 10.0.0 | ALLOW   |        |
|   | 130   | Custom | TCP      | 22    | X.X.X.X| DENY    | <--    |
|   | *     | ALL    | ALL      | ALL   | 0.0.0.0| DENY    |        |
|   +-------+--------+----------+-------+--------+---------+        |
|                                    |                              |
|   Rule 130 will be evaluated AFTER rules 100-120                  |
|   * = Default rule, evaluated last, denies all unmatched          |
|                                                                   |
+------------------------------------------------------------------+
```

## Security Groups vs. NACLs

| Feature | Security Groups | Network ACLs |
|---------|-----------------|--------------|
| Level | Instance (ENI) | Subnet |
| State | Stateful | Stateless |
| Rules | Allow only | Allow and Deny |
| Rule Processing | All rules evaluated | First match wins |
| Default Inbound | Deny all | Allow all |
| Default Outbound | Allow all | Allow all |
| Return Traffic | Automatically allowed | Must explicitly allow |
| Use Case | Fine-grained instance control | Subnet-wide rules |

## Stateful vs. Stateless

```
+------------------------------------------------------------------+
|              STATEFUL vs STATELESS EXPLAINED                      |
+------------------------------------------------------------------+
|                                                                   |
|   STATEFUL (Security Groups):                                     |
|   +------------------------+                                      |
|   |   Request  -------->   |  If inbound is allowed...            |
|   |   Response <--------   |  ...outbound response auto-allowed   |
|   +------------------------+                                      |
|                                                                   |
|   STATELESS (NACLs):                                              |
|   +------------------------+                                      |
|   |   Request  -------->   |  Inbound rule needed                 |
|   |   Response <--------   |  Outbound rule ALSO needed           |
|   +------------------------+                                      |
|                                                                   |
|   NACL requires rules for BOTH directions!                        |
|                                                                   |
+------------------------------------------------------------------+
```

## Ephemeral Ports (Important for NACLs)

| Concept | Description |
|---------|-------------|
| What | Temporary ports for return traffic |
| Range | 1024-65535 (varies by OS) |
| Why Important | NACLs need outbound rules for these ports |
| Linux | 32768-60999 |
| Windows | 49152-65535 |

## VPC Flow Logs

| Feature | Description |
|---------|-------------|
| Purpose | Capture IP traffic information |
| Levels | VPC, Subnet, or ENI |
| Destination | CloudWatch Logs, S3, or Kinesis |
| Content | Source/dest IPs, ports, protocol, action |
| Use Cases | Security analysis, troubleshooting |

## Flow Log Record Fields

```
+------------------------------------------------------------------+
|                    VPC FLOW LOG FORMAT                            |
+------------------------------------------------------------------+
|                                                                   |
|   version account-id interface-id srcaddr dstaddr srcport         |
|   dstport protocol packets bytes start end action log-status      |
|                                                                   |
|   Example:                                                        |
|   2 123456789012 eni-abc123 10.0.1.5 10.0.2.10 443 49152          |
|   6 20 4000 1620000000 1620000060 ACCEPT OK                       |
|                                                                   |
|   This shows: ACCEPTED TCP traffic from 10.0.1.5:443 to           |
|               10.0.2.10:49152, 20 packets, 4000 bytes             |
|                                                                   |
+------------------------------------------------------------------+
```

## Flow Logs Key Points

| Feature | Description |
|---------|-------------|
| Capture Level | VPC, Subnet, or Network Interface |
| Latency | Not real-time (minutes delay) |
| Immutable | Cannot modify after creation |
| Not Captured | DNS to Amazon, DHCP, metadata |
| Cost | CloudWatch/S3 storage charges |

## Security Best Practices

| Practice | Description |
|----------|-------------|
| Least Privilege | Only allow necessary traffic |
| Defense in Depth | Use both SGs and NACLs |
| Private Subnets | Place sensitive resources in private subnets |
| Flow Logs | Enable for security monitoring |
| Reference SGs | Use security group IDs instead of IPs |
| Regular Audits | Review and clean up unused rules |

## Common Security Group Patterns

```
+------------------------------------------------------------------+
|                SECURITY GROUP CHAINING                            |
+------------------------------------------------------------------+
|                                                                   |
|   [Internet]                                                      |
|       |                                                           |
|       v                                                           |
|   +------------------+    +------------------+                    |
|   | ALB SG           |    | Web Server SG    |                    |
|   | Inbound: 443     |--->| Inbound: 80      |                    |
|   | from 0.0.0.0/0   |    | from ALB-SG      | <-- Reference SG   |
|   +------------------+    +------------------+                    |
|                                  |                                |
|                                  v                                |
|                           +------------------+                    |
|                           | Database SG      |                    |
|                           | Inbound: 3306    |                    |
|                           | from Web-SG      | <-- Reference SG   |
|                           +------------------+                    |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **Security Groups** are STATEFUL and operate at the INSTANCE level
- **NACLs** are STATELESS and operate at the SUBNET level
- Security Groups can only ALLOW; NACLs can ALLOW and DENY
- NACL rules are processed in ORDER (lowest rule number first)
- Security Groups evaluate ALL rules before deciding
- Default Security Group: denies all inbound, allows all outbound
- Default NACL: allows all inbound and outbound
- **Stateful** means return traffic is automatically allowed
- **Stateless** means you must explicitly allow return traffic
- **VPC Flow Logs** capture metadata about IP traffic (not content)
- Flow Logs can be created at VPC, subnet, or ENI level

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Security Group | Stateful virtual firewall at instance level |
| NACL | Stateless network access control at subnet level |
| Stateful | Return traffic automatically allowed |
| Stateless | Return traffic must be explicitly allowed |
| VPC Flow Logs | IP traffic metadata capture service |
| Ephemeral Ports | Temporary ports for return traffic (1024-65535) |
| ENI | Elastic Network Interface |

## 💡 Key Takeaways

1. Security Groups are stateful and control traffic at the instance level
2. NACLs are stateless and control traffic at the subnet level
3. Security Groups only allow; NACLs can allow and deny traffic
4. NACL rules process in numerical order; Security Groups evaluate all rules
5. Use both Security Groups and NACLs for defense in depth
6. VPC Flow Logs capture IP traffic metadata for security analysis
7. Reference other Security Groups by ID for cleaner, more maintainable rules

---

*Previous: [01 - Amazon VPC](../01-amazon-vpc/readme.md) | Next: [03 - Amazon Route 53](../03-amazon-route-53/readme.md)*

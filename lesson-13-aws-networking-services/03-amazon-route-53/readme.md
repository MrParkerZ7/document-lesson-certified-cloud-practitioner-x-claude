# 🌐 Amazon Route 53

## Introduction

Amazon Route 53 is AWS's highly available and scalable Domain Name System (DNS) web service. It connects user requests to infrastructure running in AWS or on-premises, and can also be used to register domain names. The name "Route 53" refers to TCP/UDP port 53, which is used for DNS.

## What is DNS?

```
+------------------------------------------------------------------+
|                     HOW DNS WORKS                                 |
+------------------------------------------------------------------+
|                                                                   |
|   User types: www.example.com                                     |
|                                                                   |
|   +--------+         +-------------+         +---------------+    |
|   | User   |  --->   | DNS Server  |  --->   | IP: 54.23.1.5 |    |
|   | Browser|         | (Route 53)  |         | (Web Server)  |    |
|   +--------+         +-------------+         +---------------+    |
|       |                    |                        ^             |
|       |    1. Query:       |                        |             |
|       |    "www.example.com"                        |             |
|       |                    |                        |             |
|       |    2. Response:    |                        |             |
|       |    "54.23.1.5"     |                        |             |
|       |                    |                        |             |
|       +--------------------+------------------------+             |
|                     3. Connect to IP                              |
|                                                                   |
+------------------------------------------------------------------+
```

## Route 53 Key Features

| Feature | Description |
|---------|-------------|
| DNS Service | Translates domain names to IP addresses |
| Domain Registration | Register and manage domain names |
| Health Checks | Monitor endpoint health |
| Traffic Routing | Multiple routing policies |
| High Availability | 100% SLA uptime guarantee |
| Global Service | Not region-specific |

## DNS Record Types

| Record Type | Description | Example |
|-------------|-------------|---------|
| A | Maps domain to IPv4 address | example.com -> 54.23.1.5 |
| AAAA | Maps domain to IPv6 address | example.com -> 2001:0db8::1 |
| CNAME | Maps domain to another domain | www.example.com -> example.com |
| MX | Mail server records | example.com -> mail.example.com |
| TXT | Text records (verification) | SPF, DKIM records |
| NS | Name server records | Identifies authoritative DNS |
| Alias | AWS-specific, maps to AWS resources | example.com -> ELB DNS name |

## Alias Records (AWS Specific)

```
+------------------------------------------------------------------+
|                 ALIAS vs CNAME RECORDS                            |
+------------------------------------------------------------------+
|                                                                   |
|   CNAME Record:                                                   |
|   - Cannot be used for zone apex (naked domain)                   |
|   - example.com -> NOT allowed with CNAME                         |
|   - www.example.com -> works fine                                 |
|   - Charged for DNS queries                                       |
|                                                                   |
|   ALIAS Record (AWS only):                                        |
|   - CAN be used for zone apex                                     |
|   - example.com -> ELB, CloudFront, S3 = ALLOWED                  |
|   - FREE for queries to AWS resources                             |
|   - Native health check integration                               |
|                                                                   |
+------------------------------------------------------------------+
```

## Alias Record Targets

| AWS Resource | Can Use Alias? |
|--------------|----------------|
| ELB (ALB, NLB, CLB) | Yes |
| CloudFront Distribution | Yes |
| S3 Website Endpoint | Yes |
| API Gateway | Yes |
| Elastic Beanstalk | Yes |
| VPC Interface Endpoint | Yes |
| Another Route 53 Record | Yes |
| EC2 Public IP | No (use A record) |
| RDS Endpoint | No (use CNAME) |

## Routing Policies

| Policy | Description | Use Case |
|--------|-------------|----------|
| Simple | Single resource, no health checks | Basic routing |
| Weighted | Distribute by percentage | A/B testing, gradual migration |
| Latency | Route to lowest latency region | Global performance |
| Failover | Active-passive failover | Disaster recovery |
| Geolocation | Route by user location | Localized content |
| Geoproximity | Route by geographic distance | Traffic shifting |
| Multivalue | Multiple healthy resources | Simple load balancing |

## Routing Policy Details

```
+------------------------------------------------------------------+
|                    ROUTING POLICIES                               |
+------------------------------------------------------------------+
|                                                                   |
|   SIMPLE ROUTING:                                                 |
|   User --> Route 53 --> Single Resource                          |
|   (No health checks, returns all values if multiple)              |
|                                                                   |
|   WEIGHTED ROUTING:                                               |
|   User --> Route 53 --> 70% to Server A                          |
|                     --> 30% to Server B                          |
|   (Great for blue/green deployments)                              |
|                                                                   |
|   LATENCY ROUTING:                                                |
|   US User    --> Route 53 --> US-East Region (lowest latency)    |
|   EU User    --> Route 53 --> EU-West Region (lowest latency)    |
|                                                                   |
|   FAILOVER ROUTING:                                               |
|   User --> Route 53 --> Primary (if healthy)                     |
|                     --> Secondary (if primary fails)              |
|                                                                   |
|   GEOLOCATION ROUTING:                                            |
|   France User  --> Route 53 --> French Content Server            |
|   Germany User --> Route 53 --> German Content Server            |
|                                                                   |
+------------------------------------------------------------------+
```

## Weighted Routing Example

| Record | Weight | Traffic % |
|--------|--------|-----------|
| Server A | 70 | 70% |
| Server B | 20 | 20% |
| Server C | 10 | 10% |

## Health Checks

| Feature | Description |
|---------|-------------|
| Purpose | Monitor endpoint health |
| Types | HTTP, HTTPS, TCP |
| Frequency | Every 10 or 30 seconds |
| Threshold | Configurable failure threshold |
| Integration | Automatic failover when unhealthy |
| CloudWatch | Integrates with CloudWatch alarms |

## Health Check Types

```
+------------------------------------------------------------------+
|                    HEALTH CHECK TYPES                             |
+------------------------------------------------------------------+
|                                                                   |
|   1. ENDPOINT HEALTH CHECK:                                       |
|      Route 53 --> HTTP/HTTPS/TCP --> Your Endpoint                |
|      Checks: Response code, response body, latency                |
|                                                                   |
|   2. CALCULATED HEALTH CHECK:                                     |
|      Combines multiple health checks with AND/OR logic            |
|      Example: Healthy if 2 of 3 child checks pass                 |
|                                                                   |
|   3. CLOUDWATCH ALARM HEALTH CHECK:                               |
|      Route 53 monitors CloudWatch alarm state                     |
|      Useful for private resources (in VPC)                        |
|                                                                   |
+------------------------------------------------------------------+
```

## Domain Registration

| Feature | Description |
|---------|-------------|
| Register Domains | Purchase new domains through AWS |
| Transfer Domains | Move existing domains to Route 53 |
| Auto-Renew | Automatic domain renewal option |
| Privacy Protection | Free WHOIS privacy |
| DNS Management | Automatic hosted zone creation |

## Hosted Zones

| Type | Description | Use Case |
|------|-------------|----------|
| Public Hosted Zone | Routes internet traffic | Public websites, APIs |
| Private Hosted Zone | Routes VPC internal traffic | Internal applications |

## Route 53 Pricing

| Component | Cost |
|-----------|------|
| Hosted Zones | $0.50/month per zone |
| DNS Queries | Per million queries |
| Health Checks | Per health check/month |
| Domain Registration | Per domain/year |
| Alias Queries | FREE to AWS resources |

## Route 53 Resolver

```
+------------------------------------------------------------------+
|                   ROUTE 53 RESOLVER                               |
+------------------------------------------------------------------+
|                                                                   |
|   Hybrid DNS Resolution:                                          |
|                                                                   |
|   +-------------+          +---------------+                      |
|   | On-Premises |  <---->  | AWS VPC       |                      |
|   | DNS Server  |          | Route 53      |                      |
|   +-------------+          | Resolver      |                      |
|         |                  +---------------+                      |
|         |                        |                                |
|         v                        v                                |
|   [corp.local]            [aws.internal]                          |
|                                                                   |
|   Inbound Endpoint: On-prem resolves AWS DNS                      |
|   Outbound Endpoint: AWS resolves on-prem DNS                     |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **Route 53** is a global service (not region-specific) with 100% SLA
- Port 53 is the standard DNS port (hence the name "Route 53")
- **Alias records** are AWS-specific and FREE for AWS resource queries
- Alias records CAN be used at zone apex (naked domain); CNAME cannot
- **Simple routing** returns all values; client chooses randomly
- **Weighted routing** for A/B testing and gradual traffic shifting
- **Latency routing** sends users to lowest latency region
- **Failover routing** for disaster recovery (active-passive)
- **Geolocation routing** routes based on user's geographic location
- **Health checks** enable automatic failover when endpoints fail
- Route 53 can register domains AND manage DNS (two separate features)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| DNS | Domain Name System, translates names to IPs |
| A Record | Maps domain name to IPv4 address |
| CNAME | Maps domain to another domain name |
| Alias Record | AWS record that maps to AWS resources (free) |
| Hosted Zone | Container for DNS records |
| TTL | Time to Live, how long DNS is cached |
| Health Check | Monitors endpoint availability |
| Zone Apex | Root domain (example.com, not www.example.com) |

## 💡 Key Takeaways

1. Route 53 provides DNS, domain registration, and health checking
2. Alias records are free for AWS resources and work at zone apex
3. Use weighted routing for gradual deployments and A/B testing
4. Latency-based routing improves global application performance
5. Failover routing with health checks enables disaster recovery
6. Geolocation routing serves localized content based on user location
7. Route 53 has a 100% availability SLA - highly reliable for DNS

---

*Previous: [02 - VPC Security](../02-vpc-security/readme.md) | Next: [04 - Connectivity Options](../04-connectivity-options/readme.md)*

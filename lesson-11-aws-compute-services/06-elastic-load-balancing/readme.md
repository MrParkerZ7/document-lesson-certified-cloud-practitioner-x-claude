# ⚖️ Elastic Load Balancing (ELB)

## File Structure

```
lesson-11-aws-compute-services/
└── 06-elastic-load-balancing/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses. It improves the availability and fault tolerance of your applications.

## What is Load Balancing?

```
+------------------------------------------------------------------+
|                    ELASTIC LOAD BALANCING                         |
+------------------------------------------------------------------+
|                                                                   |
|   Without Load Balancer           With Load Balancer              |
|                                                                   |
|   Users                           Users                           |
|     |                               |                             |
|     v                               v                             |
|   +------+                   +------------+                       |
|   | EC2  |                   |    ELB     |                       |
|   +------+                   +------------+                       |
|     |                          /   |   \                          |
|   Single point               v    v    v                          |
|   of failure!             +----+----+----+                        |
|                           |EC2 |EC2 |EC2 |                        |
|                           +----+----+----+                        |
|                           High availability!                      |
|                                                                   |
+------------------------------------------------------------------+
```

## ELB Benefits

| Benefit | Description |
|---------|-------------|
| High availability | Distributes traffic across AZs |
| Health checks | Routes only to healthy targets |
| Automatic scaling | Handles varying traffic loads |
| Security | SSL/TLS termination, WAF integration |
| Elasticity | Automatically scales capacity |

## Types of Load Balancers

| Type | Layer | Use Case |
|------|-------|----------|
| Application Load Balancer (ALB) | Layer 7 (HTTP/HTTPS) | Web applications, microservices |
| Network Load Balancer (NLB) | Layer 4 (TCP/UDP) | Ultra-low latency, high throughput |
| Gateway Load Balancer (GWLB) | Layer 3 | Third-party virtual appliances |
| Classic Load Balancer | Layer 4/7 | Legacy (deprecated) |

## Application Load Balancer (ALB)

```
+------------------------------------------------------------------+
|               APPLICATION LOAD BALANCER (ALB)                     |
+------------------------------------------------------------------+
|                                                                   |
|   Layer 7 (HTTP/HTTPS) - Content-based routing                    |
|                                                                   |
|   Client Requests                                                 |
|        |                                                          |
|        v                                                          |
|   +------------------+                                            |
|   |       ALB        |                                            |
|   | Content-based    |                                            |
|   | routing rules    |                                            |
|   +------------------+                                            |
|     |           |           |                                     |
|     | /api/*    | /images/* | /orders/*                           |
|     v           v           v                                     |
|   +------+   +------+   +------+                                  |
|   | API  |   | Image|   | Order|   Target Groups                  |
|   | TG   |   | TG   |   | TG   |                                  |
|   +------+   +------+   +------+                                  |
|                                                                   |
+------------------------------------------------------------------+
```

## ALB Features

| Feature | Description |
|---------|-------------|
| Path-based routing | Route by URL path (/api, /images) |
| Host-based routing | Route by hostname (api.example.com) |
| HTTP/HTTPS | Native HTTP/2 support |
| WebSockets | Native WebSocket support |
| Redirects | URL redirects and fixed responses |
| Authentication | Integrates with Cognito, OIDC |

## Network Load Balancer (NLB)

```
+------------------------------------------------------------------+
|               NETWORK LOAD BALANCER (NLB)                         |
+------------------------------------------------------------------+
|                                                                   |
|   Layer 4 (TCP/UDP/TLS) - Connection-based                        |
|                                                                   |
|   • Ultra-low latency (microseconds)                              |
|   • Millions of requests per second                               |
|   • Static IP per AZ                                              |
|   • Elastic IP support                                            |
|                                                                   |
|   TCP/UDP Traffic                                                 |
|        |                                                          |
|        v                                                          |
|   +------------------+                                            |
|   |       NLB        |  Static IP / Elastic IP                    |
|   +------------------+                                            |
|     |           |           |                                     |
|     v           v           v                                     |
|   +------+   +------+   +------+                                  |
|   | EC2  |   | EC2  |   | EC2  |                                  |
|   +------+   +------+   +------+                                  |
|                                                                   |
+------------------------------------------------------------------+
```

## NLB Features

| Feature | Description |
|---------|-------------|
| Performance | Millions of requests per second |
| Latency | Ultra-low latency |
| Static IP | One static IP per AZ |
| Elastic IP | Assign your own Elastic IPs |
| Protocols | TCP, UDP, TLS |
| Preserve source IP | Client IP visible to targets |

## Gateway Load Balancer (GWLB)

| Feature | Description |
|---------|-------------|
| Purpose | Deploy virtual appliances |
| Layer | Layer 3 (IP packets) |
| Use cases | Firewalls, IDS/IPS, packet inspection |
| Protocol | GENEVE encapsulation |
| Integration | Third-party appliances |

## Load Balancer Comparison

| Feature | ALB | NLB | GWLB |
|---------|-----|-----|------|
| Layer | 7 | 4 | 3 |
| Protocol | HTTP/HTTPS | TCP/UDP/TLS | IP |
| Performance | High | Ultra-high | High |
| Static IP | No | Yes | N/A |
| Best for | Web apps | Low latency | Appliances |

## Target Groups

| Feature | Description |
|---------|-------------|
| Definition | Group of targets (EC2, containers, IPs) |
| Health checks | Monitor target health |
| Routing | Load balancer routes to target groups |
| Types | Instance, IP, Lambda (ALB only) |

## Target Types

| Type | Description | Supported By |
|------|-------------|--------------|
| Instance | EC2 instances | ALB, NLB |
| IP | IP addresses | ALB, NLB |
| Lambda | Lambda functions | ALB only |
| Application LB | Nested ALB | NLB only |

## Health Checks

| Setting | Description |
|---------|-------------|
| Protocol | HTTP, HTTPS, TCP |
| Path | URL path to check (HTTP/HTTPS) |
| Interval | Time between checks |
| Threshold | Healthy/unhealthy thresholds |
| Timeout | Time to wait for response |

## Listeners and Rules

```
+------------------------------------------------------------------+
|                   LISTENERS AND RULES                             |
+------------------------------------------------------------------+
|                                                                   |
|   Listener (Port 443 - HTTPS)                                     |
|   +----------------------------------------------------------+   |
|   |                                                           |   |
|   |   Rule 1: IF path is /api/* -> Forward to API Target Group|   |
|   |   Rule 2: IF path is /web/* -> Forward to Web Target Group|   |
|   |   Default: Forward to Default Target Group                |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## Cross-Zone Load Balancing

| Setting | ALB | NLB | Classic |
|---------|-----|-----|---------|
| Default | Enabled | Disabled | Disabled |
| Effect | Evenly distributes across all AZ targets | Each AZ balances its own targets | Each AZ balances its own targets |

## SSL/TLS Termination

| Feature | Description |
|---------|-------------|
| SSL Termination | Decrypt at load balancer |
| Benefit | Offload SSL processing |
| Certificate | ACM or IAM certificates |
| Backend | Can use HTTP or HTTPS to targets |

## Sticky Sessions

| Feature | Description |
|---------|-------------|
| Purpose | Route user to same target |
| Duration | Configurable (seconds to days) |
| Cookie | Application or load balancer generated |
| Use case | Stateful applications |

## ELB + Auto Scaling

```
+------------------------------------------------------------------+
|                  ELB + AUTO SCALING                               |
+------------------------------------------------------------------+
|                                                                   |
|   Users                                                           |
|     |                                                             |
|     v                                                             |
|   +------------------+                                            |
|   | Load Balancer    |                                            |
|   +------------------+                                            |
|     |         |         |                                         |
|     v         v         v                                         |
|   +------+ +------+ +------+                                      |
|   | EC2  | | EC2  | | EC2  |   Auto Scaling Group                 |
|   +------+ +------+ +------+                                      |
|                                                                   |
|   Auto Scaling:                                                   |
|   - Adds new instances to target group                            |
|   - Removes terminated instances                                  |
|   - ELB health checks trigger replacement                         |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **ALB** = Layer 7, HTTP/HTTPS, path/host-based routing
- **NLB** = Layer 4, TCP/UDP, ultra-low latency, static IP
- **GWLB** = Layer 3, for virtual appliances (firewalls)
- **Classic LB** = Legacy, avoid for new deployments
- **Target Groups** = groups of targets for routing
- **Health Checks** = ensure traffic goes to healthy targets
- **Cross-Zone** = enabled by default for ALB
- **SSL Termination** = decrypt HTTPS at load balancer
- **Sticky Sessions** = route user to same instance
- ELB works with **Auto Scaling** for elasticity

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Load Balancer | Distributes traffic across targets |
| Target Group | Collection of targets (EC2, IP, Lambda) |
| Listener | Checks for connection requests |
| Health Check | Monitors target health |
| Cross-Zone | Distribute across all targets in all AZs |
| SSL Termination | Decrypt SSL/TLS at load balancer |
| Sticky Session | Bind user session to specific target |

## 💡 Key Takeaways

1. ELB distributes traffic across multiple targets for high availability
2. ALB is Layer 7 for HTTP/HTTPS with content-based routing
3. NLB is Layer 4 for TCP/UDP with ultra-low latency
4. GWLB is Layer 3 for deploying virtual appliances
5. Target Groups organize targets for routing
6. Health checks ensure traffic only goes to healthy targets
7. Works seamlessly with Auto Scaling
8. SSL termination offloads encryption from instances

---

*Next: [Lesson 12 - AWS Database Services](../../lesson-12-aws-database-services/01-amazon-rds/readme.md)*

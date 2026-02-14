# ⚡ Content Delivery and Edge Services

## File Structure

```
lesson-13-aws-networking-services/
└── 05-content-delivery/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides services to deliver content to users with low latency by caching content at edge locations around the world. Amazon CloudFront is a Content Delivery Network (CDN) that caches content closer to users, while AWS Global Accelerator improves performance by routing traffic through AWS's global network.

## AWS Edge Infrastructure

```
+------------------------------------------------------------------+
|                    AWS EDGE LOCATIONS                             |
+------------------------------------------------------------------+
|                                                                   |
|   Edge Locations: 400+ locations in 90+ cities worldwide          |
|   Regional Edge Caches: 13 larger caches between origin and edge  |
|                                                                   |
|                    [Origin Server]                                |
|                          |                                        |
|                          v                                        |
|               [Regional Edge Cache]                               |
|                          |                                        |
|         +----------------+----------------+                       |
|         |                |                |                       |
|         v                v                v                       |
|   [Edge Loc 1]     [Edge Loc 2]     [Edge Loc 3]                 |
|         |                |                |                       |
|         v                v                v                       |
|   [Users in         [Users in        [Users in                   |
|    Tokyo]            London]          New York]                  |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon CloudFront

| Feature | Description |
|---------|-------------|
| Type | Content Delivery Network (CDN) |
| Purpose | Cache and deliver content globally |
| Edge Locations | 400+ worldwide |
| Content Types | Static, dynamic, streaming, APIs |
| Integration | S3, EC2, ELB, custom origins |
| Security | AWS Shield, WAF, HTTPS |

## How CloudFront Works

```
+------------------------------------------------------------------+
|                   CLOUDFRONT FLOW                                 |
+------------------------------------------------------------------+
|                                                                   |
|   WITHOUT CloudFront:                                             |
|   [User in Tokyo] -------- Long Distance -------> [Origin in US] |
|                     High latency, slow                            |
|                                                                   |
|   WITH CloudFront:                                                |
|   [User in Tokyo] --> [Edge in Tokyo] ........> [Origin in US]   |
|                        (Cache HIT)       (only on cache MISS)     |
|                     Fast response!                                |
|                                                                   |
|   First Request (Cache MISS):                                     |
|   1. User requests content                                        |
|   2. Edge checks cache - not found                                |
|   3. Edge fetches from origin                                     |
|   4. Edge caches and returns to user                              |
|                                                                   |
|   Subsequent Requests (Cache HIT):                                |
|   1. User requests content                                        |
|   2. Edge checks cache - FOUND!                                   |
|   3. Edge returns cached content immediately                      |
|                                                                   |
+------------------------------------------------------------------+
```

## CloudFront Origins

| Origin Type | Description | Use Case |
|-------------|-------------|----------|
| S3 Bucket | Static content from S3 | Images, CSS, JS, videos |
| S3 Static Website | S3 website endpoint | Static websites |
| EC2 Instance | Application on EC2 | Dynamic content |
| Elastic Load Balancer | Load-balanced apps | Web applications |
| Custom Origin | Any HTTP server | On-premises, other clouds |
| MediaPackage | Video streaming | Live and on-demand video |

## CloudFront Distribution Types

| Type | Description | Use Case |
|------|-------------|----------|
| Web Distribution | HTTP/HTTPS content | Websites, APIs, downloads |
| RTMP Distribution | Media streaming (deprecated) | Legacy video streaming |

## CloudFront Security Features

```
+------------------------------------------------------------------+
|                 CLOUDFRONT SECURITY                               |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+                                            |
|   | AWS Shield       | DDoS Protection (Standard = Free)         |
|   +------------------+                                            |
|            |                                                      |
|   +------------------+                                            |
|   | AWS WAF          | Web Application Firewall (optional)        |
|   +------------------+                                            |
|            |                                                      |
|   +------------------+                                            |
|   | CloudFront       | Edge Location                              |
|   | + HTTPS          | SSL/TLS encryption                        |
|   +------------------+                                            |
|            |                                                      |
|   +------------------+                                            |
|   | Origin Access    | Restrict S3 access to CloudFront only     |
|   | Control (OAC)    | (replaces OAI)                            |
|   +------------------+                                            |
|            |                                                      |
|   +------------------+                                            |
|   | Signed URLs/     | Restrict content to authorized users      |
|   | Signed Cookies   |                                            |
|   +------------------+                                            |
|                                                                   |
+------------------------------------------------------------------+
```

## CloudFront Security Options

| Feature | Description | Use Case |
|---------|-------------|----------|
| HTTPS | Encrypt viewer connections | All traffic |
| Origin Access Control | Restrict S3 to CloudFront | Private S3 content |
| Signed URLs | Time-limited access URLs | Premium content |
| Signed Cookies | Access multiple files | Subscription content |
| Geo-Restriction | Block/allow by country | Licensing, compliance |
| Field-Level Encryption | Encrypt specific fields | PII protection |
| AWS WAF | Web application firewall | SQL injection, XSS |
| AWS Shield | DDoS protection | Attacks mitigation |

## CloudFront Caching

| Concept | Description |
|---------|-------------|
| TTL | Time to Live, how long content is cached |
| Cache Key | What makes each cached object unique |
| Invalidation | Remove content from cache before TTL |
| Cache Behaviors | Different settings for different paths |

## CloudFront Pricing

| Component | Charged For |
|-----------|-------------|
| Data Transfer Out | Per GB transferred to viewers |
| HTTP Requests | Per 10,000 requests |
| Invalidation | First 1,000 paths free/month |
| Origin Shield | Optional, per request |
| Real-time Logs | Per log line |

## AWS Global Accelerator

| Feature | Description |
|---------|-------------|
| Purpose | Improve global application performance |
| Method | Routes traffic through AWS global network |
| Endpoints | EC2, ELB, Elastic IP |
| Static IPs | Two anycast static IP addresses |
| Health Checks | Automatic failover |
| Use Case | Non-HTTP apps, consistent latency |

## Global Accelerator Architecture

```
+------------------------------------------------------------------+
|                  GLOBAL ACCELERATOR                               |
+------------------------------------------------------------------+
|                                                                   |
|   WITHOUT Global Accelerator:                                     |
|   [User] --> Internet hops --> Internet hops --> [AWS Region]    |
|              (Variable latency, many hops)                        |
|                                                                   |
|   WITH Global Accelerator:                                        |
|   [User] --> [Edge Location] --> AWS Private Network --> [Region] |
|              (Enter AWS quickly)  (Fast, reliable)                |
|                                                                   |
|                    Static Anycast IPs                             |
|                   (192.0.2.1, 192.0.2.2)                          |
|                          |                                        |
|                          v                                        |
|                   [Edge Location]                                 |
|                          |                                        |
|            +-------------+-------------+                          |
|            |             |             |                          |
|            v             v             v                          |
|     [us-east-1]   [eu-west-1]   [ap-south-1]                     |
|     (Primary)     (Secondary)   (Secondary)                       |
|                                                                   |
|   Automatic failover to healthy endpoints                         |
|                                                                   |
+------------------------------------------------------------------+
```

## CloudFront vs. Global Accelerator

| Feature | CloudFront | Global Accelerator |
|---------|------------|-------------------|
| Purpose | Cache content at edge | Route to optimal endpoint |
| Content Caching | Yes | No |
| Static IPs | No (use DNS names) | Yes (2 anycast IPs) |
| Protocols | HTTP/HTTPS | TCP/UDP |
| Best For | Static/dynamic content | Non-HTTP, gaming, IoT |
| Price | Data transfer + requests | Hourly + data transfer |

## Use Case Comparison

```
+------------------------------------------------------------------+
|            WHEN TO USE WHICH SERVICE                              |
+------------------------------------------------------------------+
|                                                                   |
|   USE CLOUDFRONT WHEN:                                            |
|   - Serving static content (images, videos, JS, CSS)              |
|   - Caching dynamic API responses                                 |
|   - You need content caching to reduce origin load                |
|   - Streaming video content                                       |
|   - Website acceleration                                          |
|                                                                   |
|   USE GLOBAL ACCELERATOR WHEN:                                    |
|   - Non-HTTP protocols (TCP, UDP, gaming, IoT)                    |
|   - Need static IP addresses (whitelisting)                       |
|   - Instant regional failover required                            |
|   - Consistent performance to specific endpoints                  |
|   - Voice/Video over IP applications                              |
|                                                                   |
|   CAN USE BOTH:                                                   |
|   - Global Accelerator in front of CloudFront                     |
|   - Get static IPs + caching benefits                             |
|                                                                   |
+------------------------------------------------------------------+
```

## Edge Location Services Summary

| Service | Purpose | Key Feature |
|---------|---------|-------------|
| CloudFront | CDN, content delivery | Caches content at edge |
| Global Accelerator | Network optimization | Static IPs, AWS backbone |
| Route 53 | DNS routing | Multiple routing policies |
| Lambda@Edge | Edge compute | Run code at CloudFront edge |
| CloudFront Functions | Lightweight edge compute | Simple URL manipulation |

## Lambda@Edge vs. CloudFront Functions

| Feature | Lambda@Edge | CloudFront Functions |
|---------|-------------|---------------------|
| Runtime | Node.js, Python | JavaScript only |
| Execution Time | Up to 30 seconds | Sub-millisecond |
| Memory | Up to 10 GB | 2 MB |
| Network Access | Yes | No |
| Use Case | Complex logic | Simple transformations |
| Cost | Higher | Lower |

## 🎯 Exam Tips

- **CloudFront** is a CDN that caches content at edge locations globally
- **Edge locations** are different from Regions and AZs (400+ worldwide)
- CloudFront can serve content from S3, EC2, ELB, or custom origins
- **Origin Access Control (OAC)** restricts S3 access to CloudFront only
- CloudFront integrates with **AWS Shield** (DDoS) and **WAF** (web attacks)
- **Signed URLs/Cookies** provide time-limited access to private content
- **Global Accelerator** uses AWS global network for consistent performance
- Global Accelerator provides **two static anycast IP addresses**
- CloudFront = caching, Global Accelerator = routing (no caching)
- Use Global Accelerator for non-HTTP protocols (TCP/UDP, gaming, IoT)
- **CloudFront Functions** for simple tasks; **Lambda@Edge** for complex logic

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| CDN | Content Delivery Network, distributed content caching |
| Edge Location | AWS cache location close to end users |
| Origin | Source of content (S3, EC2, custom server) |
| Distribution | CloudFront configuration for content delivery |
| Cache Hit | Content found in edge cache |
| Cache Miss | Content not in cache, fetched from origin |
| Anycast | Multiple servers share same IP, route to nearest |
| TTL | Time to Live, cache duration |

## 💡 Key Takeaways

1. CloudFront caches content at 400+ edge locations worldwide for low latency
2. Origins can be S3, EC2, ELB, or any custom HTTP server
3. Use Origin Access Control to restrict S3 access to CloudFront only
4. CloudFront integrates with Shield and WAF for security
5. Global Accelerator routes traffic through AWS network for consistent performance
6. Global Accelerator provides static IPs; CloudFront uses DNS names
7. Choose CloudFront for caching, Global Accelerator for routing optimization

---

*Previous: [04 - Connectivity Options](../04-connectivity-options/readme.md)*

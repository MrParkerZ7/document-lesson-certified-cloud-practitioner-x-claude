# ⚡ Amazon CloudFront

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 04-amazon-cloudfront/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds. CloudFront integrates with AWS services and edge locations worldwide.

## What is CloudFront?

```
+------------------------------------------------------------------+
|                    AMAZON CLOUDFRONT                              |
+------------------------------------------------------------------+
|                                                                   |
|   CloudFront is a Content Delivery Network (CDN) that            |
|   caches content at edge locations close to users                 |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                    ORIGIN                                 |   |
|   |   +--------+   +--------+   +--------+   +--------+       |   |
|   |   |   S3   |   |   EC2  |   |   ALB  |   | Custom |       |   |
|   |   | Bucket |   |        |   |        |   | Origin |       |   |
|   |   +--------+   +--------+   +--------+   +--------+       |   |
|   +----------------------------------------------------------+   |
|                              |                                    |
|                              v                                    |
|   +----------------------------------------------------------+   |
|   |               CLOUDFRONT DISTRIBUTION                     |   |
|   |                 (Global Edge Network)                     |   |
|   +----------------------------------------------------------+   |
|         |              |              |              |           |
|         v              v              v              v           |
|   +--------+     +--------+     +--------+     +--------+        |
|   | Edge   |     | Edge   |     | Edge   |     | Edge   |        |
|   | Tokyo  |     | London |     | Sydney |     | NYC    |        |
|   +--------+     +--------+     +--------+     +--------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## CloudFront Key Components

| Component | Description |
|-----------|-------------|
| Distribution | Configuration for content delivery |
| Origin | Source of content (S3, EC2, ALB, custom) |
| Edge Location | Cache location close to users |
| Regional Edge Cache | Larger cache between edge and origin |
| Behaviors | Rules for how requests are handled |

## CloudFront Origins

| Origin Type | Use Case |
|-------------|----------|
| S3 Bucket | Static content, websites |
| EC2 Instance | Dynamic content |
| Application Load Balancer | Load-balanced applications |
| API Gateway | API endpoints |
| MediaStore | Video streaming |
| Custom Origin | Any HTTP server |

## How CloudFront Works

```
+------------------------------------------------------------------+
|                  CLOUDFRONT REQUEST FLOW                          |
+------------------------------------------------------------------+
|                                                                   |
|   1. User Request     2. DNS Resolution    3. Edge Check         |
|   +----------+        +----------+         +----------+          |
|   | User     | -----> | Route 53 | -----> | CloudFront|          |
|   | Browser  |        | DNS      |         | Edge     |          |
|   +----------+        +----------+         +----------+          |
|                                                  |                |
|                           +-----------+----------+                |
|                           |                      |                |
|                           v                      v                |
|                    +----------+           +----------+            |
|                    |Cache Hit |           |Cache Miss|            |
|                    |Return    |           |Fetch from|            |
|                    |Content   |           |Origin    |            |
|                    +----------+           +----------+            |
|                                                                   |
+------------------------------------------------------------------+
```

## CloudFront Features

| Feature | Description |
|---------|-------------|
| HTTPS | SSL/TLS encryption |
| Custom domains | Use your own domain names |
| Geo-restriction | Block or allow by country |
| Signed URLs | Secure private content |
| Lambda@Edge | Run code at edge |
| Field-level encryption | Encrypt sensitive data |
| Origin failover | Automatic failover |

## CloudFront Security

| Feature | Description |
|---------|-------------|
| AWS WAF | Web application firewall integration |
| AWS Shield | DDoS protection (Standard included) |
| HTTPS | TLS encryption in transit |
| OAC | Origin Access Control for S3 |
| Signed URLs/Cookies | Private content access |
| Geo-blocking | Restrict by geography |

## CloudFront Pricing

| Factor | Description |
|--------|-------------|
| Data transfer out | Per GB transferred |
| HTTP/HTTPS requests | Per 10,000 requests |
| Invalidation | First 1,000 free/month |
| Field encryption | Per request |
| Lambda@Edge | Per request + duration |

## CloudFront vs Direct Origin

| Aspect | CloudFront | Direct Origin |
|--------|------------|---------------|
| Latency | Low (cached locally) | Higher |
| Origin load | Reduced | Full load |
| Cost | CDN + origin | Origin only |
| Global reach | 400+ locations | Single location |
| DDoS protection | Included | Must configure |

## Cache Behaviors

| Setting | Description |
|---------|-------------|
| Path pattern | Match URLs (e.g., /images/*) |
| TTL | Time to cache content |
| Query strings | Include or exclude |
| Headers | Forward or cache based on |
| Cookies | Forward or ignore |

## CloudFront Use Cases

| Use Case | Description |
|----------|-------------|
| Static websites | Host from S3 with CloudFront |
| Video streaming | Low-latency video delivery |
| API acceleration | Faster API responses |
| Software downloads | Global software distribution |
| Dynamic content | Cache dynamic pages |

## Integration with AWS Services

| Service | Integration |
|---------|------------|
| S3 | Primary origin for static content |
| EC2/ALB | Origin for dynamic content |
| Route 53 | DNS management |
| ACM | Free SSL/TLS certificates |
| WAF | Web application firewall |
| Lambda@Edge | Edge computing |

## 🎯 Exam Tips

- **CloudFront** = CDN for low-latency content delivery
- Uses **400+ edge locations** worldwide
- Origins: **S3**, **EC2**, **ALB**, **custom HTTP**
- **Shield Standard** DDoS protection included free
- **OAC** (Origin Access Control) restricts S3 access to CloudFront
- **Lambda@Edge** runs code at edge locations
- **Signed URLs** for private content
- **Geo-restriction** blocks or allows by country

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| CDN | Content Delivery Network |
| Distribution | CloudFront configuration |
| Origin | Source of content |
| Edge Location | Cache location |
| TTL | Time To Live (cache duration) |
| OAC | Origin Access Control |

## 💡 Key Takeaways

1. CloudFront is AWS's global CDN service
2. Content is cached at 400+ edge locations
3. Supports multiple origin types (S3, EC2, ALB, custom)
4. Includes DDoS protection via Shield Standard
5. Integrates with WAF for web application security
6. Lambda@Edge enables edge computing
7. Reduces latency and offloads origin servers

---

*Next: [05 - AWS Local Zones](../05-aws-local-zones/readme.md)*

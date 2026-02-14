# 📍 Edge Locations and Points of Presence

## File Structure

```
lesson-10-aws-global-infrastructure/
└── 03-edge-locations-and-points-of-presence/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Edge Locations and Points of Presence (PoPs) are sites deployed in major cities and highly populated areas around the world. They are used to cache content closer to end users, reducing latency and improving the user experience for services like CloudFront and Route 53.

## What are Edge Locations?

```
+------------------------------------------------------------------+
|                     EDGE LOCATIONS                                |
+------------------------------------------------------------------+
|                                                                   |
|   Edge locations are data centers outside of AWS Regions          |
|   used to cache content and deliver it to users with low latency  |
|                                                                   |
|              User                                                 |
|               |                                                   |
|               v                                                   |
|      +------------------+                                         |
|      |  Edge Location   |  <-- Closest to user                    |
|      |  (Content Cache) |                                         |
|      +------------------+                                         |
|               |                                                   |
|               | (Only if cache miss)                              |
|               v                                                   |
|      +------------------+                                         |
|      |  Regional Cache  |                                         |
|      +------------------+                                         |
|               |                                                   |
|               v                                                   |
|      +------------------+                                         |
|      |  Origin (S3/EC2) |  <-- AWS Region                         |
|      +------------------+                                         |
|                                                                   |
+------------------------------------------------------------------+
```

## Points of Presence (PoPs)

| Component | Description |
|-----------|-------------|
| Edge Locations | Cache content for CloudFront |
| Regional Edge Caches | Larger caches between edge and origin |
| Total PoPs | 400+ locations worldwide |
| Countries | 90+ countries and territories |

## Edge Locations vs Regions

| Aspect | Edge Locations | Regions |
|--------|----------------|---------|
| Purpose | Content delivery, caching | Full compute and storage |
| Number | 400+ | 30+ |
| Services | CloudFront, Route 53, Lambda@Edge | All AWS services |
| Location | Major cities worldwide | Strategic geographic areas |

## Services Using Edge Locations

| Service | Use of Edge Location |
|---------|---------------------|
| CloudFront | Cache and deliver content |
| Route 53 | DNS resolution at the edge |
| Lambda@Edge | Run code at edge locations |
| CloudFront Functions | Lightweight edge computing |
| AWS Global Accelerator | Entry point for traffic |
| AWS WAF | Web application firewall at edge |
| AWS Shield | DDoS protection at edge |

## How Edge Locations Work

```
+------------------------------------------------------------------+
|                  CLOUDFRONT DELIVERY FLOW                         |
+------------------------------------------------------------------+
|                                                                   |
|   1. User Request     2. Edge Check       3. Cache Miss           |
|   +----------+        +------------+      +------------+          |
|   | User in  | -----> | Edge       | ---> | Regional   |          |
|   | Tokyo    |        | Location   |      | Cache      |          |
|   +----------+        | (Tokyo)    |      +------------+          |
|                       +------------+            |                 |
|                            |                    |                 |
|                            v                    v                 |
|   4. Cache Hit        +------------+      +------------+          |
|   Return cached  <--- |  Content   | <--- | Origin     |          |
|   content quickly     |  Cached    |      | (S3/EC2)   |          |
|                       +------------+      +------------+          |
|                                                                   |
+------------------------------------------------------------------+
```

## Global Distribution

| Region | Edge Location Cities (Examples) |
|--------|--------------------------------|
| North America | New York, Los Angeles, Dallas, Miami |
| Europe | London, Paris, Frankfurt, Amsterdam |
| Asia Pacific | Tokyo, Singapore, Sydney, Mumbai |
| South America | São Paulo, Rio de Janeiro |
| Middle East | Dubai, Tel Aviv |
| Africa | Johannesburg, Cape Town |

## Benefits of Edge Locations

| Benefit | Description |
|---------|-------------|
| Low latency | Content served from nearby location |
| Improved performance | Faster page loads |
| Reduced origin load | Less traffic to origin servers |
| Global reach | 400+ locations worldwide |
| DDoS protection | Shield and WAF at edge |
| Cost efficiency | Reduced data transfer from origin |

## Regional Edge Caches

| Feature | Description |
|---------|-------------|
| Purpose | Larger, secondary cache |
| Location | Between edge and origin |
| Capacity | More storage than edge locations |
| Use case | Less popular content |

## Lambda@Edge

Run code at edge locations to customize content delivery.

| Use Case | Example |
|----------|---------|
| Authentication | Validate tokens at edge |
| URL rewriting | Clean URLs |
| A/B testing | Route users to different versions |
| Header manipulation | Add/modify headers |
| Bot detection | Block malicious bots |

## Edge Location Security

| Feature | Description |
|---------|-------------|
| AWS Shield Standard | DDoS protection (included) |
| AWS Shield Advanced | Enhanced DDoS protection |
| AWS WAF | Web application firewall |
| SSL/TLS | Encrypted connections |
| Origin protection | Hide origin servers |

## Edge Locations Numbers

| Metric | Count (approx) |
|--------|----------------|
| Edge locations | 400+ |
| Regional edge caches | 13 |
| Countries | 90+ |
| Cities | 300+ |

## 🎯 Exam Tips

- **Edge locations** = content caching (NOT for running EC2)
- **400+** edge locations vs **30+** regions
- Used by **CloudFront**, **Route 53**, **Lambda@Edge**
- Edge locations are in **major cities** worldwide
- **Regional edge caches** are larger caches between edge and origin
- **Lambda@Edge** runs code at edge locations
- Edge locations provide **DDoS protection** via Shield

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Edge Location | Data center for caching content |
| Point of Presence | Edge location or regional cache |
| Regional Edge Cache | Larger cache between edge and origin |
| Lambda@Edge | Code execution at edge |
| Cache Hit | Content found in cache |
| Cache Miss | Content not in cache, fetch from origin |

## 💡 Key Takeaways

1. Edge locations cache content closer to end users
2. AWS has 400+ edge locations in 90+ countries
3. CloudFront, Route 53, and Lambda@Edge use edge locations
4. Edge locations are NOT the same as Regions
5. Regional edge caches provide additional caching layer
6. Edge locations improve latency and performance
7. Security features like WAF and Shield run at edge

---

*Next: [04 - Amazon CloudFront](../04-amazon-cloudfront/readme.md)*

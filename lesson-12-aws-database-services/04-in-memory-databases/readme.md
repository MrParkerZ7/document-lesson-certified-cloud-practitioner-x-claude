# ⚡ In-Memory Databases (Amazon ElastiCache)

## Introduction

Amazon ElastiCache is a fully managed in-memory data store and cache service. It supports two popular open-source in-memory engines: Redis and Memcached. ElastiCache provides microsecond latency, making it ideal for caching, session management, and real-time applications.

## What is In-Memory Caching?

In-memory caching stores frequently accessed data in RAM for ultra-fast retrieval, reducing the load on primary databases.

```
+------------------------------------------------------------------+
|                   HOW CACHING WORKS                               |
+------------------------------------------------------------------+
|                                                                   |
|   WITHOUT CACHE                       WITH CACHE                  |
|   +----------+                        +----------+                |
|   |   App    |                        |   App    |                |
|   +----+-----+                        +----+-----+                |
|        |                                   |                      |
|        | Every request                     | 1. Check cache       |
|        |                                   v                      |
|        v                              +----------+                |
|   +----------+                        | Elasti-  | Cache hit:     |
|   |   RDS    |  50-100ms              | Cache    | <1ms           |
|   | Database |                        +----+-----+                |
|   +----------+                             |                      |
|                                            | 2. Cache miss        |
|                                            v                      |
|                                       +----------+                |
|                                       |   RDS    |                |
|                                       | Database |                |
|                                       +----------+                |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon ElastiCache Overview

| Feature | Description |
|---------|-------------|
| Type | Fully managed in-memory data store |
| Engines | Redis and Memcached |
| Latency | Sub-millisecond (microsecond) |
| Scalability | Horizontal scaling with sharding |
| Availability | Multi-AZ with automatic failover |
| Use Cases | Caching, session stores, real-time analytics |

## Redis vs Memcached

ElastiCache supports two in-memory engines with different characteristics.

```
+------------------------------------------------------------------+
|                    REDIS vs MEMCACHED                             |
+------------------------------------------------------------------+
|                                                                   |
|   REDIS (Feature Rich)                MEMCACHED (Simple)          |
|   +------------------------+          +------------------------+  |
|   | - Data structures      |          | - Simple key-value     |  |
|   | - Persistence          |          | - Multi-threaded       |  |
|   | - Replication          |          | - No persistence       |  |
|   | - Pub/Sub messaging    |          | - No replication       |  |
|   | - Transactions         |          | - Simple caching       |  |
|   | - Lua scripting        |          |                        |  |
|   | - Geospatial           |          |                        |  |
|   +------------------------+          +------------------------+  |
|                                                                   |
+------------------------------------------------------------------+
```

### Detailed Comparison

| Feature | Redis | Memcached |
|---------|-------|-----------|
| Data Types | Strings, hashes, lists, sets, sorted sets | Strings only |
| Persistence | Yes (snapshots, AOF) | No |
| Replication | Yes (Multi-AZ) | No |
| High Availability | Yes (automatic failover) | No |
| Sharding | Yes (cluster mode) | Yes |
| Multi-threaded | No (single-threaded) | Yes |
| Advanced Features | Pub/Sub, transactions, Lua | Basic caching |
| Backup/Restore | Yes | No |

### When to Choose Each

| Choose Redis When | Choose Memcached When |
|-------------------|----------------------|
| Need data persistence | Simple caching only |
| Need complex data types | Need multi-threading |
| Need replication/failover | Simple key-value storage |
| Need Pub/Sub messaging | Need to scale out horizontally |
| Need sorted sets (leaderboards) | Cost is primary concern |
| Need geospatial capabilities | |

## ElastiCache Architecture

### Redis Cluster Mode

```
+------------------------------------------------------------------+
|                  REDIS CLUSTER MODE                               |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                    Redis Cluster                          |   |
|   |                                                           |   |
|   |   Shard 1           Shard 2           Shard 3             |   |
|   |   +----------+      +----------+      +----------+        |   |
|   |   | Primary  |      | Primary  |      | Primary  |        |   |
|   |   +----+-----+      +----+-----+      +----+-----+        |   |
|   |        |                 |                 |              |   |
|   |   +----+-----+      +----+-----+      +----+-----+        |   |
|   |   | Replica  |      | Replica  |      | Replica  |        |   |
|   |   +----------+      +----------+      +----------+        |   |
|   |                                                           |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   - Data partitioned across shards                                |
|   - Each shard has primary + replicas for HA                      |
|   - Automatic failover within shards                              |
|                                                                   |
+------------------------------------------------------------------+
```

### Memcached Architecture

```
+------------------------------------------------------------------+
|                  MEMCACHED CLUSTER                                |
+------------------------------------------------------------------+
|                                                                   |
|   +----------+    +----------+    +----------+    +----------+   |
|   |  Node 1  |    |  Node 2  |    |  Node 3  |    |  Node 4  |   |
|   |  Cache   |    |  Cache   |    |  Cache   |    |  Cache   |   |
|   +----------+    +----------+    +----------+    +----------+   |
|                                                                   |
|   - No replication between nodes                                  |
|   - Data distributed via consistent hashing                       |
|   - Scale by adding more nodes                                    |
|   - If node fails, data on that node is lost                      |
|                                                                   |
+------------------------------------------------------------------+
```

## ElastiCache Use Cases

| Use Case | Description | Recommended Engine |
|----------|-------------|--------------------|
| Database Caching | Cache database queries | Redis or Memcached |
| Session Store | Store user session data | Redis (persistence) |
| Gaming Leaderboards | Real-time sorted rankings | Redis (sorted sets) |
| Real-time Analytics | Fast aggregations | Redis |
| Message Queue | Pub/Sub messaging | Redis |
| Geospatial | Location-based features | Redis |
| Simple Caching | Basic key-value cache | Memcached |

## Caching Strategies

### Lazy Loading (Cache-Aside)

```
+------------------------------------------------------------------+
|                    LAZY LOADING                                   |
+------------------------------------------------------------------+
|                                                                   |
|   1. App requests data                                            |
|   2. Check cache                                                  |
|   3. If miss, fetch from DB                                       |
|   4. Store in cache                                               |
|   5. Return data                                                  |
|                                                                   |
|   +-----+     1      +-------+     3      +----+                  |
|   | App |----------->| Cache |----------->| DB |                  |
|   +-----+<-----------+-------+<-----------+----+                  |
|              5 (hit)     ^         4                              |
|                          |                                        |
|                    2. Check first                                 |
|                                                                   |
|   Pros: Only caches what's needed                                 |
|   Cons: Cache miss = slower first request                         |
|                                                                   |
+------------------------------------------------------------------+
```

### Write-Through

```
+------------------------------------------------------------------+
|                    WRITE-THROUGH                                  |
+------------------------------------------------------------------+
|                                                                   |
|   1. App writes data                                              |
|   2. Write to cache AND database                                  |
|                                                                   |
|   +-----+            +-------+                                    |
|   | App |----------->| Cache |---------+                          |
|   +-----+            +-------+         |                          |
|                          |             |                          |
|                          v             v                          |
|                      +------+      +------+                       |
|                      | Cache|      |  DB  |                       |
|                      +------+      +------+                       |
|                                                                   |
|   Pros: Cache always has latest data                              |
|   Cons: Write latency, caches unused data                         |
|                                                                   |
+------------------------------------------------------------------+
```

## ElastiCache Security

| Security Feature | Description |
|------------------|-------------|
| VPC | Deploy within your VPC |
| Security Groups | Control inbound/outbound traffic |
| Encryption at Rest | KMS encryption (Redis only) |
| Encryption in Transit | TLS connections (Redis only) |
| AUTH | Password protection (Redis only) |
| IAM | Control API access |

## ElastiCache vs DynamoDB DAX

| Feature | ElastiCache | DynamoDB DAX |
|---------|-------------|--------------|
| Purpose | General-purpose caching | DynamoDB-specific caching |
| Compatibility | Any application | DynamoDB only |
| Engines | Redis, Memcached | Proprietary |
| Management | More configuration | Fully managed |
| Use Case | Multi-database caching | DynamoDB acceleration |
| API | Redis/Memcached APIs | DynamoDB API compatible |

## 🎯 Exam Tips

- **ElastiCache** = managed in-memory caching (Redis or Memcached)
- **Redis** = more features (persistence, replication, data structures)
- **Memcached** = simpler, multi-threaded, basic caching
- Use **Redis** for leaderboards (sorted sets), session stores, Pub/Sub
- Use **Memcached** for simple caching where persistence isn't needed
- ElastiCache provides **microsecond latency** (sub-millisecond)
- Caching reduces load on primary databases
- **ElastiCache** = general caching; **DAX** = DynamoDB-specific caching
- ElastiCache requires you to **modify application code** to use the cache

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| ElastiCache | AWS managed in-memory caching service |
| Redis | In-memory data structure store with persistence |
| Memcached | Simple, high-performance distributed cache |
| Cache Hit | Data found in cache |
| Cache Miss | Data not in cache, must fetch from database |
| TTL | Time to Live - how long data stays in cache |
| Lazy Loading | Cache data only when requested |
| Write-Through | Cache data when written to database |
| Sharding | Distributing data across multiple nodes |

## 💡 Key Takeaways

1. ElastiCache provides microsecond latency for in-memory caching
2. Redis offers persistence, replication, and advanced data structures
3. Memcached is simpler and multi-threaded for basic caching needs
4. Caching reduces database load and improves application performance
5. Choose Redis for complex requirements; Memcached for simple caching
6. ElastiCache requires application code changes (unlike DAX for DynamoDB)
7. Common use cases include session stores, leaderboards, and database caching

---

*Previous: [03 - NoSQL Databases](../03-nosql-databases/readme.md) | Next: [05 - Other Database Services](../05-other-database-services/readme.md)*

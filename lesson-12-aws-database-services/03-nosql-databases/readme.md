# 🗄️ NoSQL Databases (Amazon DynamoDB)

## File Structure

```
lesson-12-aws-database-services/
└── 03-nosql-databases/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Amazon DynamoDB is a fully managed, serverless, key-value and document NoSQL database designed to run high-performance applications at any scale. It is one of the most important services to understand for the AWS Cloud Practitioner exam.

## What is NoSQL?

NoSQL databases are non-relational databases that provide flexible schemas and are designed for horizontal scaling.

```
+------------------------------------------------------------------+
|                     NoSQL vs RELATIONAL                           |
+------------------------------------------------------------------+
|                                                                   |
|   RELATIONAL (SQL)                   NoSQL                        |
|   +------------------+               +------------------+         |
|   | ID | Name | Dept |               | {                |         |
|   |----|------|------|               |   "id": "123",   |         |
|   | 1  | John | IT   |               |   "name": "John",|         |
|   | 2  | Jane | HR   |               |   "dept": "IT",  |         |
|   | 3  | Bob  | IT   |               |   "skills": [...] |        |
|   +------------------+               | }                |         |
|                                      +------------------+         |
|   Fixed schema                       Flexible schema              |
|   Vertical scaling                   Horizontal scaling           |
|   Complex queries                    Simple queries               |
|                                                                   |
+------------------------------------------------------------------+
```

## NoSQL Database Types

| Type | Description | AWS Service | Example Use Case |
|------|-------------|-------------|------------------|
| Key-Value | Simple key-value pairs | DynamoDB | Session management, caching |
| Document | JSON-like documents | DynamoDB, DocumentDB | Content management, catalogs |
| Graph | Nodes and relationships | Neptune | Social networks, recommendations |
| Wide-Column | Column families | Keyspaces | Time-series, IoT data |

## Amazon DynamoDB Overview

```
+------------------------------------------------------------------+
|                      AMAZON DYNAMODB                              |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                  FULLY MANAGED                            |   |
|   |  - No servers to manage       - Auto-scaling              |   |
|   |  - Built-in security          - Continuous backups        |   |
|   |  - Global replication         - In-memory caching         |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |                  KEY FEATURES                             |   |
|   |  - Single-digit millisecond latency at any scale          |   |
|   |  - Serverless (no capacity planning needed)               |   |
|   |  - 99.999% availability (Global Tables)                   |   |
|   +----------------------------------------------------------+   |
|                                                                   |
+------------------------------------------------------------------+
```

## DynamoDB Core Concepts

### Tables, Items, and Attributes

```
+------------------------------------------------------------------+
|                    DYNAMODB DATA MODEL                            |
+------------------------------------------------------------------+
|                                                                   |
|   TABLE: Users                                                    |
|   +--------------------------------------------------------------+|
|   |                                                               ||
|   |  ITEM (like a row)                                            ||
|   |  +-----------------------------------------------------------+||
|   |  | Partition Key | Sort Key | Attribute | Attribute |        |||
|   |  | (user_id)     | (date)   | (name)    | (email)   |        |||
|   |  |---------------|----------|-----------|-----------|        |||
|   |  | "user123"     | "2024-01"| "John"    | "j@..."   |        |||
|   |  +-----------------------------------------------------------+||
|   |                                                               ||
|   |  ITEM                                                         ||
|   |  +-----------------------------------------------------------+||
|   |  | "user456"     | "2024-01"| "Jane"    | "jane@..."|"NYC"   |||
|   |  +-----------------------------------------------------------+||
|   |  ^ Note: Items can have different attributes (flexible)       ||
|   |                                                               ||
|   +--------------------------------------------------------------+|
|                                                                   |
+------------------------------------------------------------------+
```

| Concept | Description |
|---------|-------------|
| Table | Collection of items (like a table in RDBMS) |
| Item | Individual record in a table (like a row) |
| Attribute | Data element within an item (like a column) |
| Partition Key | Primary key, used to distribute data |
| Sort Key | Optional, enables range queries |

### Primary Key Types

| Key Type | Description | Example |
|----------|-------------|---------|
| Partition Key Only | Simple primary key | user_id = "user123" |
| Partition + Sort Key | Composite primary key | user_id + order_date |

## DynamoDB Capacity Modes

| Mode | Description | Best For |
|------|-------------|----------|
| On-Demand | Pay per request, auto-scales | Unpredictable workloads |
| Provisioned | Specify read/write capacity | Predictable workloads |

### Capacity Mode Comparison

```
+------------------------------------------------------------------+
|                    CAPACITY MODES                                 |
+------------------------------------------------------------------+
|                                                                   |
|   ON-DEMAND                           PROVISIONED                 |
|   +------------------------+          +------------------------+  |
|   |  - Pay per request     |          |  - Set RCU/WCU         |  |
|   |  - Instant scaling     |          |  - Auto Scaling option |  |
|   |  - No capacity planning|          |  - Predictable costs   |  |
|   |  - Higher per-request  |          |  - Lower unit cost     |  |
|   |    cost                |          |  - Reserved capacity   |  |
|   +------------------------+          +------------------------+  |
|                                                                   |
|   Best for: New apps,                 Best for: Stable,          |
|   variable traffic                    predictable workloads       |
|                                                                   |
+------------------------------------------------------------------+
```

| Term | Definition |
|------|------------|
| RCU | Read Capacity Unit (4KB per second) |
| WCU | Write Capacity Unit (1KB per second) |

## DynamoDB Features

### Global Tables

Multi-region, fully replicated tables for globally distributed applications.

```
+------------------------------------------------------------------+
|                     GLOBAL TABLES                                 |
+------------------------------------------------------------------+
|                                                                   |
|   +----------------+         +----------------+                   |
|   |  US-EAST-1     |<------->|  EU-WEST-1     |                   |
|   |  (Primary)     | Multi-  |  (Replica)     |                   |
|   |                | master  |                |                   |
|   +----------------+         +----------------+                   |
|          ^                          ^                             |
|          |       +----------------+ |                             |
|          +------>|  AP-SOUTHEAST-1|<+                             |
|                  |  (Replica)     |                               |
|                  +----------------+                               |
|                                                                   |
|   - Active-active replication                                     |
|   - Low-latency reads/writes in any region                        |
|   - 99.999% availability                                          |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Replication | Multi-region, multi-master |
| Latency | Local read/write performance |
| Consistency | Eventually consistent globally |
| Availability | 99.999% SLA |

### DynamoDB Accelerator (DAX)

```
+------------------------------------------------------------------+
|                    DYNAMODB ACCELERATOR (DAX)                     |
+------------------------------------------------------------------+
|                                                                   |
|   Application                                                     |
|       |                                                           |
|       v                                                           |
|   +----------+                                                    |
|   |   DAX    |  Microsecond latency                               |
|   |  Cache   |  In-memory caching                                 |
|   +----+-----+                                                    |
|        |                                                          |
|        v                                                          |
|   +----------+                                                    |
|   | DynamoDB |  Millisecond latency                               |
|   |  Table   |                                                    |
|   +----------+                                                    |
|                                                                   |
|   DAX: Up to 10x read performance improvement                     |
|                                                                   |
+------------------------------------------------------------------+
```

| DAX Feature | Description |
|-------------|-------------|
| Latency | Microseconds vs milliseconds |
| Compatibility | API compatible with DynamoDB |
| Scaling | Add nodes to scale |
| Use Case | Read-heavy workloads |

### Other DynamoDB Features

| Feature | Description |
|---------|-------------|
| Point-in-Time Recovery | Restore table to any point in last 35 days |
| On-Demand Backup | Manual backups anytime |
| Encryption | At-rest (default), in-transit |
| Streams | Capture changes for event-driven apps |
| TTL | Automatically delete expired items |
| Transactions | ACID transactions across items |

## DynamoDB Use Cases

| Use Case | Why DynamoDB |
|----------|--------------|
| Gaming Leaderboards | High throughput, low latency |
| Session Management | Key-value access pattern |
| E-commerce Carts | Flexible schema, scalability |
| IoT Data | High write throughput |
| Mobile Backends | Serverless, auto-scaling |
| Real-time Analytics | Stream processing with DynamoDB Streams |

## DynamoDB vs RDS

| Aspect | DynamoDB | RDS |
|--------|----------|-----|
| Type | NoSQL (key-value/document) | Relational |
| Schema | Flexible | Fixed |
| Scaling | Horizontal (automatic) | Vertical (manual) |
| Latency | Single-digit milliseconds | Higher |
| Queries | Simple (key-based) | Complex (SQL, JOINs) |
| Transactions | Limited | Full ACID |
| Management | Serverless | Managed instances |
| Pricing | Per request or provisioned | Instance hours |

## 🎯 Exam Tips

- **DynamoDB** = serverless, key-value and document NoSQL database
- **Single-digit millisecond** latency at any scale
- **On-Demand mode** = pay per request, no capacity planning
- **Provisioned mode** = set RCU/WCU, lower cost for predictable workloads
- **Global Tables** = multi-region, multi-master replication
- **DAX** = in-memory cache for microsecond latency (10x improvement)
- DynamoDB is **fully managed** - no servers to provision
- **Partition Key** = required, determines data distribution
- **Sort Key** = optional, enables range queries
- Use DynamoDB for **simple queries**, RDS for **complex queries with JOINs**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| DynamoDB | AWS fully managed NoSQL database service |
| Partition Key | Primary key attribute for data distribution |
| Sort Key | Optional secondary key for range queries |
| RCU | Read Capacity Unit (4KB strongly consistent) |
| WCU | Write Capacity Unit (1KB per second) |
| Global Tables | Multi-region replication feature |
| DAX | DynamoDB Accelerator (in-memory cache) |
| DynamoDB Streams | Change data capture for event processing |
| TTL | Time to Live for automatic item expiration |

## 💡 Key Takeaways

1. DynamoDB is a serverless NoSQL database with single-digit millisecond latency
2. It supports both key-value and document data models
3. On-Demand mode requires no capacity planning; Provisioned mode offers cost savings
4. Global Tables provide multi-region, active-active replication
5. DAX (DynamoDB Accelerator) provides microsecond read latency via caching
6. DynamoDB is ideal for high-scale applications with simple access patterns
7. Choose DynamoDB for scalability and speed; RDS for complex queries and transactions

---

*Previous: [02 - Relational Databases](../02-relational-databases/readme.md) | Next: [04 - In-Memory Databases](../04-in-memory-databases/readme.md)*

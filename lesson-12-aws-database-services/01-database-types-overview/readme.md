# 🗄️ Database Types Overview

## File Structure

```
lesson-12-aws-database-services/
└── 01-database-types-overview/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Understanding database types is fundamental to choosing the right AWS database service for your application. AWS offers purpose-built databases for different workloads, and the Cloud Practitioner exam expects you to understand when to use relational vs NoSQL databases, and OLTP vs OLAP systems.

## Database Categories

```
+------------------------------------------------------------------+
|                     AWS DATABASE LANDSCAPE                        |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------------+    +------------------------+        |
|   |     RELATIONAL         |    |       NoSQL            |        |
|   |------------------------+    |------------------------+        |
|   |  - Structured data     |    |  - Flexible schema     |        |
|   |  - ACID transactions   |    |  - High scalability    |        |
|   |  - SQL queries         |    |  - Low latency         |        |
|   |                        |    |                        |        |
|   |  AWS: RDS, Aurora      |    |  AWS: DynamoDB         |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
|   +------------------------+    +------------------------+        |
|   |     IN-MEMORY          |    |     PURPOSE-BUILT      |        |
|   |------------------------+    |------------------------+        |
|   |  - Microsecond latency |    |  - Graph: Neptune      |        |
|   |  - Caching layer       |    |  - Time-series: TS     |        |
|   |                        |    |  - Ledger: QLDB        |        |
|   |  AWS: ElastiCache      |    |  - Document: DocDB     |        |
|   +------------------------+    +------------------------+        |
|                                                                   |
+------------------------------------------------------------------+
```

## Relational vs NoSQL Databases

| Aspect | Relational | NoSQL |
|--------|------------|-------|
| Schema | Fixed, predefined | Flexible, dynamic |
| Data Model | Tables with rows and columns | Key-value, document, graph, wide-column |
| Query Language | SQL | Varies by database type |
| Scalability | Vertical (scale up) | Horizontal (scale out) |
| Transactions | Strong ACID compliance | Eventual consistency (usually) |
| Use Cases | Financial systems, ERP, CRM | Web apps, gaming, IoT, real-time |
| AWS Services | RDS, Aurora | DynamoDB, DocumentDB |

## OLTP vs OLAP

Understanding the difference between transactional and analytical workloads is critical for database selection.

### OLTP (Online Transaction Processing)

| Characteristic | Description |
|----------------|-------------|
| Purpose | Handle day-to-day transactions |
| Query Type | Simple, short queries |
| Data Volume | Many small transactions |
| Operations | INSERT, UPDATE, DELETE |
| Example | E-commerce orders, banking transactions |
| AWS Services | RDS, Aurora, DynamoDB |

### OLAP (Online Analytical Processing)

| Characteristic | Description |
|----------------|-------------|
| Purpose | Analyze historical data |
| Query Type | Complex, aggregation queries |
| Data Volume | Large datasets, batch processing |
| Operations | SELECT with GROUP BY, JOINs |
| Example | Business reporting, data mining |
| AWS Services | Redshift, Athena |

### OLTP vs OLAP Comparison

```
+------------------------------------------------------------------+
|                    OLTP vs OLAP COMPARISON                        |
+------------------------------------------------------------------+
|                                                                   |
|   OLTP (Transactional)              OLAP (Analytical)             |
|   +----------------------+          +----------------------+      |
|   |  "Write" Focused     |          |  "Read" Focused      |      |
|   |                      |          |                      |      |
|   |  INSERT INTO orders  |          |  SELECT SUM(sales)   |      |
|   |  VALUES (...)        |          |  FROM orders         |      |
|   |                      |          |  GROUP BY region     |      |
|   |  Fast, small queries |          |  Complex queries     |      |
|   |  Real-time data      |          |  Historical data     |      |
|   +----------------------+          +----------------------+      |
|                                                                   |
|   AWS: RDS, Aurora, DynamoDB        AWS: Redshift, Athena         |
|                                                                   |
+------------------------------------------------------------------+
```

## When to Use Each Database Type

### Use Relational Databases (RDS/Aurora) When:

- Data has clear relationships between tables
- You need ACID transactions (banking, inventory)
- Complex queries with multiple JOINs required
- Data integrity is critical
- Working with structured, consistent data

### Use NoSQL Databases (DynamoDB) When:

- Schema may change frequently
- Need massive horizontal scalability
- Working with semi-structured data (JSON)
- Require single-digit millisecond latency
- Building real-time applications

### Use In-Memory Databases (ElastiCache) When:

- Need sub-millisecond response times
- Caching frequently accessed data
- Managing session data
- Gaming leaderboards

### Use Purpose-Built Databases When:

| Database | Use When |
|----------|----------|
| Neptune | Working with highly connected data (social networks, fraud detection) |
| DocumentDB | Need MongoDB compatibility |
| Timestream | Storing time-series data (IoT, DevOps metrics) |
| QLDB | Need immutable, cryptographically verifiable ledger |
| Keyspaces | Need Apache Cassandra compatibility |

## Database Selection Flowchart

```
+------------------------------------------------------------------+
|                 CHOOSING THE RIGHT DATABASE                       |
+------------------------------------------------------------------+
|                                                                   |
|   Do you need relational features (SQL, JOINs, transactions)?     |
|                    |                                              |
|         +----YES---+----NO----+                                   |
|         |                     |                                   |
|         v                     v                                   |
|   +----------+          Need high scalability                     |
|   | RDS or   |          & flexible schema?                        |
|   | Aurora   |                    |                               |
|   +----------+         +----YES---+----NO----+                    |
|                        |                     |                    |
|                        v                     v                    |
|                  +----------+          Purpose-built?             |
|                  | DynamoDB |                |                    |
|                  +----------+          (Graph, Ledger,            |
|                                         Time-series)              |
|                                               |                   |
|                                               v                   |
|                                     Neptune, QLDB, Timestream     |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Database Services Summary

| Service | Type | Best For |
|---------|------|----------|
| Amazon RDS | Relational | Traditional apps, ERP, CRM |
| Amazon Aurora | Relational | High-performance MySQL/PostgreSQL |
| Amazon DynamoDB | Key-value/Document | Serverless, high-scale apps |
| Amazon ElastiCache | In-memory | Caching, session management |
| Amazon Redshift | Data Warehouse | Analytics, business intelligence |
| Amazon Neptune | Graph | Social networks, recommendations |
| Amazon DocumentDB | Document | MongoDB workloads |
| Amazon QLDB | Ledger | Immutable audit trails |
| Amazon Timestream | Time-series | IoT, DevOps monitoring |
| Amazon Keyspaces | Wide-column | Cassandra workloads |

## 🎯 Exam Tips

- **Relational databases** = structured data, SQL, ACID transactions, JOINs
- **NoSQL databases** = flexible schema, horizontal scaling, high throughput
- **OLTP** = transactional workloads (RDS, Aurora, DynamoDB)
- **OLAP** = analytical workloads (Redshift, Athena)
- **DynamoDB** = serverless, single-digit millisecond latency, auto-scaling
- **Aurora** = MySQL/PostgreSQL compatible, 5x faster than MySQL
- Know that AWS offers **purpose-built databases** for specific use cases
- **ElastiCache** = caching layer to reduce database load

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Relational Database | Database that stores data in tables with rows and columns |
| NoSQL | Non-relational databases designed for specific data models |
| OLTP | Online Transaction Processing - operational databases |
| OLAP | Online Analytical Processing - analytical databases |
| ACID | Atomicity, Consistency, Isolation, Durability |
| Schema | Structure defining how data is organized |
| Horizontal Scaling | Adding more machines to distribute load |
| Vertical Scaling | Adding more power to existing machines |

## 💡 Key Takeaways

1. AWS offers purpose-built databases optimized for different workloads
2. Relational databases (RDS, Aurora) are best for structured data with complex relationships
3. NoSQL databases (DynamoDB) excel at scale and flexible schemas
4. OLTP handles real-time transactions; OLAP handles analytical queries
5. In-memory databases (ElastiCache) provide microsecond latency for caching
6. Choose the right database based on data model, scale requirements, and query patterns
7. Purpose-built databases like Neptune (graph) and QLDB (ledger) serve specialized needs

---

*Next: [02 - Relational Databases](../02-relational-databases/readme.md)*

# 🗄️ Other AWS Database Services

## File Structure

```
lesson-12-aws-database-services/
└── 05-other-database-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS offers purpose-built databases for specific workloads beyond relational and key-value databases. Understanding these specialized services and their use cases is important for the Cloud Practitioner exam.

## AWS Purpose-Built Databases

```
+------------------------------------------------------------------+
|                 AWS PURPOSE-BUILT DATABASES                       |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |    NEPTUNE       |  |   DOCUMENTDB     |  |   KEYSPACES      | |
|   |    (Graph)       |  |   (Document)     |  |   (Wide-Column)  | |
|   |  Social networks |  |  MongoDB compat. |  | Cassandra compat.| |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
|   +------------------+  +------------------+  +------------------+ |
|   |     QLDB         |  |   TIMESTREAM     |  |    REDSHIFT      | |
|   |    (Ledger)      |  |  (Time-series)   |  | (Data Warehouse) | |
|   | Immutable records|  |   IoT, metrics   |  |    Analytics     | |
|   +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Neptune (Graph Database)

Amazon Neptune is a fully managed graph database service for highly connected datasets.

### Neptune Overview

```
+------------------------------------------------------------------+
|                      AMAZON NEPTUNE                               |
+------------------------------------------------------------------+
|                                                                   |
|   GRAPH DATA MODEL                                                |
|                                                                   |
|         [Alice]                                                   |
|          /    \                                                   |
|    FRIENDS    WORKS_AT                                            |
|        /        \                                                 |
|    [Bob]      [Acme Corp]                                         |
|       \          /                                                |
|     WORKS_AT   LOCATED_IN                                         |
|         \      /                                                  |
|         [Seattle]                                                 |
|                                                                   |
|   Nodes = Entities (People, Places, Things)                       |
|   Edges = Relationships (connects nodes)                          |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Type | Fully managed graph database |
| Models | Property Graph (Gremlin), RDF (SPARQL) |
| Availability | Multi-AZ with read replicas |
| Storage | Up to 128TB, auto-scaling |
| Backup | Continuous backup to S3 |

### Neptune Use Cases

| Use Case | Description |
|----------|-------------|
| Social Networks | Model friend relationships, interactions |
| Fraud Detection | Identify suspicious patterns and connections |
| Recommendation Engines | "People who bought X also bought Y" |
| Knowledge Graphs | Connect and query diverse data sources |
| Network Management | Model IT infrastructure relationships |
| Identity Resolution | Link identities across systems |

## Amazon DocumentDB (Document Database)

Amazon DocumentDB is a fully managed document database service compatible with MongoDB.

```
+------------------------------------------------------------------+
|                    AMAZON DOCUMENTDB                              |
+------------------------------------------------------------------+
|                                                                   |
|   DOCUMENT DATA MODEL (JSON-like)                                 |
|                                                                   |
|   {                                                               |
|     "_id": "user123",                                             |
|     "name": "John Doe",                                           |
|     "email": "john@example.com",                                  |
|     "orders": [                                                   |
|       {                                                           |
|         "id": "order1",                                           |
|         "items": ["item1", "item2"],                              |
|         "total": 99.99                                            |
|       }                                                           |
|     ],                                                            |
|     "preferences": {                                              |
|       "newsletter": true,                                         |
|       "theme": "dark"                                             |
|     }                                                             |
|   }                                                               |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Compatibility | MongoDB 3.6, 4.0, 5.0 compatible |
| Type | Fully managed document database |
| Storage | Auto-scales up to 128TB |
| Availability | 6 copies across 3 AZs |
| Replicas | Up to 15 read replicas |

### DocumentDB Use Cases

| Use Case | Description |
|----------|-------------|
| Content Management | Store articles, blog posts with flexible schema |
| User Profiles | Store user data with varying attributes |
| Catalogs | Product catalogs with different attributes |
| Mobile Applications | Backend for apps with JSON data |

## Amazon Keyspaces (Wide-Column Database)

Amazon Keyspaces is a managed Apache Cassandra-compatible database service.

```
+------------------------------------------------------------------+
|                    AMAZON KEYSPACES                               |
+------------------------------------------------------------------+
|                                                                   |
|   WIDE-COLUMN DATA MODEL                                          |
|                                                                   |
|   +----------------------------------------------------------+   |
|   |  Partition Key  |  Clustering Column  |  Columns...       |   |
|   |-----------------|---------------------|-------------------|   |
|   |  user_id:123    |  timestamp:2024-01  |  event:click      |   |
|   |                 |  timestamp:2024-02  |  event:purchase   |   |
|   |                 |  timestamp:2024-03  |  event:view       |   |
|   |-----------------|---------------------|-------------------|   |
|   |  user_id:456    |  timestamp:2024-01  |  event:login      |   |
|   +----------------------------------------------------------+   |
|                                                                   |
|   - Cassandra Query Language (CQL) compatible                     |
|   - Serverless, scales automatically                              |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Compatibility | Apache Cassandra compatible (CQL) |
| Type | Serverless, fully managed |
| Scaling | Automatic, handles any scale |
| Availability | Multi-Region replication available |
| Pricing | On-demand or provisioned capacity |

### Keyspaces Use Cases

| Use Case | Description |
|----------|-------------|
| IoT Applications | Store high-volume sensor data |
| Time-series Data | Event logs, activity tracking |
| Migration | Migrate Cassandra workloads to AWS |

## Amazon QLDB (Ledger Database)

Amazon Quantum Ledger Database (QLDB) provides an immutable, cryptographically verifiable transaction log.

```
+------------------------------------------------------------------+
|                        AMAZON QLDB                                |
+------------------------------------------------------------------+
|                                                                   |
|   IMMUTABLE LEDGER                                                |
|                                                                   |
|   Block 1          Block 2          Block 3          Block 4      |
|   +--------+       +--------+       +--------+       +--------+   |
|   | Trans  |------>| Trans  |------>| Trans  |------>| Trans  |   |
|   | Data   |       | Data   |       | Data   |       | Data   |   |
|   | Hash   |       | Hash   |       | Hash   |       | Hash   |   |
|   +--------+       +--------+       +--------+       +--------+   |
|                                                                   |
|   - Every change is tracked                                       |
|   - Cryptographically verifiable                                  |
|   - Cannot delete or modify history                               |
|   - Complete audit trail                                          |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Type | Fully managed ledger database |
| Immutability | Append-only, cannot delete history |
| Verification | SHA-256 cryptographic hashing |
| Query | PartiQL (SQL-compatible) |
| ACID | Full ACID transactions |

### QLDB Use Cases

| Use Case | Description |
|----------|-------------|
| Financial Transactions | Audit trail for all transactions |
| Supply Chain | Track product history and provenance |
| Healthcare | Immutable patient records |
| HR Systems | Track employee credential history |
| Insurance Claims | Verifiable claim history |

### QLDB vs Blockchain

| Feature | QLDB | Blockchain |
|---------|------|------------|
| Centralized | Yes (AWS owned) | No (distributed) |
| Trust Model | Trust AWS | Trust network |
| Performance | High throughput | Lower throughput |
| Use Case | Single-owner ledger | Multi-party trust |

## Amazon Timestream (Time-Series Database)

Amazon Timestream is a fast, scalable, fully managed time-series database.

```
+------------------------------------------------------------------+
|                     AMAZON TIMESTREAM                             |
+------------------------------------------------------------------+
|                                                                   |
|   TIME-SERIES DATA                                                |
|                                                                   |
|   Temperature readings over time:                                 |
|                                                                   |
|   Temp ^                                                          |
|    25  |          *     *                                         |
|    20  |    *  *     *     *  *                                   |
|    15  | *                       *  *                             |
|    10  |                              *                           |
|        +---------------------------------> Time                   |
|         9am  10am  11am  12pm  1pm  2pm  3pm                      |
|                                                                   |
|   - Optimized for time-ordered data                               |
|   - Automatic data lifecycle management                           |
|   - Built-in analytics functions                                  |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Type | Serverless time-series database |
| Storage Tiers | Memory (recent), Magnetic (historical) |
| Performance | 1000x faster than relational for time-series |
| Cost | 1/10th the cost of relational databases |
| Built-in Functions | Time-series analytics functions |

### Timestream Use Cases

| Use Case | Description |
|----------|-------------|
| IoT Sensors | Collect and analyze sensor data |
| DevOps Metrics | Monitor application performance |
| Industrial Telemetry | Machine and equipment monitoring |
| Clickstream | User activity analytics |

## Amazon Redshift (Data Warehouse)

Amazon Redshift is a fast, fully managed, petabyte-scale data warehouse.

```
+------------------------------------------------------------------+
|                      AMAZON REDSHIFT                              |
+------------------------------------------------------------------+
|                                                                   |
|   +------------------+     +------------------+                   |
|   |  Data Sources    |     |   Redshift       |     +----------+ |
|   |  - RDS           |---->|   Cluster        |---->| BI Tools | |
|   |  - S3            |     |                  |     | Tableau  | |
|   |  - DynamoDB      |     |  Leader Node     |     | QuickSight|
|   |  - Kinesis       |     |       |          |     +----------+ |
|   +------------------+     |  Compute Nodes   |                   |
|                            |  [ ][ ][ ][ ]    |                   |
|                            +------------------+                   |
|                                                                   |
|   - Columnar storage for fast analytics                           |
|   - Massively parallel processing (MPP)                           |
|   - Petabyte-scale data warehouse                                 |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Type | Columnar data warehouse |
| Scale | Petabyte-scale |
| Performance | Massively parallel processing |
| Storage | Columnar for analytics |
| Redshift Spectrum | Query S3 data directly |
| Redshift Serverless | No cluster management |

### Redshift Use Cases

| Use Case | Description |
|----------|-------------|
| Business Intelligence | Complex analytics queries |
| Data Consolidation | Centralize data from multiple sources |
| Historical Analysis | Analyze years of data |
| Reporting | Generate business reports |

## Database Services Comparison

| Service | Type | Use Case | Key Feature |
|---------|------|----------|-------------|
| Neptune | Graph | Social networks, fraud | Relationship queries |
| DocumentDB | Document | Content management | MongoDB compatible |
| Keyspaces | Wide-column | IoT, time-series | Cassandra compatible |
| QLDB | Ledger | Audit trails | Immutable, verifiable |
| Timestream | Time-series | IoT metrics | Time-optimized |
| Redshift | Warehouse | Analytics | Petabyte-scale OLAP |

## 🎯 Exam Tips

- **Neptune** = graph database for highly connected data (social networks, fraud)
- **DocumentDB** = MongoDB-compatible document database
- **Keyspaces** = Cassandra-compatible wide-column database
- **QLDB** = immutable ledger with cryptographic verification (audit trails)
- **Timestream** = purpose-built for time-series data (IoT, metrics)
- **Redshift** = data warehouse for analytics (OLAP, not OLTP)
- QLDB is **centralized** (unlike blockchain which is distributed)
- Timestream automatically moves data between storage tiers
- Redshift uses **columnar storage** for fast analytics

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Graph Database | Database optimized for relationship queries |
| Document Database | Database storing JSON-like documents |
| Wide-Column | Database with rows and dynamic columns |
| Ledger Database | Immutable, append-only transaction log |
| Time-Series | Data indexed by timestamp |
| Data Warehouse | Database optimized for analytical queries |
| Columnar Storage | Data stored by columns for analytics |
| MPP | Massively Parallel Processing |

## 💡 Key Takeaways

1. AWS offers purpose-built databases for specific workloads
2. Neptune excels at querying highly connected data (graphs)
3. DocumentDB provides MongoDB compatibility for document workloads
4. QLDB provides immutable, cryptographically verifiable ledger capabilities
5. Timestream is optimized for time-series data with automatic tiering
6. Redshift is a petabyte-scale data warehouse for analytics
7. Choose the right purpose-built database based on your data model and access patterns

---

*Previous: [04 - In-Memory Databases](../04-in-memory-databases/readme.md) | Next: [06 - Database Migration](../06-database-migration/readme.md)*

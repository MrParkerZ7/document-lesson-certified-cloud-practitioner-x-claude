# 📊 AWS Analytics Services

## File Structure

```
lesson-15-aws-ai-ml-and-analytics-services/
└── 02-analytics-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides a comprehensive suite of analytics services that enable organizations to collect, process, analyze, and visualize data at any scale. From serverless query engines to petabyte-scale data warehouses, these services help transform raw data into actionable insights without managing infrastructure.

## Analytics Services Overview

```
+------------------------------------------------------------------+
|                   AWS ANALYTICS PIPELINE                          |
+------------------------------------------------------------------+
|                                                                   |
|   COLLECT           STORE            PROCESS          ANALYZE     |
|   ┌─────────┐      ┌─────────┐      ┌─────────┐      ┌─────────┐  |
|   │ Kinesis │ ──▶  │   S3    │ ──▶  │  Glue   │ ──▶  │ Athena  │  |
|   │ Streams │      │  Data   │      │   EMR   │      │Redshift │  |
|   └─────────┘      │  Lake   │      └─────────┘      │QuickSight│ |
|                    └─────────┘                       └─────────┘  |
|                                                                   |
|   Real-time      Centralized       Transform        Query &       |
|   Ingestion      Storage           & Process        Visualize     |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Athena

Amazon Athena is a serverless, interactive query service that analyzes data in Amazon S3 using standard SQL.

```
+------------------------------------------------------------------+
|                       AMAZON ATHENA                               |
+------------------------------------------------------------------+
|                                                                   |
|   ┌─────────────────┐        ┌─────────────────┐                  |
|   │     S3 DATA     │        │   SQL QUERY     │                  |
|   │  ┌───────────┐  │        │                 │                  |
|   │  │ logs/     │  │   ◀──  │ SELECT * FROM   │                  |
|   │  │ data.csv  │  │        │ logs WHERE...   │                  |
|   │  │ data.json │  │        │                 │                  |
|   │  │ data.parquet│ │        │                 │                  |
|   │  └───────────┘  │        └─────────────────┘                  |
|   └─────────────────┘                                             |
|                                                                   |
|   • Serverless - no infrastructure to manage                      |
|   • Pay per query - $5 per TB scanned                             |
|   • Supports CSV, JSON, Parquet, ORC, Avro                        |
|   • Integrates with AWS Glue Data Catalog                         |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Serverless | No infrastructure to provision or manage |
| Standard SQL | Use familiar ANSI SQL queries |
| Data Formats | CSV, JSON, ORC, Parquet, Avro |
| Pricing | Pay only for data scanned ($5/TB) |
| Integration | Glue Data Catalog, QuickSight, S3 |
| Performance | Use columnar formats (Parquet) for faster queries |

| Use Case | Description |
|----------|-------------|
| Log Analysis | Query CloudTrail, ALB, VPC flow logs |
| Ad-hoc Queries | One-time data exploration |
| Data Lake Queries | Query data lake in S3 |
| Cost Optimization | Analyze AWS cost reports |

## Amazon Redshift

Amazon Redshift is a fully managed, petabyte-scale cloud data warehouse for analytics.

```
+------------------------------------------------------------------+
|                      AMAZON REDSHIFT                              |
+------------------------------------------------------------------+
|                                                                   |
|   DATA SOURCES                      REDSHIFT CLUSTER              |
|   ┌──────────┐                     ┌────────────────────────┐     |
|   │    S3    │──┐                  │  ┌────┐ ┌────┐ ┌────┐  │     |
|   └──────────┘  │                  │  │Node│ │Node│ │Node│  │     |
|   ┌──────────┐  │                  │  └────┘ └────┘ └────┘  │     |
|   │   RDS    │──┼──▶ REDSHIFT ──▶  │         Leader         │     |
|   └──────────┘  │                  │  ┌────────────────────┐│     |
|   ┌──────────┐  │                  │  │   Compute Nodes    ││     |
|   │ Kinesis  │──┘                  │  │   (Parallel SQL)   ││     |
|   └──────────┘                     │  └────────────────────┘│     |
|                                    └────────────────────────┘     |
|                                                                   |
|   • Columnar storage for fast analytics                           |
|   • Massively Parallel Processing (MPP)                           |
|   • Scales to petabytes of data                                   |
|   • Redshift Spectrum - query S3 directly                         |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Columnar Storage | Optimized for analytics queries |
| MPP | Massively Parallel Processing architecture |
| Scale | Petabytes of structured data |
| Redshift Spectrum | Query S3 data without loading |
| Serverless Option | Auto-scaling without clusters |
| Concurrency Scaling | Handle traffic spikes |

| Component | Description |
|-----------|-------------|
| Leader Node | Receives queries, develops execution plans |
| Compute Nodes | Execute queries in parallel |
| Node Slices | Portions of memory and disk on each node |

### Redshift vs Athena

| Criteria | Redshift | Athena |
|----------|----------|--------|
| Best For | Complex analytics, BI workloads | Ad-hoc queries, infrequent queries |
| Data Location | Loaded into Redshift | Stays in S3 |
| Infrastructure | Managed clusters (or serverless) | Fully serverless |
| Performance | Very fast for large datasets | Fast for small-medium queries |
| Pricing | Per-node (or per-query for serverless) | Per query ($5/TB scanned) |
| Use Case | Data warehouse | Data lake queries |

## Amazon EMR (Elastic MapReduce)

Amazon EMR is a managed big data platform for processing vast amounts of data using open-source tools.

```
+------------------------------------------------------------------+
|                        AMAZON EMR                                 |
+------------------------------------------------------------------+
|                                                                   |
|   BIG DATA FRAMEWORKS                                             |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │  Apache Spark  │  Apache Hadoop  │  Presto  │  Hive  │ HBase │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                              │                                    |
|                              ▼                                    |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                      EMR CLUSTER                             │ |
|   │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐     │ |
|   │  │  Master  │  │   Core   │  │   Core   │  │   Task   │     │ |
|   │  │   Node   │  │   Node   │  │   Node   │  │   Node   │     │ |
|   │  └──────────┘  └──────────┘  └──────────┘  └──────────┘     │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
|   Use Cases: ETL, log analysis, ML training, clickstream analysis |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Frameworks | Spark, Hadoop, Presto, Hive, HBase, Flink |
| Cluster Types | On-demand, Spot, Reserved |
| Storage | HDFS, EMRFS (S3), EBS |
| Auto-scaling | Scale based on workload |
| EMR Serverless | Run without managing clusters |

| Node Type | Description |
|-----------|-------------|
| Master | Manages cluster, tracks job status |
| Core | Run tasks and store HDFS data |
| Task | Run tasks only, no HDFS storage |

| Use Case | Framework |
|----------|-----------|
| ETL Processing | Apache Spark |
| Machine Learning | Apache Spark MLlib |
| Interactive Queries | Presto, Hive |
| Real-time Streaming | Apache Flink |
| Log Analysis | Hadoop MapReduce |

## Amazon Kinesis

Amazon Kinesis collects, processes, and analyzes real-time streaming data.

```
+------------------------------------------------------------------+
|                      AMAZON KINESIS                               |
+------------------------------------------------------------------+
|                                                                   |
|   DATA PRODUCERS          KINESIS              CONSUMERS          |
|   ┌──────────┐                                ┌──────────┐        |
|   │ IoT      │──┐                         ┌──▶│ Lambda   │        |
|   │ Devices  │  │    ┌──────────────┐     │   └──────────┘        |
|   └──────────┘  │    │              │     │   ┌──────────┐        |
|   ┌──────────┐  │───▶│   KINESIS    │─────┼──▶│ EMR      │        |
|   │ Apps     │  │    │   STREAMS    │     │   └──────────┘        |
|   └──────────┘  │    │              │     │   ┌──────────┐        |
|   ┌──────────┐  │    └──────────────┘     └──▶│ Redshift │        |
|   │ Logs     │──┘                             └──────────┘        |
|   └──────────┘                                                    |
|                                                                   |
+------------------------------------------------------------------+
```

### Kinesis Services

| Service | Description | Use Case |
|---------|-------------|----------|
| Kinesis Data Streams | Collect and process real-time streams | Custom processing applications |
| Kinesis Data Firehose | Load streams to data stores | Deliver to S3, Redshift, Splunk |
| Kinesis Data Analytics | Analyze streams with SQL | Real-time dashboards |
| Kinesis Video Streams | Capture and process video streams | Security, ML on video |

### Kinesis Data Streams vs Firehose

| Feature | Data Streams | Data Firehose |
|---------|--------------|---------------|
| Management | Manual (provisioned) | Fully managed |
| Processing | Custom consumers required | Built-in transformation |
| Latency | Real-time (< 1 second) | Near real-time (60+ seconds) |
| Destinations | Custom applications | S3, Redshift, Splunk, HTTP |
| Scaling | Manual shard management | Automatic |
| Data Retention | 24 hours to 365 days | No retention (delivery only) |

```
+------------------------------------------------------------------+
|               KINESIS DATA STREAMS vs FIREHOSE                    |
+------------------------------------------------------------------+
|                                                                   |
|   DATA STREAMS (Custom Processing)                                |
|   ┌───────┐    ┌──────────────┐    ┌───────────┐                  |
|   │Source │───▶│   Shards     │───▶│ Lambda/   │                  |
|   └───────┘    │ (You manage) │    │ EC2/EMR   │                  |
|                └──────────────┘    └───────────┘                  |
|                                                                   |
|   FIREHOSE (Managed Delivery)                                     |
|   ┌───────┐    ┌──────────────┐    ┌───────────┐                  |
|   │Source │───▶│  Firehose    │───▶│ S3/       │                  |
|   └───────┘    │ (Fully mgd)  │    │ Redshift  │                  |
|                └──────────────┘    └───────────┘                  |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon QuickSight

Amazon QuickSight is a serverless, ML-powered business intelligence (BI) service for creating visualizations and dashboards.

```
+------------------------------------------------------------------+
|                    AMAZON QUICKSIGHT                              |
+------------------------------------------------------------------+
|                                                                   |
|   DATA SOURCES                    QUICKSIGHT                      |
|   ┌──────────┐                   ┌──────────────────────────────┐ |
|   │ Redshift │──┐                │  ┌────────────────────────┐  │ |
|   └──────────┘  │                │  │    DASHBOARD           │  │ |
|   ┌──────────┐  │                │  │  ┌─────┐  ┌──────────┐ │  │ |
|   │  Athena  │──┼───────────────▶│  │  │ 📊  │  │ 📈       │ │  │ |
|   └──────────┘  │                │  │  │Chart│  │ Graph    │ │  │ |
|   ┌──────────┐  │                │  │  └─────┘  └──────────┘ │  │ |
|   │    S3    │──┤                │  │  ┌─────┐  ┌──────────┐ │  │ |
|   └──────────┘  │                │  │  │ 🥧  │  │ 📋       │ │  │ |
|   ┌──────────┐  │                │  │  │ Pie │  │ Table    │ │  │ |
|   │   RDS    │──┘                │  │  └─────┘  └──────────┘ │  │ |
|   └──────────┘                   │  └────────────────────────┘  │ |
|                                  └──────────────────────────────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Serverless | No servers to manage |
| SPICE Engine | Super-fast, Parallel, In-memory Calculation Engine |
| ML Insights | Automatic anomaly detection, forecasting |
| Pay-per-Session | Per-session pricing for viewers |
| Embedded Analytics | Embed dashboards in applications |
| Mobile Access | Native mobile apps |

| Data Source | Description |
|-------------|-------------|
| AWS Services | Redshift, Athena, S3, RDS, Aurora |
| Databases | PostgreSQL, MySQL, SQL Server |
| SaaS | Salesforce, ServiceNow, Jira |
| Files | CSV, Excel, JSON |

## AWS Glue

AWS Glue is a fully managed serverless ETL (Extract, Transform, Load) service.

```
+------------------------------------------------------------------+
|                        AWS GLUE                                   |
+------------------------------------------------------------------+
|                                                                   |
|   SOURCE DATA              GLUE                  TARGET           |
|   ┌──────────┐         ┌──────────┐          ┌──────────┐         |
|   │    S3    │──┐      │          │      ┌──▶│    S3    │         |
|   └──────────┘  │      │  EXTRACT │      │   └──────────┘         |
|   ┌──────────┐  │      │    ▼     │      │   ┌──────────┐         |
|   │   RDS    │──┼─────▶│TRANSFORM │──────┼──▶│ Redshift │         |
|   └──────────┘  │      │    ▼     │      │   └──────────┘         |
|   ┌──────────┐  │      │   LOAD   │      │   ┌──────────┐         |
|   │ On-prem  │──┘      │          │      └──▶│  Athena  │         |
|   └──────────┘         └──────────┘          └──────────┘         |
|                                                                   |
|   GLUE COMPONENTS:                                                |
|   • Glue Data Catalog - Metadata repository                       |
|   • Glue Crawlers - Discover and catalog data schemas             |
|   • Glue Jobs - ETL scripts (Python/Scala)                        |
|   • Glue Studio - Visual ETL designer                             |
|                                                                   |
+------------------------------------------------------------------+
```

| Component | Description |
|-----------|-------------|
| Data Catalog | Central metadata repository |
| Crawlers | Automatically discover schemas |
| ETL Jobs | Serverless Spark-based ETL |
| Glue Studio | Visual ETL job designer |
| DataBrew | Visual data preparation |
| Streaming ETL | Process streaming data |

| Feature | Description |
|---------|-------------|
| Serverless | No infrastructure to manage |
| Auto-generated Code | Creates ETL code automatically |
| Job Bookmarks | Track processed data |
| Scheduling | Built-in job scheduling |
| Integration | Athena, Redshift, EMR, S3 |

## AWS Data Pipeline

AWS Data Pipeline is a web service for orchestrating and automating data movement and transformation.

```
+------------------------------------------------------------------+
|                    AWS DATA PIPELINE                              |
+------------------------------------------------------------------+
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                     PIPELINE DEFINITION                      │ |
|   │  ┌──────────┐    ┌──────────┐    ┌──────────┐               │ |
|   │  │  Source  │───▶│ Activity │───▶│  Target  │               │ |
|   │  │   (S3)   │    │  (EMR)   │    │(Redshift)│               │ |
|   │  └──────────┘    └──────────┘    └──────────┘               │ |
|   │                       │                                      │ |
|   │                  ┌────┴────┐                                 │ |
|   │                  │Schedule │                                 │ |
|   │                  │ (Daily) │                                 │ |
|   │                  └─────────┘                                 │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
|   Features: Scheduling, retry logic, notifications, dependencies  |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Scheduling | Run pipelines on schedule |
| Dependencies | Define activity dependencies |
| Retry Logic | Automatic retry on failures |
| On-premises | Move data from on-premises |
| Notifications | SNS alerts on completion/failure |

> **Note**: AWS Data Pipeline is older; consider AWS Glue or Step Functions for new projects.

## AWS Lake Formation

AWS Lake Formation simplifies building, securing, and managing data lakes.

```
+------------------------------------------------------------------+
|                   AWS LAKE FORMATION                              |
+------------------------------------------------------------------+
|                                                                   |
|   DATA SOURCES              LAKE FORMATION          DATA LAKE     |
|   ┌──────────┐                                     ┌──────────┐   |
|   │ Database │──┐                                  │          │   |
|   └──────────┘  │     ┌────────────────────┐      │    S3    │   |
|   ┌──────────┐  │     │  • Ingest Data     │      │   Data   │   |
|   │    S3    │──┼────▶│  • Catalog         │─────▶│   Lake   │   |
|   └──────────┘  │     │  • Clean/Transform │      │          │   |
|   ┌──────────┐  │     │  • Secure Access   │      │          │   |
|   │ On-prem  │──┘     └────────────────────┘      └──────────┘   |
|   └──────────┘                │                        │         |
|                               ▼                        ▼         |
|                    ┌───────────────────┐    ┌───────────────────┐|
|                    │ Fine-grained      │    │ Athena, Redshift  │|
|                    │ Access Control    │    │ EMR, QuickSight   │|
|                    └───────────────────┘    └───────────────────┘|
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Description |
|---------|-------------|
| Data Ingestion | Import from databases, S3, on-premises |
| Cataloging | Automatic schema discovery |
| Transformation | Built-in ML transforms |
| Security | Fine-grained access control |
| Governance | Track data lineage |
| Blueprints | Pre-built templates for common sources |

| Capability | Description |
|------------|-------------|
| Column-level Security | Restrict access to specific columns |
| Row-level Security | Filter rows based on user/group |
| Governed Tables | ACID transactions on S3 data |
| Cross-account Sharing | Share data across AWS accounts |

## Analytics Services Comparison

| Service | Best For | Key Feature |
|---------|----------|-------------|
| Athena | Ad-hoc S3 queries | Serverless SQL |
| Redshift | Data warehousing | Petabyte-scale analytics |
| EMR | Big data processing | Open-source frameworks |
| Kinesis | Real-time streaming | Stream processing |
| QuickSight | BI dashboards | Serverless visualization |
| Glue | ETL processing | Serverless Spark ETL |
| Data Pipeline | Data orchestration | Workflow automation |
| Lake Formation | Data lake management | Security and governance |

## When to Use Each Service

```
+------------------------------------------------------------------+
|              ANALYTICS SERVICE DECISION TREE                      |
+------------------------------------------------------------------+
|                                                                   |
|   Need to query data in S3?                                       |
|   ├── Yes, infrequent queries ──────────▶ ATHENA                  |
|   └── Yes, frequent complex queries ────▶ REDSHIFT SPECTRUM       |
|                                                                   |
|   Need a data warehouse?                                          |
|   └── Yes ──────────────────────────────▶ REDSHIFT                |
|                                                                   |
|   Need to process big data with Spark/Hadoop?                     |
|   └── Yes ──────────────────────────────▶ EMR                     |
|                                                                   |
|   Need real-time data streaming?                                  |
|   ├── Custom processing needed ─────────▶ KINESIS DATA STREAMS    |
|   └── Just deliver to S3/Redshift ──────▶ KINESIS FIREHOSE        |
|                                                                   |
|   Need to create dashboards?                                      |
|   └── Yes ──────────────────────────────▶ QUICKSIGHT              |
|                                                                   |
|   Need serverless ETL?                                            |
|   └── Yes ──────────────────────────────▶ GLUE                    |
|                                                                   |
|   Need to build a data lake?                                      |
|   └── Yes ──────────────────────────────▶ LAKE FORMATION          |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **Athena** = serverless SQL queries on S3 data, pay per query ($5/TB scanned)
- **Redshift** = petabyte-scale data warehouse, columnar storage, MPP architecture
- **Redshift Spectrum** = query S3 data directly from Redshift without loading
- **EMR** = managed Hadoop/Spark clusters for big data processing
- **Kinesis Data Streams** = real-time streaming with custom processing (you manage shards)
- **Kinesis Data Firehose** = fully managed delivery to S3, Redshift, Splunk
- **Kinesis Data Analytics** = real-time SQL analytics on streams
- **QuickSight** = serverless BI service with SPICE in-memory engine
- **Glue** = serverless ETL with automatic schema discovery (Crawlers)
- **Glue Data Catalog** = central metadata repository used by Athena and Redshift
- **Lake Formation** = build secure data lakes with fine-grained access control
- Use **Athena** for ad-hoc queries; use **Redshift** for complex, frequent analytics
- Use **columnar formats** (Parquet, ORC) with Athena to reduce costs and improve speed

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| ETL | Extract, Transform, Load - data integration process |
| Data Warehouse | Central repository for structured analytics data |
| Data Lake | Storage repository for raw structured and unstructured data |
| Streaming Data | Continuous flow of data generated in real-time |
| OLAP | Online Analytical Processing - complex queries for analysis |
| Columnar Storage | Data stored by columns for fast analytics |
| MPP | Massively Parallel Processing - distributed query execution |
| SPICE | QuickSight's in-memory calculation engine |
| Shard | Unit of capacity in Kinesis Data Streams |
| Crawler | Glue component that discovers data schemas |

## 💡 Key Takeaways

1. Amazon Athena provides serverless SQL queries on S3 data - pay only for data scanned
2. Amazon Redshift is a petabyte-scale data warehouse optimized for analytics workloads
3. Amazon EMR runs big data frameworks like Spark, Hadoop, and Presto at scale
4. Amazon Kinesis handles real-time streaming data collection and processing
5. Kinesis Data Streams requires manual management; Firehose is fully managed
6. Amazon QuickSight is a serverless BI service for creating dashboards
7. AWS Glue provides serverless ETL and the Data Catalog for metadata management
8. AWS Lake Formation simplifies building secure data lakes with fine-grained access control
9. Use Athena for ad-hoc queries and Redshift for frequent, complex analytics
10. Use columnar formats (Parquet, ORC) to optimize costs and performance with Athena
11. Glue Crawlers automatically discover and catalog data schemas

---

*Previous: [01 - AI/ML Services](../01-ai-ml-services/readme.md)*

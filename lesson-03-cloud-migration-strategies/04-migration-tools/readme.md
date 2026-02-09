# AWS Migration Tools

## Overview

AWS provides a comprehensive set of tools to help organizations migrate workloads to the cloud. These tools support various migration strategies and simplify the migration process from discovery to validation.

## Migration Tool Categories

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    AWS Migration Tool Categories                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐        │
│   │    Discovery    │  │   Migration     │  │   Database      │        │
│   │    & Planning   │  │   Execution     │  │   Migration     │        │
│   └─────────────────┘  └─────────────────┘  └─────────────────┘        │
│                                                                          │
│   ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐        │
│   │    Data         │  │    VMware       │  │   Application   │        │
│   │    Transfer     │  │    Migration    │  │   Modernization │        │
│   └─────────────────┘  └─────────────────┘  └─────────────────┘        │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Key Migration Tools

### 1. AWS Migration Hub

**Purpose**: Central location to track migrations across AWS tools

| Feature | Description |
|---------|-------------|
| **Discovery** | Collect data about on-premises environment |
| **Tracking** | Monitor migration progress |
| **Integration** | Works with other migration tools |
| **Dashboard** | Single view of migration status |

### 2. AWS Application Discovery Service

**Purpose**: Discover and collect data about on-premises servers

| Feature | Description |
|---------|-------------|
| **Agent-based** | Deep data collection (requires agent) |
| **Agentless** | Basic discovery (no agent needed) |
| **Data Collected** | CPU, memory, disk, network, processes |
| **Export** | Export data for analysis |

### 3. AWS Application Migration Service (MGN)

**Purpose**: Lift and shift migration of servers (formerly CloudEndure Migration)

```
On-Premises Server          AWS Application Migration Service           AWS
┌─────────────┐            ┌──────────────────────────┐         ┌──────────┐
│   Source    │  ────────► │  • Continuous replication │ ────►  │  EC2     │
│   Server    │            │  • Non-disruptive testing  │        │ Instance │
│             │            │  • Cutover automation      │        │          │
└─────────────┘            └──────────────────────────┘         └──────────┘
```

| Feature | Description |
|---------|-------------|
| **Continuous Replication** | Real-time data sync |
| **Non-disruptive Testing** | Test without affecting source |
| **Automated Conversion** | Converts to AWS format |
| **Minimal Downtime** | Cutover in minutes |

### 4. AWS Database Migration Service (DMS)

**Purpose**: Migrate databases to AWS with minimal downtime

| Feature | Description |
|---------|-------------|
| **Homogeneous** | Same database engine (Oracle → RDS Oracle) |
| **Heterogeneous** | Different engines (Oracle → Aurora PostgreSQL) |
| **Continuous Replication** | Keep source and target in sync |
| **Minimal Downtime** | Migrate while database is in use |

#### Supported Sources and Targets

| Sources | Targets |
|---------|---------|
| Oracle | Amazon RDS |
| SQL Server | Amazon Aurora |
| MySQL | Amazon DynamoDB |
| PostgreSQL | Amazon Redshift |
| MongoDB | Amazon S3 |
| SAP | Amazon DocumentDB |

### 5. AWS Schema Conversion Tool (SCT)

**Purpose**: Convert database schemas for heterogeneous migrations

| Feature | Description |
|---------|-------------|
| **Schema Conversion** | Convert DB schema |
| **Code Conversion** | Convert stored procedures, functions |
| **Assessment Report** | Identify conversion challenges |
| **Integration** | Works with DMS |

### 6. AWS DataSync

**Purpose**: Transfer data between on-premises and AWS

| Feature | Description |
|---------|-------------|
| **High Speed** | Up to 10x faster than open-source tools |
| **Automatic** | Handles encryption, integrity validation |
| **Targets** | S3, EFS, FSx |
| **Scheduling** | Automate transfers |

### 7. AWS Snow Family

**Purpose**: Physical devices for large-scale data transfer

| Device | Storage | Use Case |
|--------|---------|----------|
| **Snowcone** | 8-14 TB | Edge computing, small transfers |
| **Snowball Edge** | 80-210 TB | Large migrations, edge computing |
| **Snowmobile** | 100 PB | Massive data center migrations |

### 8. AWS Transfer Family

**Purpose**: Managed file transfer to S3 and EFS

| Protocol | Description |
|----------|-------------|
| **SFTP** | Secure File Transfer Protocol |
| **FTPS** | FTP over SSL |
| **FTP** | File Transfer Protocol |
| **AS2** | Applicability Statement 2 |

## VMware Migration Tools

### VMware Cloud on AWS
- Run VMware workloads on AWS infrastructure
- Use familiar VMware tools
- vMotion support for live migration

### Migration Tools Comparison

| Tool | Use Case | Strategy |
|------|----------|----------|
| **Migration Hub** | Central tracking | All |
| **Application Discovery** | Discovery & planning | All |
| **Application Migration Service** | Server migration | Rehost |
| **DMS** | Database migration | Rehost, Replatform |
| **SCT** | Schema conversion | Replatform |
| **DataSync** | File transfer | All |
| **Snow Family** | Large data transfer | All |
| **VMware Cloud** | VMware workloads | Relocate |

## Migration Process Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     Typical Migration Process                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  1. DISCOVER                2. ASSESS                3. PLAN            │
│  ┌──────────────┐          ┌──────────────┐        ┌──────────────┐    │
│  │ Application  │ ───────► │ Migration    │ ────►  │ Migration    │    │
│  │ Discovery    │          │ Hub          │        │ Strategy     │    │
│  │ Service      │          │ Assessment   │        │              │    │
│  └──────────────┘          └──────────────┘        └──────────────┘    │
│                                                           │              │
│                                                           ▼              │
│  6. VALIDATE               5. CUTOVER               4. MIGRATE          │
│  ┌──────────────┐         ┌──────────────┐        ┌──────────────┐     │
│  │ Testing &    │ ◄────── │ Final        │ ◄───── │ MGN, DMS,    │     │
│  │ Optimization │         │ Switchover   │        │ DataSync     │     │
│  └──────────────┘         └──────────────┘        └──────────────┘     │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

## Exam Tips

- **AWS Application Migration Service (MGN)** is for lift-and-shift server migrations
- **AWS DMS** migrates databases with minimal downtime
- **AWS SCT** converts database schemas (use with DMS for heterogeneous migrations)
- **AWS DataSync** is for transferring files to S3, EFS, FSx
- **Snow Family** is for large-scale offline data transfer
- **Migration Hub** provides a central dashboard for tracking
- Know the difference between **homogeneous** (same engine) and **heterogeneous** (different engine) database migrations

## Key Takeaways

1. **Migration Hub** is your central tracking dashboard
2. **Application Discovery Service** helps plan migrations
3. **MGN** is the primary tool for server lift-and-shift
4. **DMS + SCT** work together for database migrations
5. **Snow Family** is for large offline data transfers
6. **DataSync** is for ongoing file synchronization
7. Choose tools based on your **migration strategy** (7 R's)

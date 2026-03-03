# 🗄️ Comparison-between-Types-of-Databases

## 📋 Table of Contents
- [Overview](#-overview)
- [Database Types](#️-database-types)
- [General Classification](#general-classification-of-analyzed-databases)
- [Distributed Databases](#1-distributed-databases)
- [NoSQL Databases](#2-nosql-databases)
- [Serverless Databases](#3-serverless-databases)
- [Fault-Tolerant Databases](#4-fault-tolerant-databases)
- [Databases with Checkpointing](#5-databases-with-checkpointing)
- [Delta Lake / Data Lake](#6-delta-lake--data-lake)
- [Head-to-Head Comparisons](#-head-to-head-comparisons)
- [Selection Guide](#-selection-guide-when-to-use-each-type)
- [Synchronization & Consistency](#-synchronization--consistency-protocols)
- [Conclusions](#-conclusions)
- [References](#-references)
<br>

## 📝 Overview
This repository documents a comparative study of the main types of modern databases, analyzing their characteristics, advantages, limitations, and ideal use cases. The following categories are covered:
| Category | Databases Analyzed |
|----------|--------------------|
| Distributed | PouchDB, MongoDB, Amazon DynamoDB, Apache Couchbase, CockroachDB |
| NoSQL | MongoDB, Riak, Amazon DynamoDB, Apache Couchbase |
| Serverless | Amazon Aurora Serverless, CockroachDB Cloud |
| Fault-Tolerant | RIAK, MySQL Cluster |
| Checkpointing | SQLite, Neo4j |
| Delta Lake | Delta Lake (Databricks) |
<br>

## 🗂️ Database Types
### General Classification of Analyzed Databases
| Database | Distributed | NoSQL | Serverless | Fault-Tolerant | Checkpointing | Data Model |
|----------|:-----------:|:-----:|:----------:|:--------------:|:-------------:|------------|
| **MongoDB** | ✅ | ✅ | ✅ (Atlas) | ✅ | ✅ | Document |
| **RIAK** | ✅ | ✅ | ❌ | ✅ | ❌ | Key-Value |
| **Amazon DynamoDB** | ✅ | ✅ | ✅ | ✅ | ❌ | Key-Value / Document |
| **Apache Couchbase** | ✅ | ✅ | ❌ | ✅ | ❌ | Document |
| **CockroachDB** | ✅ | ❌ | ✅ | ✅ | ❌ | Distributed Relational |
| **Amazon Aurora Serverless** | ✅ | ❌ | ✅ | ✅ | ❌ | Relational |
| **MySQL Cluster** | ✅ | ❌ | ❌ | ✅ | ✅ | Relational |
| **SQLite** | ❌ | ❌ | ❌ | ❌ | ✅ | Embedded Relational |
| **Neo4j** | ✅ (paid) | ✅ | ❌ | ✅ (paid) | ✅ | Graph |
| **PouchDB** | ✅ | ✅ | ❌ | ✅ | ❌ | Document |
| **Delta Lake** | ✅ | ❌ | ❌ | ✅ | ✅ | Data Lakehouse |
| **PostgreSQL** | ❌ (native) | ❌ | ❌ | ✅ | ✅ | Relational |
<br>

## 1. Distributed Databases
Systems that store data across multiple physical locations but behave as a single unified system, allowing transparent and simultaneous access from different sites.

### Key Characteristics
| Feature | Description | Analogy |
|---------|-------------|---------|
| **Location Transparency** | Hides the physical location of data from the user | Ordering pizza via an app without knowing which branch fulfills it |
| **Fragmentation Independence** | Manages how data is split and stored (horizontal/vertical) | Splitting by rows (horizontal) or by columns (vertical) |
| **Local Autonomy** | Each node operates independently | Branch offices running locally while belonging to the same organization |
| **Synchronization** | Keeps data consistent across the network | Real-time collaborative editing in Google Docs |
| **Failure Handling** | Recovery strategies for node-level errors | Substituting an injured player during a match |
| **Security** | Encryption, authentication, and distributed access control | Home alarm system with different locks on each door |
| **Scalability** | Increases capacity by adding more nodes | Adding wagons to a train to carry more passengers |
| **Load Balancing** | Distributes operations evenly across nodes | Multiple checkout lanes in a supermarket |
<br>

### Notable Distributed Databases
| Database | Node Type | Scalability | Consistency | Primary Use Case |
|----------|:---------:|:-----------:|:-----------:|------------------|
| Apache Cassandra | Peer-to-peer | Horizontal | Eventual | IoT, time-series data |
| Apache HBase | Master-Slave | Horizontal | Strong | Big Data on Hadoop |
| MongoDB | Replica Set / Sharding | Horizontal | Configurable | Modern web applications |
| Amazon DynamoDB | Managed (AWS) | Automatic | Eventual / Strong | High-traffic serverless apps |
| CockroachDB | Peer-to-peer | Horizontal | Strong (ACID) | Finance, global applications |
| PouchDB | Peer-to-peer (sync CouchDB) | Limited | Eventual | Offline-first apps |
| Redis | Master-Slave / Cluster | Horizontal | Configurable | Cache, sessions, queues |
<br>

## 2. NoSQL Databases
Systems that do not use the typical SQL relational model. Useful for handling large volumes of sparse data and varied data structures.

### NoSQL Data Models
| Model | Description | Databases | Ideal Use Case |
|-------|-------------|-----------|----------------|
| **Key-Value** | Simple key → value pair | Redis, RIAK, DynamoDB | Cache, sessions, configurations |
| **Document** | Nested JSON/BSON documents | MongoDB, CouchDB, Couchbase | Catalogs, user profiles |
| **Columnar** | Data organized by columns | Apache Cassandra, HBase | Time-series, analytics |
| **Graph** | Nodes and relationships | Neo4j, Amazon Neptune | Social networks, recommendations |
| **Multi-model** | Combination of models | ArangoDB, Couchbase | Heterogeneous data applications |
<br>

### NoSQL Comparative Feature Matrix
| Feature | MongoDB | RIAK | DynamoDB | Couchbase | CouchDB |
|---------|:-------:|:----:|:--------:|:---------:|:-------:|
| Flexible schema | ✅ | ✅ | ✅ | ✅ | ✅ |
| Horizontal scalability | ✅ | ✅ | ✅ | ✅ | ✅ |
| Eventual consistency | ✅ | ✅ | ✅ | ✅ | ✅ |
| ACID support | ✅ (4.0+) | ❌ | ❌ (partial) | ✅ | ❌ |
| Ad-hoc queries | ✅ | ❌ | Limited | ✅ | ✅ |
| Secondary indexes | ✅ | ✅ | ✅ | ✅ | ✅ |
| Open source | ✅ | ✅ | ❌ | ✅ (CE) | ✅ |
<br>

## 3. Serverless Databases
Services where the cloud provider automatically handles scaling and optimization. Users pay only for the resources they consume.

### Key Characteristics
| Feature | Description | Advantage |
|---------|-------------|-----------|
| **Automatic Elasticity** | Resources scale automatically based on load | No over-provisioning |
| **Pay-per-Use Model** | Costs based on exact resource consumption | Cost reduction for variable workloads |
| **Simplified Management** | Provider handles infrastructure and maintenance | Lower operational burden for the team |
| **Cloud Integration** | Native connectivity with other cloud services | Integrated ecosystem |
| **Agile Development** | Developers focus solely on code | Faster development cycles |
<br>

### Serverless Solutions Comparison
| Platform | Provider | Underlying Engine | Min Scale | Max Scale | Cold Start | Billing Basis |
|----------|----------|-------------------|:---------:|:---------:|:----------:|---------------|
| **Amazon Aurora Serverless** | AWS | MySQL / PostgreSQL | 0 ACU | Configurable | ~5–30s | Per ACU/hour |
| **CockroachDB Serverless** | Cockroach Labs | CockroachDB | 0 | Automatic | Minimal | Per RU consumed |
| **MongoDB Atlas Serverless** | MongoDB Inc. | MongoDB | 0 | Automatic | Minimal | Per operation |
| **PlanetScale** | PlanetScale | Vitess/MySQL | 0 | Automatic | Minimal | Per row read/written |
| **FaunaDB** | Fauna | Fauna | 0 | Automatic | Minimal | Per operation |
| **Firebase Realtime DB** | Google | Proprietary | 0 | Automatic | None | Per GB stored / downloaded |
<br>

## 4. Fault-Tolerant Databases
Systems designed to guarantee data availability and integrity even when component failures occur, through techniques such as replication and automatic recovery.

### Fault Tolerance Mechanisms
| Mechanism | Description | Analogy |
|-----------|-------------|---------|
| **Replication** | Data copies maintained across multiple nodes | Keeping copies of a music album stored in different locations |
| **Automatic Recovery** | Resumes operations automatically after a failure | Streaming service that switches networks without user intervention |
| **Automatic Failover** | Switches to backup systems without manual intervention | Emergency generator in a hospital that activates on power outage |
| **Load Balancing** | Distributes load to reduce single points of failure | Highway with multiple lanes — traffic diverts if one is blocked |
| **Continuous Monitoring** | Constant supervision to detect and resolve issues quickly | Home alarm system that alerts when something goes wrong |
<br>

### Replication Types
| Type | How It Works | Consistency | Performance | Use Case |
|------|-------------|:-----------:|:-----------:|----------|
| **Synchronous** | Transaction is not committed until all replicas are updated | High | ↓ Lower (latency) | Critical financial data |
| **Asynchronous** | Replicas are updated with a delay | Eventual | ↑ Higher | Logs, analytics, media content |
<br>

### Load Balancing Algorithms
| Algorithm | How It Works | Advantage | Limitation |
|-----------|-------------|-----------|------------|
| **Round Robin** | Distributes requests sequentially across all nodes | Simple and predictable | Ignores current node load |
| **Least Connections** | Routes to the node with fewest active connections | Fairer under variable loads | Higher tracking overhead |
| **Consistent Hashing** | Distributes via hash function over keys | Reference locality, fewer redistributions | More complex to implement |
<br>


## 5. Databases with Checkpointing
Databases that periodically save a snapshot of their state to enable fast recovery in the event of a failure, reducing the time needed to restore the system.

### Key Concepts
| Concept | Description | Analogy |
|---------|-------------|---------|
| **Control Points** | System state saved at regular intervals | Auto-saving a document while working on it |
| **Fast Recovery** | Resumes from the last checkpoint instead of rebuilding from scratch | Restarting a video game from the last save point |
| **Data Loss Minimization** | Frequent checkpoints reduce the window of potential data loss | Multiple save slots in a game |
| **Performance Efficiency** | Balance between checkpoint frequency and overall system throughput | Deciding how often to save a long project |
| **Automation** | Checkpoints triggered automatically by time or specific events | Scheduled automatic irrigation system |
<br>

### Checkpointing Types
| Type | How It Works | Performance Impact | Recovery Complexity |
|------|-------------|:-----------------:|:-------------------:|
| **Synchronous** | All queries pause while state is written to persistent storage | High (introduces latency) | Low (state is always consistent) |
| **Asynchronous** | Queries continue while the checkpoint is being written | Low | High (must account for concurrent queries during checkpoint) |
<br>

### Log-Based Recovery Theory (WAL)
| Operation | Description | When It Applies |
|-----------|-------------|-----------------|
| **REDO** | Re-executes operations that completed before the failure but were not fully persisted | Commit occurred but data was not written to disk |
| **UNDO** | Rolls back operations that were in progress at the time of failure | Transaction left the system in an inconsistent state |
<br>

## 6. Delta Lake / Data Lake
### Data Lake vs Data Warehouse vs Data Lakehouse
| Feature | Data Lake | Data Warehouse | Data Lakehouse |
|---------|:---------:|:--------------:|:--------------:|
| Data type | Raw / unstructured | Structured | Both |
| Schema approach | Schema-on-read | Schema-on-write | Both |
| Storage cost | Low | High | Low–Medium |
| Data quality | Variable | High | High |
| ACID transactions | ❌ | ✅ | ✅ |
| ML / AI support | ✅ | Limited | ✅ |
| Underlying technology | Hadoop / S3 | Proprietary SQL | Delta Lake / Iceberg |
| Scalability | Petabytes | Terabytes | Petabytes |
| Schema flexibility | High | Low | High |
<br>

### Delta Lake Feature Breakdown
| Feature | Description | Benefit |
|---------|-------------|---------|
| **Open Storage Format (Parquet)** | Columnar format optimized for large datasets | High compression and fast analytical reads |
| **ACID Transactions** | Atomic, consistent, isolated, and durable operations | Guaranteed data integrity |
| **Time Travel (Data Versioning)** | View and restore data to a previous point in time | Auditing and recovery from accidental changes |
| **Schema Evolution** | Schema changes without rewriting entire datasets | Flexibility in evolving data pipelines |
| **Apache Spark Integration** | Distributed high-performance processing | Scalability for big data workloads |
| **Unified Batch + Streaming** | Both processing modes on the same platform | Simplified architecture |
| **Z-Order Optimization** | Co-locates related data to minimize read overhead | Faster analytical query performance |
<br>

## 🔍 Head-to-Head Comparisons
### MongoDB vs MySQL
| Criterion | MongoDB | MySQL |
|-----------|:-------:|:-----:|
| Data model | Documents (JSON/BSON) | Relational (tables) |
| Schema | Flexible / dynamic | Rigid / static |
| Scalability | Native horizontal | Vertical (primarily) |
| Query language | MQL (MongoDB Query Language) | Standard SQL |
| ACID transactions | ✅ (v4.0+) | ✅ |
| Complex joins | ❌ (embedded docs / $lookup) | ✅ |
| Performance on unstructured data | ✅ Superior | ❌ Inferior |
| Strict security & consistency | ❌ Weaker | ✅ Stronger |
| Ideal use cases | Modern apps, variable schemas | ERP, finance, structured data |
<br>

### RIAK vs MongoDB
| Criterion | RIAK | MongoDB |
|-----------|:----:|:-------:|
| Data model | Key-Value | Document |
| Master node | ❌ (masterless) | ✅ (primary node) |
| Single point of failure | ❌ None | ✅ Possible |
| Data distribution | Consistent ring (SHA-1 hash) | Sharding |
| Ad-hoc queries | Very limited | ✅ Full support |
| Fault tolerance | ✅ Very high | ✅ High |
| Operational complexity | Medium | Medium–High |
<br>

### Neo4j vs Relational Databases
| Criterion | Neo4j | PostgreSQL / MySQL |
|-----------|:-----:|:-----------------:|
| Data model | Graph (nodes + relationships) | Relational tables |
| Complex relationship queries | ✅ Native and efficient | ❌ Expensive JOINs |
| Query language | Cypher / Gremlin | SQL |
| Use cases | Social networks, fraud detection, recommendations | Transactions, reporting |
| Horizontal scalability | ✅ (enterprise edition) | Limited |
| ACID support | ✅ | ✅ |
<br>

## 🧭 Selection Guide: When to Use Each Type
| Need / Scenario | Recommendation | Reason |
|-----------------|----------------|--------|
| Simple app, single server, low traffic | SQLite / MySQL | Lightweight, zero configuration |
| Modern web app with variable or evolving data | MongoDB | Flexible schema, horizontally scalable |
| High availability with no single point of failure | RIAK | Masterless architecture |
| Complex relationship queries / debugging | Neo4j | Graph model with native BFS traversal |
| Large-scale data versioning and auditing | Delta Lake | Time travel, ACID guarantees, Parquet format |
| Fully managed cloud infrastructure | Amazon Aurora Serverless / DynamoDB | No server management required |
| Offline-capable app with sync | PouchDB + CouchDB | Automatic bidirectional sync |
| High-volume distributed writes | Apache Cassandra | Write-optimized, peer-to-peer architecture |
| Real-time analytics + ML pipelines | Delta Lake + Spark | Unified batch and streaming platform |
| Distributed financial / transactional data | CockroachDB | Distributed ACID with standard SQL interface |
<br>

## 🔄 Synchronization & Consistency Protocols
### CAP Theorem
> Any distributed system can only guarantee **2 out of 3** properties simultaneously:
| Property | Description |
|----------|-------------|
| **C** — Consistency | All nodes see the same data at the same time |
| **A** — Availability | Every request receives a response |
| **P** — Partition Tolerance | The system operates even if communication between nodes fails |
<br>

| Database | CAP Guarantee |
|----------|:-------------:|
| MongoDB | CP |
| RIAK | AP |
| Cassandra | AP |
| HBase | CP |
| CockroachDB | CP |
| DynamoDB | AP (configurable) |
<br>

### Consistency Levels
| Level | Description | Performance Cost | Typical Use |
|-------|-------------|:----------------:|-------------|
| **Strong** | Every read returns the most recently written value | High | Banks, real-time inventory |
| **Causal** | Causally related operations are seen in order | Medium | Social networks, messaging |
| **Eventual** | Data converges to the same value eventually, with no timing guarantee | Low | DNS, shopping carts, likes |
| **Weak** | No synchronization guarantees | Minimal | Metrics, telemetry |
<br>

### Synchronization Protocols
| Protocol | Description | Advantage | Limitation |
|----------|-------------|-----------|------------|
| **Distributed Locking** | Controls access to data during concurrent transactions | Prevents write conflicts | Can cause deadlocks |
| **Timestamps** | Each transaction receives a unique timestamp to establish ordering | Deterministic ordering | Requires clock synchronization across nodes |
| **Two-Phase Commit (2PC)** | All nodes must agree before a transaction is committed | Full consistency guarantee | Slow or blocked if a node fails mid-protocol |
<br>

## 📊 Visual Summary by Use Case

```
Data Volume
     │
HIGH │  Delta Lake ──── Cassandra ──── HBase
     │       │               │
     │    DynamoDB        MongoDB
     │       │
 LOW │   SQLite ─── MySQL ─── PostgreSQL ─── Neo4j
     └──────────────────────────────────────────────
         Simple      Distributed     Graph / Analytics
                   (architecture type)
```
<br>

## 📌 Conclusions
1. **There is no universal database engine**: each system has advantages and limitations depending on the environment and requirements.
2. **For simple environments**: SQLite or MySQL are sufficient and efficient with minimal setup.
3. **For large-scale data versioning and auditing**: Delta Lake is the most robust option available.
4. **For fault tolerance with no single point of failure**: RIAK stands out thanks to its masterless, ring-based architecture.
5. **For debugging and relationship-heavy queries**: Neo4j simplifies analysis through its native graph model and depth-first search traversal.
6. **Benchmarks are environment-dependent**: hardware, software, operating system, and network bandwidth all directly affect each engine's behavior, making fair cross-system comparisons challenging without a controlled environment.
<br>

## 📚 References
| # | Resource | Link |
|---|----------|------|
| 1 | Oracle — Distributed Database Concepts | [docs.oracle.com](https://docs.oracle.com/en/database/oracle/oracle-database/19/admin/distributed-database-concepts.html) |
| 4 | The Definitive Guide to NoSQL Databases | [toptal.com](https://www.toptal.com/database/the-definitive-guide-to-nosql-databases) |
| 9 | AWS — What is a serverless database? | [aws.amazon.com](https://aws.amazon.com/es/what-is/serverless-database/) |
| 11 | CockroachDB — What is a serverless database? | [cockroachlabs.com](https://www.cockroachlabs.com/blog/what-is-a-serverless-database/) |
| 22 | Microsoft — What is Delta Lake? | [learn.microsoft.com](https://learn.microsoft.com/es-es/azure/databricks/delta/) |
| 23 | Delta Lake — The Linux Foundation | [delta.io](https://delta.io/) |
| 32 | MongoDB — Introduction to MongoDB | [mongodb.com](https://www.mongodb.com/docs/manual/introduction/) |
| 39 | IBM Cloud — Riak | [cloud.ibm.com](https://cloud.ibm.com/docs/database-tools?topic=database-tools-dbt-about-riak) |
| 47 | Neo4j — The Graph Data Platform | [neo4j.com](https://neo4j.com/es/producto/) |
| 53 | Pure Storage — What is Delta Lake? | [purestorage.com](https://www.purestorage.com/la/knowledge/what-is-delta-lake.html) |
| 55 | IBM — What is the CAP Theorem? | [ibm.com](https://www.ibm.com/mx-es/topics/cap-theorem) |
| 57 | PostgreSQL 16.2 Documentation | [postgresql.org](https://www.postgresql.org/files/documentation/pdf/16/postgresql-16-A4.pdf) |
| 58 | Kinsta — MongoDB vs MySQL | [kinsta.com](https://kinsta.com/blog/mongodb-vs-mysql/) |

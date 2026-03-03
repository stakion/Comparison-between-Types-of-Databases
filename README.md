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



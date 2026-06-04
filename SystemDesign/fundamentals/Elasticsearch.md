# 📘 Elasticsearch - Complete System Design Guide

---

# What is Elasticsearch?

Elasticsearch is a **distributed search and analytics engine** built on top of Apache Lucene.

It is designed to provide:

* Full-text search
* Fast filtering
* Aggregations
* Log analytics
* Autocomplete
* Search suggestions
* Real-time analytics

Unlike a traditional database, Elasticsearch is optimized for **search operations** rather than transactional workloads.

---

# Why Do We Need Elasticsearch?

Consider a system with millions of records.

Example:

```text
Users: 10 Million
Orders: 100 Million
Products: 50 Million
```

Searching using SQL:

```sql
SELECT *
FROM Users
WHERE Name LIKE '%Varun%'
```

works for small datasets but becomes expensive as data grows.

Elasticsearch uses **inverted indexes**, allowing searches across millions or billions of documents in milliseconds.

---

# Is Elasticsearch a Database?

Technically, yes—it stores data.

However, in system design interviews and production systems, Elasticsearch is usually treated as:

> A Search Engine, not the System of Record.

---

# Does Elasticsearch Store Data?

Yes.

Elasticsearch stores:

* Documents
* Search indexes
* Metadata
* Aggregation structures

Example document:

```json
{
  "userId": 1001,
  "name": "Varun Nayak",
  "location": "Illinois",
  "skills": ["C#", ".NET", "Azure"]
}
```

The data exists inside Elasticsearch.

It does NOT simply store pointers to a relational database.

---

# Elasticsearch vs Relational Database

| Feature           | PostgreSQL/MySQL | Elasticsearch |
| ----------------- | ---------------- | ------------- |
| Source of Truth   | ✅                | ❌             |
| ACID Transactions | ✅                | ❌             |
| Joins             | ✅                | Limited       |
| Full-Text Search  | Basic            | Excellent     |
| Filtering         | Good             | Excellent     |
| Aggregations      | Good             | Excellent     |
| Search Ranking    | Limited          | Excellent     |
| Analytics         | Moderate         | Excellent     |

---

# Why Not Use Elasticsearch as the Main Database?

Because Elasticsearch is optimized for search, not transactions.

Example:

## Banking System

Transfer $100:

```text
Account A -> -100
Account B -> +100
```

If a failure occurs midway:

```text
Account A = Updated
Account B = Not Updated
```

Financial systems require:

* ACID Transactions
* Rollbacks
* Referential Integrity
* Constraints
* Consistency

Traditional databases provide these guarantees.

Elasticsearch does not.

---

# Why Elasticsearch Cannot Replace SQL Databases

Relational databases support:

```text
Users
Orders
Payments
Products
Inventory
```

with:

* Foreign Keys
* Transactions
* Joins
* Constraints

Elasticsearch is designed around:

```text
Search
Filtering
Analytics
Aggregations
```

Therefore:

```text
PostgreSQL = System of Record

Elasticsearch = Search Layer
```

---

# What is Denormalization?

Relational databases store data across multiple tables.

Example:

```text
Users
Skills
Companies
Education
```

SQL performs joins.

```sql
SELECT *
FROM Users
JOIN Skills
JOIN Companies
```

Elasticsearch avoids joins.

Instead, it stores:

```json
{
  "userId": 1001,
  "name": "Varun Nayak",
  "company": "InRule",
  "skills": ["C#", ".NET", "Azure"]
}
```

Everything needed for search exists inside one document.

This is called:

> Denormalization

---

# Elasticsearch vs Cache (Redis)

Many people confuse Elasticsearch with Redis.

## Redis

Stores:

```text
Frequently Accessed Data
```

Examples:

* User Sessions
* Shopping Cart
* API Responses

Usually:

```text
5% - 20% of total data
```

---

## Elasticsearch

Stores:

```text
Entire Searchable Dataset
```

Example:

```text
10 Million User Profiles
```

or

```text
100 Million Products
```

Elasticsearch is NOT a cache.

It is a search index.

---

# Elasticsearch vs Redis

| Feature                      | Redis      | Elasticsearch |
| ---------------------------- | ---------- | ------------- |
| Cache                        | ✅          | ❌             |
| Search Engine                | ❌          | ✅             |
| Session Storage              | ✅          | ❌             |
| Full Text Search             | Limited    | Excellent     |
| Source of Truth              | ❌          | ❌             |
| Stores Entire Search Dataset | Usually No | Usually Yes   |

---

# Typical Architecture

```text
                  Search Request
User --------------------------------> Elasticsearch

                                          ^
                                          |
                                          |
                                     Kafka/Event
                                          |
                                          |
                                          v

                                    PostgreSQL
                               (Source of Truth)
```

---

# How New Data Reaches Elasticsearch

There are several approaches.

---

## Approach 1: Dual Write

```text
Application
     |
     +--> PostgreSQL
     |
     +--> Elasticsearch
```

Example:

```csharp
SaveUser();

SaveToPostgres();

SaveToElastic();
```

### Problem

If PostgreSQL succeeds and Elasticsearch fails:

```text
Data becomes inconsistent
```

Not recommended for large systems.

---

## Approach 2: Event-Driven Architecture (Recommended)

```text
User
 |
API
 |
PostgreSQL
 |
Kafka / Service Bus
 |
Search Indexer
 |
Elasticsearch
```

### Flow

Step 1

```text
User Created
```

Step 2

```text
Save to PostgreSQL
```

Step 3

```text
Publish Event
```

```json
{
  "eventType": "UserCreated",
  "userId": 1001
}
```

Step 4

```text
Indexer Service Consumes Event
```

Step 5

```text
Update Elasticsearch
```

Benefits:

* Reliable
* Scalable
* Retry Support
* Eventual Consistency

---

## Approach 3: Change Data Capture (CDC)

Modern approach.

```text
PostgreSQL
      |
Transaction Log
      |
Debezium
      |
Kafka
      |
Indexer
      |
Elasticsearch
```

CDC automatically captures:

```sql
INSERT
UPDATE
DELETE
```

from database transaction logs.

No application code changes required.

---

# Common Elasticsearch Tools

## Elasticsearch

Stores and searches documents.

---

## Kibana

Used for:

* Dashboards
* Search Exploration
* Analytics
* Visualization

---

## Logstash

Used for:

* ETL
* Data Transformation
* Log Processing

---

## Beats

Lightweight agents for shipping logs.

Examples:

```text
Filebeat
Metricbeat
Auditbeat
Heartbeat
```

---

## Kafka

Frequently used for:

```text
Database Changes
Events
Search Index Updates
```

---

## Debezium

CDC platform.

Captures database changes and pushes them into Kafka.

---

# ELK Stack

Most popular logging architecture.

```text
Applications
      |
      v
   Logstash
      |
      v
 Elasticsearch
      |
      v
    Kibana
```

ELK stands for:

```text
E = Elasticsearch
L = Logstash
K = Kibana
```

---

# Real World Use Cases

## E-Commerce

Search:

```text
iPhone 17 Pro
```

with:

* Filters
* Sorting
* Facets

---

## LinkedIn

Search:

```text
C# Developers in Chicago
```

---

## Netflix

Search:

```text
Action Movies
```

---

## Log Analytics

Search:

```text
Error Logs
Last 24 Hours
```

---

## Autocomplete

Example:

```text
Ama...
```

Suggestions:

```text
Amazon
Amazon Prime
Amazon Music
```

---

# Interview Answer

When asked:

### Why Elasticsearch?

Answer:

> Elasticsearch is a distributed search engine used for full-text search, filtering, and analytics. It stores a denormalized searchable copy of data while the primary relational database remains the source of truth.

### Why Not Use Elasticsearch as Database?

Answer:

> Elasticsearch lacks strong transactional guarantees and relational capabilities. It is optimized for search workloads, while relational databases provide ACID transactions and data consistency.

### How Is Data Synced?

Answer:

> New data is written to PostgreSQL first. Events are published through Kafka or captured using CDC tools like Debezium. An indexing service then updates Elasticsearch asynchronously, providing eventual consistency.

---

# Key Takeaway

```text
PostgreSQL = Source of Truth

Kafka / CDC = Synchronization Layer

Elasticsearch = Search Layer

Redis = Cache Layer
```

This architecture is commonly used in large-scale systems such as LinkedIn, Amazon, Netflix, Uber, and many enterprise applications.

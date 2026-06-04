# 📘 CAP Theorem & Data Consistency Summary

## 🔧 What is Data Consistency?
In distributed systems, data consistency refers to how up-to-date and synchronized data is across multiple nodes or replicas. Different consistency models offer trade-offs between performance, availability, and correctness.

## 🧠 CAP Theorem

### 📘 Definition:
CAP stands for:
- **Consistency (C):** Every read receives the most recent write or an error.
- **Availability (A):** Every request receives a (non-error) response, without guarantee of the latest write.
- **Partition Tolerance (P):** The system continues to operate despite network partitions (communication failures between nodes).

### ⚠️ The Rule:
In a distributed system, you can only guarantee **two out of the three properties** at any given time.

### 📈 CAP Triangle (Text Representation):
```
   Consistency
     /     \
    /       \
Availability — Partition Tolerance
```

## 🔍 CAP Trade-Off Examples
| System Type | CAP Trade-Off | Example Systems |
|--------------|---------------|-----------------|
| **CP (Consistent + Partition Tolerant)** | Sacrifices availability | HBase, MongoDB (strong consistency) |
| **AP (Available + Partition Tolerant)** | Sacrifices consistency | Cassandra, Couchbase |
| **CA (Consistent + Available)** | Not possible in distributed systems with partitions | Single-node systems only |

## 🔄 Eventual Consistency

### 📘 Definition:
Eventual consistency means that, given enough time and no new updates, all replicas in a distributed system will converge to the same state.

### 🔧 Characteristics:
- Reads may return stale data temporarily.
- System guarantees that data will eventually be consistent.
- Common in high-availability systems.

### 🧠 Use Cases:
- DNS systems
- Social media feeds
- Shopping carts
- Distributed caches

## 🔍 Strong vs Eventual Consistency
| Consistency Model | Guarantees | Trade-Offs |
|--------------------|-------------|-------------|
| **Strong Consistency** | Every read reflects the latest write | Lower availability, higher latency |
| **Eventual Consistency** | Reads may be stale, but converge over time | High availability, better performance |

## 🛒 Scenario 1: Shopping Cart System
**✅ Best Fit: Strong Consistency (CP)**
- Cart must reflect the latest state during checkout.
- Prevents charging for removed items or missing added items.
- Uses CP systems like MongoDB or relational databases.

## 💬 Scenario 2: Messaging App
**✅ Best Fit: Eventual Consistency (AP)**
- Messages can arrive slightly late or out of order.
- Prioritizes availability and performance.
- Uses AP systems like Cassandra or DynamoDB.

## 📊 Summary Table
| System | Consistency Model | CAP Type | Why It Fits |
|---------|------------------|-----------|--------------|
| **Shopping Cart** | Strong Consistency | CP | Ensures accurate checkout and item state |
| **Messaging App** | Eventual Consistency | AP | Prioritizes availability and performance |

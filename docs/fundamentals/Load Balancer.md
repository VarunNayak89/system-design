# 🔧 Load Balancing Overview

---

## 🔧 What is Load Balancing?

Load balancing is the process of distributing incoming network traffic across multiple servers to ensure:

- ✅ Reliability
- ✅ Scalability
- ✅ Performance

---

## ⚙️ Why Use Load Balancing?

- Prevent server overload  
- Improve fault tolerance  
- Enable horizontal scaling  
- Reduce latency for users  

---

## 🧠 Common Load Balancing Algorithms

### 1. **Round-Robin**
- Distributes requests sequentially across servers.
- Assumes all servers have equal capacity.

**Example:**
Request 1 → Server A
Request 2 → Server B
Request 3 → Server C
Request 4 → Server A (repeats)


**Pros:** Simple, fair distribution  
**Cons:** Doesn’t consider server load  

---

### 2. **Least Connections**
- Sends traffic to the server with the **fewest active connections**.

**Example:**
Server A: 10 connections
Server B: 5 connections
Server C: 2 connections → Next request goes here


**Pros:** Dynamic load awareness  
**Cons:** Requires real-time tracking  

---

### 3. **IP Hash**
- Uses a hash of the client’s IP to determine which server handles the request.

**Pros:** Ensures session persistence  
**Cons:** Uneven distribution if IPs are skewed  

---

### 4. **Weighted Round-Robin / Least Connections**
- Assigns **weights** to servers based on capacity.
- Higher weight = more requests.

**Example:**
Server A (weight 3), Server B (weight 1)
→ Server A gets 3x the traffic of Server B



**Pros:** Good for mixed server sizes  
**Cons:** Requires accurate weight config  

---

## 🛠️ Load Balancer Tools

| Tool                  | Type     | Features                                 |
|-----------------------|----------|------------------------------------------|
| NGINX                 | Software | Supports all major algorithms            |
| HAProxy               | Software | High-performance, flexible configuration |
| AWS Elastic LB        | Cloud    | Auto-scaling, health checks              |
| Azure Load Balancer   | Cloud    | Integrated with Azure services           |
| GCP Load Balancing    | Cloud    | Global distribution, autoscaling         |

---

## 📊 Load Balancing Algorithms Comparison

| Algorithm                | Distribution Logic                | Load Awareness | Session Persistence | Best Use Case                                 |
|--------------------------|-----------------------------------|----------------|----------------------|------------------------------------------------|
| **Round-Robin**          | Sequential rotation               | ❌ No          | ❌ No                | Simple, equal-capacity servers                |
| **Least Connections**    | Fewest active connections         | ✅ Yes         | ❌ No                | Dynamic traffic, long-lived connections       |
| **IP Hash**              | Hash of client IP                 | ❌ No          | ✅ Yes               | Sticky sessions, user affinity                |
| **Weighted Round-Robin** | Rotation based on server weights  | ❌ No          | ❌ No                | Mixed-capacity servers                        |
| **Weighted Least Conn.** | Fewest connections + weight       | ✅ Yes         | ❌ No                | Smart distribution with capacity awareness    |

---

## 🧠 Strategy Tips

- Use **Round-Robin** for simplicity with equal servers.
- Use **Least Connections** for **dynamic** workloads.
- Use **IP Hash** when **session persistence** is needed.
- Use **Weighted algorithms** when server capacities differ.

---

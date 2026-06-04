# System Design Tooling Landscape

A concise overview of core technologies commonly referenced in system design discussions and implementations.

---

## 🗄️ Relational (SQL) Databases
Structured databases that store data in tables with predefined schemas. Ideal for transactional systems requiring ACID compliance.

| Tool                  | Company                               |
|-----------------------|----------------------------------------|
| MySQL                 | Oracle                                 |
| PostgreSQL            | PostgreSQL Global Development Group    |
| Microsoft SQL Server  | Microsoft                              |
| Oracle Database       | Oracle                                 |
| MariaDB               | MariaDB Corporation                    |

---

## 📦 NoSQL Databases
Flexible, schema-less databases designed for scalability and handling unstructured or semi-structured data.

| Tool               | Type          | Company                         |
|--------------------|---------------|----------------------------------|
| MongoDB            | Document      | MongoDB Inc.                     |
| Cassandra          | Wide-column   | Apache Software Foundation       |
| Couchbase          | Document      | Couchbase Inc.                   |
| DynamoDB           | Key-value     | Amazon Web Services (AWS)        |
| Redis              | Key-value     | Redis Ltd.                       |
| Neo4j              | Graph         | Neo4j Inc.                       |
| Amazon DocumentDB  | Document      | AWS                              |

---

## ⚡ In-Memory Caches
Used to store frequently accessed data in memory for ultra-fast retrieval, reducing load on databases.

| Tool                | Company               |
|---------------------|-----------------------|
| Redis               | Redis Ltd.            |
| Memcached           | Community-driven      |
| Hazelcast           | Hazelcast Inc.        |
| Amazon ElastiCache  | AWS                   |

---

## 📩 Messaging & Streaming Systems
Enable asynchronous communication between services and real-time data streaming for event-driven architectures.

| Tool          | Type                     | Company                       |
|---------------|--------------------------|-------------------------------|
| RabbitMQ      | Message Queue            | VMware                        |
| Apache Kafka  | Distributed Streaming    | Apache Software Foundation    |
| Amazon SQS    | Message Queue            | AWS                           |
| Amazon SNS    | Pub/Sub                  | AWS                           |
| Google Pub/Sub| Pub/Sub                  | Google Cloud                  |
| NATS          | Lightweight Messaging    | Synadia                       |
| Apache Pulsar | Distributed Messaging    | Apache Software Foundation    |

---

## 🔍 Search Engines
Used for full-text search, indexing, and querying large datasets efficiently.

| Tool          | Company                       |
|---------------|-------------------------------|
| Elasticsearch | Elastic NV                     |
| Solr          | Apache Software Foundation     |
| OpenSearch    | AWS                            |

---

## 📊 Monitoring & Observability
Tools for tracking system health, performance metrics, logs, and alerts to ensure reliability and uptime.

| Tool       | Type       | Company           |
|------------|------------|-------------------|
| Prometheus | Metrics    | CNCF              |
| Grafana    | Dashboards | Grafana Labs      |
| Datadog    | Monitoring | Datadog Inc.      |
| New Relic  | Monitoring | New Relic Inc.    |
| Splunk     | Logs       | Splunk Inc.       |
| ELK Stack  | Logging    | Elastic NV        |

---

## ☁️ Cloud Platforms
Provide scalable infrastructure, storage, compute, and managed services for deploying applications.

| Platform               | Company    |
|------------------------|------------|
| AWS                    | Amazon     |
| Azure                  | Microsoft  |
| Google Cloud Platform  | Google     |
| IBM Cloud              | IBM        |
| Oracle Cloud           | Oracle     |

---

## 🧱 Containerization & Orchestration
Enable packaging applications into containers and managing them across distributed environments.

| Tool         | Type            | Company    |
|--------------|-----------------|------------|
| Docker       | Containerization| Docker Inc.|
| Kubernetes   | Orchestration   | CNCF       |
| Amazon ECS/EKS | Orchestration | AWS        |
| OpenShift    | Orchestration   | Red Hat    |

---

## 🔌 Communication Protocols
Facilitate efficient and structured communication between services, often used in microservices.

| Tool       | Type                       | Company         |
|------------|----------------------------|-----------------|
| gRPC       | Remote Procedure Call      | Google          |
| WebSocket  | Full-duplex Communication  | W3C & IETF      |
| HTTP/2     | Transport Protocol         | IETF            |

---

## 🧭 Coordination & Service Discovery
Used for managing distributed systems, service registration, configuration, and leader election.

| Tool               | Type                     | Company                   |
|--------------------|--------------------------|---------------------------|
| Apache ZooKeeper   | Distributed Coordination | Apache Software Foundation|
| etcd               | Key-value Store          | CNCF                      |
| Consul             | Service Discovery        | HashiCorp                 |

---



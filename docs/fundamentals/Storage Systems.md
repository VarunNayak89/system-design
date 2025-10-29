# Types of Storage

---

## 🔹 1. Block Storage

- **Definition:** Data is stored in fixed-size blocks, like sectors on a hard drive.  
- **Use Cases:** High-performance applications (databases, VMs, OS disks)  
- **Access Pattern:** Raw device-level access, fast read/write  
- **Examples:**
  - Amazon EBS (Elastic Block Store)
  - Google Persistent Disks
  - iSCSI, SAN  

✔️ *Think of it like a virtual hard drive.*

---

## 🔹 2. File Storage

- **Definition:** Data is stored as files in a hierarchical file system (folders/directories).  
- **Use Cases:** Shared file systems, logs, content management systems  
- **Access Pattern:** File-level operations (read, write, append)  
- **Examples:**
  - Amazon EFS (Elastic File System)
  - Google Filestore
  - NFS, SMB, CIFS  

✔️ *Think of it like a shared network drive.*

---

## 🔹 3. Object Storage

- **Definition:** Data is stored as objects (file + metadata + unique ID) in a flat namespace.  
- **Use Cases:** Media files, backups, logs, big data, user uploads  
- **Access Pattern:** HTTP-based (GET, PUT, DELETE)  
- **Examples:**
  - Amazon S3
  - Google Cloud Storage (GCS)
  - Azure Blob Storage  

✔️ *Think of it like a giant key-value store for files.*

---

## ✅ Comparison Table

| Feature | Block Storage | File Storage | Object Storage |
|----------|----------------|---------------|----------------|
| **Structure** | Raw blocks | Files in directories | Flat object system |
| **Protocol** | iSCSI, Fibre | NFS, SMB | HTTP/HTTPS |
| **Use Case** | Databases, VMs | Shared drives | Media, backups, web apps |
| **Performance** | High | Medium | Depends on size |
| **Scalability** | Medium | Medium | Very high |
| **Metadata Support** | Limited | Basic (file metadata) | Rich (custom tags) |

---

## 2️⃣ Cold vs Hot Storage

### 🔥 Hot Storage

- **Definition:** Frequently accessed data  
- **Characteristics:**
  - Low latency  
  - High performance  
  - Higher cost  
- **Examples:**
  - Active user data  
  - Database indexes  
  - Recent uploads  
- **Tech:** SSDs, in-memory cache (Redis), S3 Standard, GCS Standard  

---

### ❄️ Cold Storage

- **Definition:** Infrequently accessed data (archival)  
- **Characteristics:**
  - High latency (minutes to hours)  
  - Low cost  
  - Suitable for compliance, logs, backups  
- **Examples:**
  - Old logs or images  
  - Legal/compliance documents  
  - System backups  
- **Tech:** S3 Glacier, GCS Archive, Azure Archive, tape storage  

---

## 🧠 Interview Tip

> “For user-uploaded media like images or videos, I’d use object storage (S3/GCS) for scalability.  
> New files go to hot storage (S3 Standard), and after 30 days we transition them to cold storage (S3 Glacier) using lifecycle rules to reduce cost.”

---

## 🛠️ When to Choose What?

| Scenario | Best Option |
|-----------|--------------|
| High IOPS database (e.g., MySQL) | Block Storage (EBS) |
| Web app file uploads (images, docs) | Object Storage (S3) |
| Shared access by multiple servers | File Storage (EFS) |
| Compliance archive / backups | Cold Object Storage |
| Analytics on big logs | Object Storage (S3) + Athena or BigQuery |

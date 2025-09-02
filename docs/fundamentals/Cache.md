# 📘 Caching Patterns Summary

---

## 🔧 What is Caching?

Caching stores frequently accessed data in fast storage (like memory) to reduce latency and load on backend systems.

---

## 🧠 Key Concept: TTL (Time-To-Live)

- **TTL** defines how long a cached item stays valid.
- Helps manage memory and data freshness.
- Example in Redis (C#):
  ```csharp
  db.StringSet("key", "value", TimeSpan.FromMinutes(5));
## ⚙️ Caching Technologies
Technology	Purpose	Use Case
CDN	Caches static content at edge locations	Images, videos, CSS/JS
Redis	In-memory key-value store with rich types	Sessions, analytics, rate limiting
Memcached	Lightweight in-memory cache for strings	Query results, simple objects

## 📊 Caching Patterns Comparison
| Pattern         | Read Behavior                                                        | Write Behavior                                           | Cache Coverage                | Cache Update Timing  | Cache Logic Location   |
|----------------|----------------------------------------------------------------------|----------------------------------------------------------|-------------------------------|-----------------------|------------------------|
| Cache-Aside     | App reads from cache, loads from DB if miss & write in cache         | App writes directly to DB (cache not updated)            | Partial (hot data only)       | On read (lazy load)   | Application code       |
| Read-Through    | App reads from cache, cache loads from DB if miss & stores in cache  | App writes directly to DB (cache not updated)            | Partial or full               | On read (lazy load)   | Cache layer/service    |
| Write-Through   | App reads from cache (all data is in cache)                          | App writes to cache, cache writes to DB immediately      | Full (if all writes go through cache) | On write (sync)      | Cache layer/service    |
| Write-Behind    | App reads from cache (all data is in cache)                          | App writes to cache, cache writes to DB asynchronously   | Full (if all writes go through cache) | On write (async)     | Cache layer/service    |

## 🔹 Grouped by Behavior
🟦 Read-Focused Patterns
| Pattern       | Read Behavior                              | Cache Update Timing |
|---------------|---------------------------------------------|---------------------|
| Cache-Aside   | App checks cache, loads from DB if miss     | On read (lazy)      |
| Read-Through  | Cache handles read and DB fallback          | On read (lazy)      |


🟩 Write-Focused Patterns
| Pattern        | Write Behavior                                  | Cache Update Timing |
|----------------|--------------------------------------------------|---------------------|
| Write-Through  | App writes to cache, cache writes to DB          | On write (sync)     |
| Write-Behind   | App writes to cache, cache writes to DB later    | On write (async)    |

## 🧠 Strategy Tips
✅ Use Cache-Aside for flexible, partial caching.

✅ Use Read-Through for centralized cache logic.

✅ Use Write-Through for consistency.

✅ Use Write-Behind for high-performance writes.


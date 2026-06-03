Check diagram 1 with component
## Diagram 1

![System Design](./system%20Design.jpg)

CDN : Content Delivery Network, Keep user data close to user location 
ex Cloudflare, Amazon CloudFront, Akamai Technologies, Azure Front door Do CDN and global load balancing

Load Balancer : receives incoming requests and distributes them across multiple backend servers using a routing algorithm (such as round robin, least connections, or hashing) to improve availability, scalability, and performance. 

Cahce: store frequently accessed data,
ex, Redis, memcached

Primary DB and Read Replicas: keep write db and read db separate to distribute load in database

Message Queue : decouple systems and process work asynchronosly, queue store messages untill workers can process them
ex Azure service bus (as .net engineer most relevant answer), Azure Storage Queues, Google Pub/Sub and self hostages are RabbitMQ, Apache Kafka and ActiveMQ

Idempotency Key: ensure that repeated requests are processed only once, even if the client retries the request multiple times
Idempotency is typically implemented at the API layer using an Idempotency-Key header. We store processed keys and responses in Redis or a database so duplicate requests can be detected and the original response returned instead of executing the operation again


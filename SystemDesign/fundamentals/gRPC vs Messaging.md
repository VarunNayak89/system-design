# gRPC vs Messaging

- **gRPC** → synchronous request/response (fast function call over the network; HTTP/2 + Protobuf; supports streaming).
- **RabbitMQ / Pub/Sub** → asynchronous messaging (send-and-forget, queues/topics; consumers pick up later).

---

## How they differ

| Aspect          | gRPC (RPC over HTTP/2)                                         | RabbitMQ / Pub/Sub (Messaging)                                                           |
|-----------------|-----------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| Interaction     | **Sync** (client waits), also supports client/server streaming  | **Async** (producer doesn’t wait)                                                         |
| Typical pattern | Query/command (“do X now, return result”)                       | Events & tasks (“X happened”, “process this job”)                                         |
| Coupling        | Tighter (caller needs callee up & reachable)                    | Looser (decoupled via broker; producers/consumers evolve independently)                   |
| Backpressure    | Requires client/server flow control & limits                    | Queue naturally absorbs spikes (**load leveling**)                                        |
| Fan-out         | Manual (caller must call many services)                          | Built-in via topics/subscriptions (N→M delivery)                                          |
| Delivery        | Usually **at-most-once** unless you add retries/idempotency      | **At-least-once** (design for idempotency); optional ordering by key/partition; DLQs      |
| Latency         | Very low                                                         | Adds broker hop; great for non-urgent/async workloads                                      |
| State/Storage   | No message storage                                               | Durable queues/streams (retries, retention, **DLQs**)                                     |

---

## When to use which

### Use **gRPC** when
- You need an **immediate answer** (auth check, pricing, inventory read).
- **Low latency** and **strong schemas** (Protobuf) matter.
- You control both sides and can **version** contracts.

### Use **RabbitMQ / Pub/Sub** when
- You’re doing **event-driven** or **task processing** (send email, generate invoice, ETL).
- You need **fan-out**, **decoupling**, **retries**, **dead-letter queues**, or **load smoothing**.
- The consumer can **process later**; the caller **shouldn’t block**.

---

## Common hybrid (most real systems)

- **Command path** (user clicks “Pay”): `API → gRPC → Payment Service` (needs immediate result).
- **Side effects**: Payment service emits `PaymentSucceeded` → **Pub/Sub/RabbitMQ** → Notification, Ledger, Analytics consume independently.
- **Background jobs**: Image/video processing, report generation → queue worker via RabbitMQ.

![gRPC vs Messaging Diagram](../images/grpc-vs-messaging.png)

> **DLQ** = Dead-Letter Queue for messages that repeatedly fail processing.

---

## Quick rules of thumb

- “**Do this now and tell me if it worked**” → **gRPC**  
- “**This happened; whoever cares can react**” or “**process this later / retryable work**” → **Messaging**

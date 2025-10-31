# System Design Glossary

Keep these core terms at your fingertips when discussing distributed systems, reliability, and scaling trade-offs.

## Availability & Reliability
- **Availability:** Percentage of time a system is operational. Expressed in “nines” (e.g., 99.9% ⇒ ~8h45m downtime/year).
- **Reliability:** Probability a system performs correctly under stated conditions for a period. Often tied to mean time between failures (MTBF).
- **SLA / SLO / SLI:** Agreement, objective, and indicator describing expected performance and how it is measured.
- **Failover:** Automatic switching to a standby system upon failure (active-active vs active-passive).
- **Graceful Degradation:** System continues providing limited functionality under stress.

## Consistency Models
- **Strong Consistency:** Reads return the most recent write (linearizability). Often requires coordination and higher latency.
- **Eventual Consistency:** Data converges without guaranteeing immediate synchronization. Suitable for high availability.
- **Read-after-write Consistency:** A writer immediately sees its own write; others may observe delayed updates.
- **Consistency Spectrum:** CAP theorem (Consistency, Availability, Partition tolerance) and PACELC (If Partition, choose Availability or Consistency; Else, trade Latency vs Consistency).
- **Consensus Protocols:** Paxos, Raft, Zab—used to achieve agreement among distributed nodes.

## Latency & Throughput
- **Latency:** Time to complete a single request. Tail latency (p95/p99) reveals worst-case behavior.
- **Throughput:** Number of requests processed per unit time. Balanced via concurrency and resource utilization.
- **Backpressure:** Mechanism to slow producers when consumers are overwhelmed (e.g., queue limits, credit-based flow control).
- **Circuit Breaker:** Component that trips after failures to prevent cascading impact, allowing fallback or retries after cooldown.

## Queueing & Messaging
- **Message Queue:** Decouples producer and consumer via FIFO or topic-based delivery (e.g., RabbitMQ, SQS).
- **Stream Processing:** Append-only logs (Kafka, Kinesis) enabling ordered consumption and replay.
- **At-least-once vs Exactly-once:** Delivery guarantees; at-least-once requires idempotency, exactly-once is harder, often achieved via transactional semantics.
- **Dead Letter Queue (DLQ):** Holds messages that repeatedly fail processing for later inspection.

## Scaling & Partitioning
- **Horizontal Scaling:** Add more nodes (stateless services, sharded databases).
- **Vertical Scaling:** Increase resources of a single node (CPU, RAM); limited headroom.
- **Partitioning / Sharding:** Splitting data or workload across nodes based on key or range.
- **Rebalancing:** Moving load/data between partitions to maintain even distribution.

## Observability & Operations
- **Metrics:** Numeric time-series (request rate, error rate, latency).
- **Logs:** Structured/unstructured event records for debugging.
- **Tracing:** Follows a request through distributed services, capturing spans and timing.
- **Runbooks:** Step-by-step operational guides for incidents or routine tasks.

## Security & Networking
- **mTLS (Mutual TLS):** Both client and server present certificates for authentication.
- **Rate Limiting:** Control request rate via token bucket, leaky bucket, or fixed window.
- **Zero Trust:** Never trust, always verify; apply auth/authz at every boundary.
- **Service Mesh:** Infrastructure layer (e.g., Istio, Linkerd) providing traffic management, observability, and security for microservices.

## Cost & Efficiency
- **Load Shedding:** Intentionally dropping low-priority work during overload to protect core functionality.
- **Autoscaling:** Adjusting resources automatically based on metrics (CPU, QPS, custom).
- **Capacity Planning:** Forecasting resource needs; includes headroom policies and growth modeling.
- **Resource Utilization:** Measuring how efficiently CPU, memory, IO, and networking are used.

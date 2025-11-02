# System Design Refresher

Use this guide to frame architecture discussions quickly, explain trade-offs, and see how edge defense, load balancing, services, and data layers compose before diving into component-specific guides.

## Cheat Sheet
- Start with the north star: product goals, scale assumptions (traffic, data, latency, availability).
- Draw the high-level flow first (client → edge → application → data) before zooming into components.
- Discuss trade-offs using standard lenses: latency vs consistency, throughput vs cost, build vs buy.
- Name failure modes and mitigation strategies (replication, retries, backpressure, circuit breakers).

## Quick Refresh
- **Requirements:** Collect functional (features, reads vs writes) and non-functional (SLAs, compliance) constraints. Call out unknowns and suggest safe assumptions.
- **High-Level Architecture:** Describe entry points (CDN, DNS, API gateway), application layer (services, queues), and persistence (databases, caches, object stores).
- **Data Design:** Choose storage models (SQL, NoSQL, search) based on access patterns. Mention partitioning, replication, and schema evolution.
- **Scaling Patterns:** Explain horizontal vs vertical scaling, stateless services, autoscaling, and multi-region replication. Know when to leverage managed services.
- **Resiliency:** Cover health checks, load balancing, failover, backoff/retry policies, circuit breakers, and observability (metrics, traces, logs).
- **Security & Edge Defense:** Touch on auth/authz, secrets management, encryption, rate limiting, WAF/CDN-based DDoS protection, and API gateway concerns.

## Core Components

### Load Balancer
- Routes traffic across healthy backend instances; supports layer 4 (TCP) or layer 7 (HTTP) balancing.
- Implements health checks, stickiness, and traffic splitting for blue/green or canary deployments.
- Failure modes: unhealthy instance churn, uneven load distribution, single-region outages. Mitigations include cross-zone balancing and auto-scaling integrations.

### Edge Protection (CDN / WAF / DDoS Shield)
- CDN/WAF sits in front of load balancers to absorb volumetric attacks, cache static assets, and enforce threat rules.
- Integrates with DDoS scrubbing centers and rate limiting to drop malicious traffic before it hits the application tier.
- Coordinate logging and alerting to escalate when attack thresholds are exceeded; rehearse failover to alternate providers.

#### DDoS Mitigation Checklist
- Traffic inspection: enable WAF rules, bot detection, and anomaly scoring at the edge provider.
- Rate controls: configure global and per-client rate limits; propagate limits through API gateway policies.
- Scrubbing & failover: contract managed DDoS scrubbing service or multi-CDN strategy with automated failover.
- Network hardening: restrict direct access to load balancer IPs via ACLs/security groups; expose only via edge layer.
- Runbooks & drills: maintain step-by-step response plans and rehearse load tests/attack simulations with stakeholders.

### API Gateway
- Central entry point for client requests; handles routing, authentication, rate limiting, and request transformation.
- Enables versioning, monetization, and observability across microservices.
- Thin vs rich gateways: decide how much business logic to embed to avoid new bottlenecks.

### Caching Layer
- Reduce latency and offload primary stores with CDN edge caches, application caches (Redis/Memcached), and database caches.
- Define TTL, eviction policies, and cache invalidation strategies (write-through, write-behind, cache-aside).
- Plan for consistency: eventual consistency may be acceptable; invalidate on writes or changes in upstream data.

### Data Storage & Sharding
- Select storage engines to match workload (transactional, analytical, blob, search).
- Partition data via range, hash, or geo sharding; manage hot partitions and rebalancing.
- Combine replication (for availability) with sharding (for scale) and describe monitoring for lag or split-brain scenarios.

## Practice Drills
- Pick a familiar product (news feed, ride sharing, e-commerce checkout) and sketch the architecture in three layers: ingress, services, data.
- Time-box 15-minute designs: 5 minutes requirements, 5 minutes architecture, 5 minutes deep dive on a component or trade-off.
- Practice “what if” pivots: sudden traffic spikes, data deletion requests, region outages, third-party dependency failures.

## Deep Dive Later
- Explore managed offerings (AWS ALB, API Gateway, CloudFront, DynamoDB, RDS, GCP equivalents) and their limitations.
- Study real-world postmortems to sharpen failure analysis stories.
- Maintain glossaries for consistency models (strong, eventual, causal) and messaging patterns (queues vs streams).

## Diagram Ideas
- High-level architecture: clients → CDN/WAF → load balancer → services → databases/queues/cache.
- Sequence diagram for read/write paths highlighting consistency and caching touchpoints.
- Failure game plan: visualizing circuit breaker, retry, and fallback interactions during an outage.

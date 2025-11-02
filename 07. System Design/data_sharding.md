# Data Sharding & Storage Tiering Deep Dive

Explain how to split and replicate data intelligently to meet growth, latency, and isolation goals.

## Cheat Sheet
- **Why shard?** Horizontal scale, lower per-node load, regional latency optimization, tenant isolation.
- **Core decisions:** Shard key choice, partitioning strategy, replication model, rebalancing plan.
- **Common pitfalls:** Hot partitions, uneven growth, cross-shard joins, complex transactions, operational overhead.
- **Interview hook:** Share a migration story or incident involving shard rebalancing or tenant isolation.

## Quick Refresh
- **Partitioning Strategies:** Range, hash, list, composite, directory-based. Mention pros/cons for each.
- **Replication:** Pair sharding with master/replica, leaderless, or quorum-based models to balance availability and consistency.
- **Routing:** Application-layer lookup, middleware (shard map), proxy services (e.g., Vitess, Citus).
- **Metadata:** Maintain consistent shard metadata and automate updates during scaling.
- **Cross-Shard Operations:** Avoid when possible; use scatter-gather queries or analytic pipelines when necessary.
- **Multi-Tenancy:** Decide between shared, pooled, or dedicated shards per tenant. Mention noisy neighbor concerns and data residency requirements.

## Partitioning Patterns & Trade-Offs

### Range Sharding
- **How it works:** Partition data by ordered key ranges (e.g., user ID ranges, timestamps).
- **Pros:** Efficient range scans, locality-aware caching, good for time-series.
- **Cons:** Hot spots when recent writes concentrate in one range; requires periodic split or rotation.
- **Mitigation:** Pre-split ranges, rotate active shards, combine with hash on high-cardinality attributes.

### Hash Sharding
- **How it works:** Apply hash function to key and distribute uniformly.
- **Pros:** Even distribution for random access workloads, simple to scale with consistent hashing.
- **Cons:** Poor range query support, harder to co-locate related data.
- **Mitigation:** Use consistent hashing rings, virtual nodes to ease rebalancing.

### Directory / Lookup Sharding
- **How it works:** Maintain a routing table mapping keys/tenants to shards.
- **Pros:** Flexibility to place large tenants or special workloads on dedicated shards.
- **Cons:** Metadata service becomes critical dependency; requires strong consistency and failover.
- **Mitigation:** Replicate directory, cache lookups with TTL, log changes for recovery.

### Geo/Regional Sharding
- **How it works:** Route users to regional shards (e.g., EU vs US data centers) for compliance and latency.
- **Pros:** Data residency compliance, lower latency within region.
- **Cons:** Cross-region coordination for global features, failover complexity.
- **Mitigation:** Pair with global service mesh, asynchronous replication, or multi-master setups with conflict resolution.

## Rebalancing & Growth
- **Capacity Planning:** Monitor shard size, QPS, and storage growth. Set thresholds for split/merge operations.
- **Automated Rebalancing:** Implement tools to migrate data gradually (bulk copy + dual writes + cutover). Consider Vitess, Citus, Spanner-style automation.
- **Dual Writes & Backfill:** Plan for consistency during migration — copy data, replay binlogs/CDC, verify via checksums.
- **Tenant Moves:** For SaaS, support moving a tenant between shards with minimal downtime; communicate maintenance windows.

## Isolation & Consistency
- **Transactions:** Cross-shard transactions are expensive. Use two-phase commit sparingly or design to avoid them.
- **Joins:** Denormalize or precompute aggregates; use analytical systems for cross-shard queries.
- **Backups & DR:** Coordinate backups per shard; ensure consistent points in time across replicas.
- **Security:** Separate encryption keys per shard, enforce access controls for compliance (HIPAA, GDPR).

## Storage Tiering
- **Hot vs Cold Data:** Keep hot data in primary shards, move cold/archival data to cheaper stores (S3 + query engines).
- **Hybrid Approaches:** Serve latest data from OLTP shards, historical from OLAP warehouse; combine in APIs via summary tables or asynchronous aggregation.
- **Lifecycle Policies:** Automate TTL-based movement, compaction, or deletion to control storage costs.

## Example Anecdotes
- **Shard exhaustion:** User ID hash caused a single large customer to overload one shard. Adopted virtual nodes and tenant-aware routing.
- **Regional expansion:** Launching in EU required separate shard for GDPR; built async pipeline for cross-region analytics.
- **Dual-write migration:** Moving from single database to sharded cluster involved CDC stream, replaying backlog, and carefully orchestrated cutover.
- **Resharding incident:** Manual resharding caused data drift; postmortem drove automated tooling with validation and traffic throttling.

## Interview Prompts
- How would you shard a fast-growing multi-tenant SaaS product? Which key would you choose and why?
- What happens when a shard becomes a hot spot, and how do you mitigate it?
- Describe a zero-downtime approach to migrating data to new shards.
- How do you handle global reporting requirements when data lives in multiple regional shards?

## Deep Dive Later
- Explore sharding frameworks (Vitess for MySQL, Citus for PostgreSQL, Cosmos DB, DynamoDB global tables).
- Study Spanner/CockroachDB for globally-distributed consistency models.
- Prototype shard-aware services with consistent hashing libraries or proxy layers to build intuition.

## Diagram Ideas
- Shard map diagram: client → router → shard nodes with replication pairs.
- Timeline of resharding: copy, dual writes, validation, cutover.
- Multi-tenant layout: dedicated shards vs pooled shards highlighting noisy neighbor isolation.

### Diagram Prep Notes
1. Shard map: list shard IDs, primary/replica roles, and routing metadata service.
2. Resharding timeline: capture phases (split, dual write, verification, cutover) with duration estimates.

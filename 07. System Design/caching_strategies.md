# Caching Strategies Deep Dive

Explain how caches cut latency and load, manage consistency, and align with product goals.

## Cheat Sheet
- **Why cache?** Reduce latency, absorb traffic spikes, protect downstream systems, and cut costs.
- **Layers:** CDN/edge, application cache, database cache, client cache.
- **Patterns:** Cache-aside, write-through, write-behind, read-through, refresh-ahead.
- **Pitfalls:** Stale data, thundering herds, cache stampedes, eviction storms.

## Quick Refresh
- **Cache Selection:** Match technology to access pattern (CDN for static assets, Redis/Memcached for key-value, local memory cache for single-node).
- **TTL & Eviction:** Set time-to-live based on freshness needs. Understand LRU, LFU, FIFO. Plan for manual invalidation when TTL is too long.
- **Consistency:** Choose between eventual consistency (cheap, widely used) and strong consistency (complex, often slower). Mention read repair or write fences for critical paths.
- **Compression & Serialization:** Minimize payload size; weigh CPU cost vs bandwidth savings.
- **Security:** Avoid caching PII in shared layers. Use cache keys that don’t leak sensitive information.

## Patterns & Trade-Offs

### Cache-Aside (Lazy Loading)
- Application checks cache first; on miss, fetches from source and populates cache.
- **Pros:** Simple, avoids stale writes, works with any datastore.
- **Cons:** Stampedes on cold start or popular keys; mitigate with locking, request coalescing, or jittered TTLs.

### Write-Through
- Application writes to cache and datastore synchronously.
- **Pros:** Cache stays warm; good for read-heavy workloads.
- **Cons:** Adds write latency; failed cache write can complicate error handling.

### Write-Behind (Write-Back)
- Application writes to cache, then asynchronously persists to datastore.
- **Pros:** Absorbs bursts, reduces write amplification.
- **Cons:** Risk of data loss on cache failure; requires durable queues or logs.

### Read-Through
- Cache layer managed by library/proxy; app always calls cache, which fetches on miss.
- **Pros:** Centralized logic, consistent behavior.
- **Cons:** Less control; vendor lock-in or complex frameworks.

### Refresh-Ahead / Prewarming
- Automatically refresh hot keys before they expire.
- **Pros:** Smooths latency for known hotspots.
- **Cons:** Risk of fetching unused keys; need heuristics or ML-based predictions.

## Operational Considerations
- **Cache Stampede Mitigation:** Use request coalescing, mutex locks, probabilistic early expiration (e.g., dogpile prevention), or tiered caching.
- **Monitoring:** Track hit rate, eviction rate, latency, resource usage. Alert on sudden drops in hit rate or surge in evictions.
- **Scaling:** Partition caches by consistent hashing; manage rebalancing carefully to avoid widespread cache misses.
- **Failure Modes:** Plan for cache cluster outages — fallback to graceful degradation, precomputed responses, or traffic shaping.

## Example Anecdotes
- **Launch day:** CDN cached static assets, reducing origin load by 90%; missed cache invalidation caused stale hero image — scripted invalidation and added monitoring.
- **Cache stampede:** Viral content caused DB overload after cache eviction. Added jittered TTL and single-flight locking to prevent duplicate fetches.
- **Price updates:** Financial app required strong consistency; used write-through caches with short TTL and per-key invalidation hooks.
- **Session caching:** Redis outage invalidated user sessions. Lesson: combine sticky sessions with durable stores or multi-region cache replication.

## Interview Prompts
- How would you cache a frequently read but occasionally updated resource? Discuss invalidation and latency expectations.
- Describe handling a cache miss storm after deploying globally.
- Explain why caching user-specific data differs from caching canonical reference data.
- Outline how you’d monitor cache effectiveness and detect regressions.

## Deep Dive Later
- Experiment with Redis features (Lua scripting, Redis Cluster, streams) or Memcached deployment.
- Study CDN configurations (CloudFront, Fastly, Akamai) for edge cases like signed URLs and private content.
- Build a simulation of cache hit/miss patterns using traffic traces to explain cost savings and trade-offs.

## Diagram Ideas
- Layered cache stack: client cache, CDN, application cache, database cache with arrows showing miss/hit flow.
- Sequence diagram for cache-aside: request → cache miss → database → cache populate → response.
- Heat map concept: shard/partition load before and after caching to illustrate hit-rate impact.

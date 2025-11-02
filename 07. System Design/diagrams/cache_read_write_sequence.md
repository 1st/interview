# Cache Read/Write Flow (Cache-Aside)

```mermaid
sequenceDiagram
    participant C as Client
    participant G as API Gateway
    participant S as Service
    participant K as Cache
    participant D as Database

    C->>G: 1. HTTP Request (product detail)
    G->>S: Forward request (auth context)
    S->>K: Check cache (GET product:123)
    alt Cache Hit
        K-->>S: Cached payload
        S-->>C: Response (from cache)
    else Cache Miss
        K-->>S: Miss
        S->>D: Query product 123
        D-->>S: Product record
        S->>K: Populate cache with TTL (write)
        note right of K: TTL = 5 min<br/>Tags = product:123
        S-->>C: Response (fresh)
    end
    opt Invalidations
        S->>K: Delete/Update cache on product change
    end
```

**Key Points**
- Cache miss triggers database read and cache populate with TTL.
- Optional invalidation step ensures updates propagate (e.g., on write path/event).
- Mention TTL and tagging strategy during interviews; highlight idempotent writes.

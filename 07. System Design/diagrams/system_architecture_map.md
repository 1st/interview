# System Design Architecture Map (Draft)

```mermaid
graph LR
    subgraph Clients
        A[Web Client]
        B[Mobile Client]
        C[Partner Integration]
    end
    A -->|HTTPS| D[DNS]
    B -->|HTTPS| D
    C -->|HTTPS| D
    D --> E[CDN / WAF / DDoS Shield]
    E -->|Cached assets| A
    E --> F[Regional Load Balancer]
    subgraph Services
        G[API Gateway
(Auth, Rate Limiting, Logging)]
        H[Service A]
        I[Service B]
        J[Service C]
    end
    F --> G
    G --> H
    G --> I
    G --> J
    H --> K[(Cache Layer)]
    I --> K
    J --> L[(Message Queue / Stream)]
    K --> M[(Databases / Object Storage)]
    I --> M
    J --> M
    L --> I
    subgraph Observability
        N[Metrics]
        O[Logs]
        P[Traces]
    end
    H --> N
    I --> N
    J --> N
    H --> O
    I --> O
    J --> O
    H --> P
    I --> P
    J --> P
    N --> Q[Ops Dashboards]
    O --> Q
    P --> Q
```

**Notes**
- Edge layer (CDN/WAF) absorbs DDoS traffic and serves static assets; sanitized traffic flows to load balancers.
- API gateway enforces authentication and rate limiting before routing to services.
- Services interact with cache, message queues, and data stores while emitting observability data.

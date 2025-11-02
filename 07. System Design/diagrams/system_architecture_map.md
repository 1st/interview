# System Design Architecture Map (Draft)

```mermaid
graph TD
    subgraph Clients
        A[Web Client]
        B[Mobile Client]
        C[Partner Integration]
    end
    subgraph Edge
        D[DNS]
        E[CDN / WAF / DDoS Shield]
    end
    subgraph Ingress
        F[Regional Load Balancer]
        G[API Gateway: Auth, Rate Limiting, Logging]
    end
    subgraph Services
        H[Service A]
        I[Service B]
        J[Service C]
    end
    subgraph Data & Messaging
        K[(Cache Layer)]
        L[(Message Queue / Stream)]
        M[(Databases / Object Storage)]
    end
    subgraph Observability
        N[Metrics]
        O[Logs]
        P[Traces]
    end

    A -->|HTTPS| D
    B -->|HTTPS| D
    C -->|HTTPS| D
    D --> E
    E -->|Sanitized traffic| F
    F --> G
    G --> H
    G --> I
    G --> J

    H --> K
    I --> K
    J --> L
    K --> M
    I --> M
    J --> M
    L --> I

    H --> N
    H --> O
    H --> P
    I --> N
    I --> O
    I --> P
    J --> N
    J --> O
    J --> P

    N --> Q[Ops Dashboards]
    O --> Q
    P --> Q
```

**Notes**
- Edge layer (CDN/WAF) absorbs DDoS traffic and serves static assets; sanitized traffic flows to load balancers.
- API gateway enforces authentication and rate limiting before routing to services.
- Services interact with cache, message queues, and data stores while emitting observability data.

# System Design Architecture Map

```mermaid
graph TB
    classDef sync fill:#e3f2fd,stroke:#1565c0,color:#0d47a1;
    classDef async fill:#fff3e0,stroke:#ef6c00,color:#bf360c;
    classDef data fill:#f1f8e9,stroke:#33691e,color:#1b5e20;

    subgraph Clients
        A[Web Client]
        B[Mobile Client]
        C[Partner Integration]
    end
    subgraph Edge
        D[DNS]
        E[CDN / WAF]
    end
    subgraph Ingress
        F[Load Balancer]
        G[API Gateway]
    end
    subgraph Services
        H[Service A]
        I[Service B]
        J[Service C]
    end
    subgraph Data
        K[(Cache)]
        L[(Database)]
        M[(Queue)]
    end
    subgraph Observability
        N[Metrics]
        O[Logs]
        P[Traces]
    end
    Q[Ops Dashboards]

    A --> D
    B --> D
    C --> D
    D --> E
    E --> F
    F --> G
    G --> H
    G --> I
    G --> J

    H --> K
    I --> K
    H --> L
    I --> L
    J --> M
    M --> I

    H --> N
    H --> O
    H --> P
    I --> N
    I --> O
    I --> P
    J --> N
    J --> O
    J --> P

    N --> Q
    O --> Q
    P --> Q

    class H,I sync;
    class J async;
    class K,L,M data;
```

**Legend**
- Sync Service: Service A / Service B
- Async Service: Service C (Queue)
- Data Stores: Cache, Database, Queue
- Observability: Metrics, Logs, Traces feeding Ops dashboards

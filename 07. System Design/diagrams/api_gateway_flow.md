# API Gateway Request Flow

```mermaid
graph TD
    classDef edge fill:#e3f2fd,stroke:#1565c0,color:#0d47a1;
    classDef gateway fill:#ede7f6,stroke:#512da8,color:#311b92;
    classDef service fill:#fff3e0,stroke:#ef6c00,color:#bf360c;
    classDef data fill:#f1f8e9,stroke:#33691e,color:#1b5e20;
    classDef observability fill:#fbe9e7,stroke:#d84315,color:#bf360c;

    Client[Client] --> Edge[CDN / WAF]
    Edge --> Gateway[API Gateway]
    Gateway -->|Auth validation| AuthProvider[Auth Provider]
    Gateway -->|Rate limit| QuotaStore[Quota Store]
    Gateway --> Router{Routing Rules}
    Router --> ServiceA[Service A]
    Router --> ServiceB[Service B]
    Router --> BFF[Mobile BFF Service]
    BFF --> ServiceC[Service C]
    ServiceA --> CacheDB[(Cache / Database)]
    ServiceB --> QueueStore[(Queue / Database)]
    ServiceC --> ServiceDB[(Database)]
    Gateway --> Observability[Metrics / Logs / Traces]
    Observability --> OpsDash[Ops Dashboards]

    class Client,Edge edge;
    class Gateway,Router gateway;
    class AuthProvider,BFF,ServiceA,ServiceB,ServiceC service;
    class QuotaStore,CacheDB,QueueStore,ServiceDB data;
    class Observability,OpsDash observability;
```

**Notes**
- Edge layer shields against DDoS/threats before the gateway.
- Gateway handles authentication, rate limiting, and routing.
- Mobile BFF tailors responses for mobile clients.
- Observability pipeline catches metrics/logs/traces for dashboards.

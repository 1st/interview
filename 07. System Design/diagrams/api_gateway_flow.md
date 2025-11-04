# API Gateway Request Flow

```mermaid
graph TD
    classDef node fill:#e8f5e9,stroke:#2e7d32,color:#1b5e20;

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
```

**Notes**
- Edge layer shields against DDoS/threats before the gateway.
- Gateway handles authentication, rate limiting, and routing.
- Mobile BFF tailors responses for mobile clients.
- Observability pipeline catches metrics/logs/traces for dashboards.

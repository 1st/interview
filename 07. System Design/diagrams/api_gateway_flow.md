# API Gateway Request Flow

```mermaid
graph TD
    Client[Client] --> Edge[CDN / WAF]
    Edge --> Gateway[API Gateway]
    Gateway -->|Auth / JWT validation| AuthService[Auth Provider]
    Gateway -->|Rate limit check| QuotaService[Quota Store]
    Gateway --> Router{Routing Rules}
    Router --> ServiceA[Service A (REST)]
    Router --> ServiceB[Service B (gRPC)]
    Router --> BFF[Mobile BFF]
    BFF --> ServiceC[Service C]
    ServiceA --> DB1[(DB / Cache)]
    ServiceB --> DB2[(Message Queue / Stream)]
    ServiceC --> DB3[(Database)]
    Gateway --> Observability[Metrics / Logs / Traces]
    Observability --> Ops[Ops Dashboards]
```

**Notes**
- Edge layer (CDN/WAF) handles DDoS and basic threat detection before the gateway.
- Gateway enforces auth and rate limits, then routes based on path/version/client.
- Observability hooks capture metrics/logs/traces for downstream analysis.
```

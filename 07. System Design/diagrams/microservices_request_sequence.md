# Microservices Request Journey

```mermaid
sequenceDiagram
    participant Client
    participant Gateway as API Gateway
    participant BFF as Mobile BFF Service
    participant ServiceA as Service A
    participant ServiceB as Service B
    participant EventBus as Event Bus
    participant Inventory as Inventory Service
    participant Metrics as Observability

    Client->>Gateway: HTTPS Request (Place order)
    Gateway->>BFF: Forward request with auth context
    BFF->>ServiceA: Validate request & orchestrate
    ServiceA->>Metrics: Emit trace span
    ServiceA->>Inventory: Check stock
    Inventory-->>ServiceA: Stock status
    ServiceA->>ServiceB: Charge payment (REST)
    ServiceB-->>ServiceA: Payment result
    ServiceA->>EventBus: Publish OrderCreated event
    EventBus->>Inventory: Async reserve stock
    EventBus->>Metrics: Emit event metrics
    ServiceA-->>BFF: Order response
    BFF-->>Client: Success (order id)
```

**Notes**
- Sequence mixes synchronous calls with async events; highlight tracing spans and metrics.
- Mention saga/compensation logic if payment or inventory fails.

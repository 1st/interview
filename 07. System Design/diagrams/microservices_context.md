# Microservices Context Map

```mermaid
graph TB
    subgraph Shared Infrastructure
        Gateway[API Gateway]
        Discovery[Service Discovery]
        Observability[Observability Stack]
    end

    subgraph Catalog Context
        CatalogService[Catalog Service]
        InventoryService[Inventory Service]
        PricingService[Pricing Service]
        CatalogDB[(Catalog DB)]
    end

    subgraph Orders Context
        OrderService[Order Service]
        PaymentService[Payment Service]
        ShippingService[Shipping Service]
        OrderDB[(Order DB)]
    end

    subgraph Users Context
        AuthService[Auth Service]
        ProfileService[Profile Service]
        UserDB[(User DB)]
    end

    Gateway --> CatalogService
    Gateway --> OrderService
    Gateway --> AuthService

    CatalogService --> Discovery
    OrderService --> Discovery
    AuthService --> Discovery

    CatalogService --> Observability
    OrderService --> Observability
    AuthService --> Observability

    CatalogService --> CatalogDB
    InventoryService --> CatalogDB
    PricingService --> CatalogDB

    OrderService --> OrderDB
    PaymentService --> OrderDB
    ShippingService --> OrderDB

    AuthService --> UserDB
    ProfileService --> UserDB
```

**Notes**
- Shared infrastructure provides gateway, discovery, and observability for bounded contexts.
- Each context owns its data store; additional services follow the same pattern (not shown).
- Highlight ownership boundaries and shared dependencies during interviews.

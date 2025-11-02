# Microservices Context Map

```mermaid
graph TD
    subgraph Shared Infrastructure
        Gateway[API Gateway]
        Discovery[Service Discovery]
        Observability[Observability Stack]
    end

    subgraph Catalog
        CatalogSvc[Catalog Service]
        InventorySvc[Inventory Service]
        PricingSvc[Pricing Service]
    end

    subgraph Orders
        OrderSvc[Order Service]
        PaymentSvc[Payment Service]
        ShippingSvc[Shipping Service]
    end

    subgraph Users
        AuthSvc[Auth Service]
        ProfileSvc[Profile Service]
    end

    Gateway --> CatalogSvc
    Gateway --> OrderSvc
    Gateway --> AuthSvc

    CatalogSvc --> Discovery
    OrderSvc --> Discovery
    AuthSvc --> Discovery

    CatalogSvc --> Observability
    InventorySvc --> Observability
    PricingSvc --> Observability
    OrderSvc --> Observability
    PaymentSvc --> Observability
    ShippingSvc --> Observability
    AuthSvc --> Observability
    ProfileSvc --> Observability

    CatalogSvc --> InventorySvc
    CatalogSvc --> PricingSvc
    OrderSvc --> PaymentSvc
    OrderSvc --> ShippingSvc
    OrderSvc --> InventorySvc
    PaymentSvc --> AuthSvc
    ProfileSvc --> AuthSvc

    subgraph Data Stores
        CatalogDB[(Catalog DB)]
        OrderDB[(Order DB)]
        UserDB[(User DB)]
    end

    CatalogSvc --> CatalogDB
    InventorySvc --> CatalogDB
    OrderSvc --> OrderDB
    PaymentSvc --> OrderDB
    ShippingSvc --> OrderDB
    AuthSvc --> UserDB
    ProfileSvc --> UserDB
```

**Notes**
- Shared infrastructure provides gateway, discovery, and observability for bounded contexts.
- Each bounded context (Catalog, Orders, Users) owns its data store; services communicate via APIs.
- Highlight ownership boundaries and shared dependencies during interviews.

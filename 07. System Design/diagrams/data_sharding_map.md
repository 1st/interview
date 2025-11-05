# Data Sharding Topology

```mermaid
graph TD
    classDef router fill:#e3f2fd,stroke:#1565c0,color:#0d47a1;
    classDef primary fill:#fff3e0,stroke:#ef6c00,color:#bf360c;
    classDef replica fill:#f1f8e9,stroke:#33691e,color:#1b5e20;
    classDef observability fill:#fbe9e7,stroke:#d84315,color:#bf360c;
    classDef metadata fill:#ede7f6,stroke:#512da8,color:#311b92;
    classDef upstream fill:#e8f5e9,stroke:#2e7d32,color:#1b5e20;

    ClientService[Upstream Service] --> Router[Shard Router / Metadata Service]
    Router -->|Tenant A| ShardAPrimary[Shard A Primary]
    Router -->|Tenant B| ShardBPrimary[Shard B Primary]
    Router -->|Tenant C| ShardCPrimary[Shard C Primary]

    ShardAPrimary --> ShardAReplica[Shard A Replica] --- Note["Replication async (latency < 200ms)."]
    ShardBPrimary --> ShardBReplica[Shard B Replica]
    ShardCPrimary --> ShardCReplica[Shard C Replica]

    ShardAPrimary --> MonitoringA[Metrics / Logs]
    ShardBPrimary --> MonitoringB[Metrics / Logs]
    ShardCPrimary --> MonitoringC[Metrics / Logs]

    Router --> Metadata[(Shard Map / Config)]
    Metadata --> Router

    subgraph Rebalancing
        direction TB
        NewShard[Shard D Primary]
        Router -. move tenant .-> NewShard
        ShardAPrimary -. migrate data .-> NewShard
    end

    class ClientService upstream;
    class Router router;
    class ShardAPrimary,ShardBPrimary,ShardCPrimary,NewShard primary;
    class ShardAReplica,ShardBReplica,ShardCReplica replica;
    class MonitoringA,MonitoringB,MonitoringC observability;
    class Metadata metadata;
```

**Notes**
- Router consults shard map to send tenants to the correct primary.
- Each shard has primaries and replicas for HA; monitoring feeds are shown for observability.
- Rebalancing adds new shard and migrates tenant/data gradually; mention latency impact of async replication.

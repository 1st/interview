# Data Sharding Topology

```mermaid
graph TD
    Client[Service] --> Router[Shard Router / Metadata Service]
    Router -->|Tenant A| ShardAPrimary[Shard A Primary]
    Router -->|Tenant B| ShardBPrimary[Shard B Primary]
    Router -->|Tenant C| ShardCPrimary[Shard C Primary]

    ShardAPrimary --> ShardAReplica[Shard A Replica]
    ShardBPrimary --> ShardBReplica[Shard B Replica]
    ShardCPrimary --> ShardCReplica[Shard C Replica]

    ShardAPrimary --> MonitoringA[Metrics/Logs]
    ShardBPrimary --> MonitoringB[Metrics/Logs]
    ShardCPrimary --> MonitoringC[Metrics/Logs]

    Router --> Metadata[(Shard Map / Config)]
    Metadata --> Router

    subgraph Rebalancing
        NewShard[Shard D Primary]
        Router -. move tenant .-> NewShard
        ShardAPrimary -. migrate data .-> NewShard
    end
```

**Notes**
- Router consults shard map to send tenants to the correct primary.
- Each shard has primaries and replicas for HA; monitoring feeds are shown for observability.
- Rebalancing adds new shard and migrates tenant/data gradually.
```

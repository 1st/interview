# Kubernetes Cluster Architecture

```mermaid
graph TB
    Clients[kubectl / CI Pipelines]
    Clients -->|REST| APIServer[API Server]

    subgraph Control Plane
        APIServer
        Controller[Controller Manager]
        Scheduler
        Etcd[(etcd)]
    end

    APIServer --> Controller
    APIServer --> Scheduler
    APIServer --> Etcd

    subgraph Worker Node
        Kubelet[Kubelet]
        KubeProxy[Kube-proxy]
        PodA[Pod A]
        PodB[Pod B]
        PodC[Pod C]
    end

    Controller --> Kubelet
    Scheduler --> PodA
    Scheduler --> PodB
    Scheduler --> PodC

    Kubelet --> PodA
    Kubelet --> PodB
    Kubelet --> PodC

    subgraph Networking
        Ingress[Ingress Controller]
        Service[Service - ClusterIP/LoadBalancer]
        CNI[CNI Plugin]
    end

    Ingress --> Service
    Service --> PodA
    Service --> PodB
    Service --> PodC
    CNI --> PodA
    CNI --> PodB
    CNI --> PodC
```

**Notes**
- Control plane components manage desired state; workers (one shown, replicated as needed) run kubelet/kube-proxy and host pods.
- Ingress and Services expose workloads; CNI provides pod networking.
- External clients interact via `kubectl`/CI hitting the API server.

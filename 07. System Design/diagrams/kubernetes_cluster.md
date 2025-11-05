# Kubernetes Cluster Architecture

```mermaid
graph TB
    classDef client fill:#e3f2fd,stroke:#1565c0,color:#0d47a1;
    classDef control fill:#ede7f6,stroke:#512da8,color:#311b92;
    classDef worker fill:#fff3e0,stroke:#ef6c00,color:#bf360c;
    classDef network fill:#f1f8e9,stroke:#33691e,color:#1b5e20;

    Clients[kubectl / CI Pipelines] -->|REST| APIServer[API Server]

    subgraph ControlPlane[Control Plane]
        direction TB
        APIServer
        Controller[Controller Manager]
        Scheduler
        Etcd[(etcd)]
    end

    APIServer --> Controller
    APIServer --> Scheduler
    APIServer --> Etcd

    subgraph WorkerNodes[Worker Nodes (representative)]
        direction TB
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

    subgraph Networking[Networking]
        direction TB
        Ingress[Ingress Controller]
        Service[Service (ClusterIP/LoadBalancer)]
        CNI[CNI Plugin]
    end

    Ingress --> Service
    Service --> PodA
    Service --> PodB
    Service --> PodC
    CNI <-->|Pod networking| PodA
    CNI <-->|Pod networking| PodB
    CNI <-->|Pod networking| PodC

    class Clients client;
    class APIServer,Controller,Scheduler,Etcd control;
    class Kubelet,KubeProxy,PodA,PodB,PodC worker;
    class Ingress,Service,CNI network;
```

**Notes**
- Control plane components manage desired state; worker nodes (others implied) run kubelet/kube-proxy and host pods.
- Ingress/Service expose workloads; CNI handles pod networking.
- External clients interact via `kubectl`/CI hitting the API server.

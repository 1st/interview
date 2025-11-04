# Kubernetes Cluster Architecture

```mermaid
graph TB
    Clients[kubectl / CI Pipelines] -->|REST| APIServer[API Server]

    subgraph ControlPlane[Control Plane]
        APIServer
        Controller[Controller Manager]
        Scheduler
        Etcd[(etcd)]
    end

    APIServer --> Controller
    APIServer --> Scheduler
    APIServer --> Etcd

    subgraph WorkerNodes[Worker Nodes (representative)]
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
```

**Notes**
- Control plane components manage desired state; worker nodes (others implied) run kubelet/kube-proxy and host pods.
- Ingress/Service expose workloads; CNI handles pod networking.
- External clients interact via `kubectl`/CI hitting the API server.

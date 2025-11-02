# Kubernetes Cluster Architecture

```mermaid
graph TD
    subgraph Control Plane
        APIServer[API Server]
        Controller[Controller Manager]
        Scheduler[Scheduler]
        Etcd[(etcd)]
    end

    subgraph Worker Nodes
        subgraph Node1[Worker Node]
            Kubelet1[Kubelet]
            Proxy1[Kube-proxy]
            Pod1[Pod A]
            Pod2[Pod B]
        end
        subgraph Node2[Worker Node]
            Kubelet2[Kubelet]
            Proxy2[Kube-proxy]
            Pod3[Pod C]
        end
    end

    ClientKubectl[kubectl / CI] -->|REST| APIServer
    APIServer --> Controller
    APIServer --> Scheduler
    APIServer --> Etcd

    Controller --> Kubelet1
    Controller --> Kubelet2
    Scheduler --> Pod1
    Scheduler --> Pod2
    Scheduler --> Pod3

    Kubelet1 --> Pod1
    Kubelet1 --> Pod2
    Kubelet2 --> Pod3

    subgraph Networking
        CNI[CNI Plugin]
        Service[Service - ClusterIP/LoadBalancer]
        Ingress[Ingress Controller]
    end

    CNI --> Pod1
    CNI --> Pod2
    CNI --> Pod3
    Ingress --> Service
    Service --> Pod1
    Service --> Pod2
    Service --> Pod3
```

**Notes**
- Control plane components manage desired state; workers run kubelet/kube-proxy and host pods.
- CNI provides pod networking; services and ingress expose workloads.
- External clients interact via `kubectl`/CI pipelines hitting the API server.
```

# Kubernetes Operations Deep Dive

Refresh the essentials for deploying, scaling, and troubleshooting workloads on Kubernetes.

## Cheat Sheet
- **Core assets:** Pods, deployments, services, configmaps/secrets, ingress, statefulsets.
- **Control loop mindset:** Declarative desired state via API server, reconciled by controllers (deployments, HPA, kube-scheduler).
- **Interview hook:** Discuss an incident or migration involving Kubernetes rollout or cluster tuning.

## Quick Refresh
- **Cluster Architecture:** API server, etcd, controller manager, scheduler on control plane; kubelet, kube-proxy, CNI on worker nodes.
- **Workload Types:** Deployments for stateless apps, StatefulSets for ordered pods, DaemonSets for node agents, Jobs/CronJobs for batch; align choices with service boundaries discussed in [Microservices Architecture](microservices.md).
- **Networking:** ClusterIP, NodePort, LoadBalancer services; ingress controllers; CNI plugins (Calico, Cilium). Understand service discovery via DNS.
- **Config & Secrets:** Inject environment variables or volumes; manage rotation; leverage external secret stores when needed.
- **Scaling:** Horizontal Pod Autoscaler (metrics-based), Vertical Pod Autoscaler, Cluster Autoscaler. Know resource requests/limits and bin packing considerations.
- **Reliability:** Readiness/liveness/startup probes, rolling updates, PodDisruptionBudgets, PodTopologySpread.
- **Security:** RBAC, namespaces, network policies, PodSecurity (admission controllers), image scanning, runtime policies.
- **Observability:** Use kubectl, kubectl top, metrics-server, Prometheus/Grafana, logging stacks (ELK, Loki), tracing sidecars.

## Patterns & Trade-Offs
- **Multi-tenant Clusters:** Namespaces and resource quotas provide isolation; consider separate clusters for strict isolation or compliance.
- **Blue/Green & Canary Releases:** Leverage multiple deployments, service selectors, or progressive delivery tools (Argo Rollouts, Flagger).
- **Service Mesh Integration:** Envoy/Linkerd sidecars for mTLS, retries, traffic shaping; weigh added complexity.
- **Stateful Workloads:** Use StatefulSets with persistent volumes (CSI drivers). Consider operator patterns for databases.
- **Hybrid/Edge Deployments:** Manage clusters across cloud and on-prem with fleet managers (Anthos, EKS Anywhere, AKS Arc).

## Example Anecdotes
- **Cluster outage:** Misconfigured resource limits starved system pods; implementing resource requests and monitoring prevented recurrence.
- **Deploy rollback:** Failed rollout recovered via Deployment revision history and `kubectl rollout undo`.
- **Autoscaling surprise:** HPA oscillations due to bursty metrics; added custom metrics and stabilization windows.
- **Security audit:** RBAC gaps uncovered cross-namespace access; tightened roles, added network policies, and enabled OPA Gatekeeper.

## Interview Prompts
- How do you debug a pod stuck in CrashLoopBackOff? What commands do you run first?
- Explain how you would design CI/CD to deploy safely to Kubernetes across environments.
- Describe how you secure inter-service traffic and sensitive configuration inside a cluster.
- What indicators tell you it’s time to split clusters or adopt a platform team?

## Deep Dive Later
- Operators (Kubebuilder, Operator SDK) for custom lifecycle automation.
- GitOps workflows with Argo CD or Flux.
- Cluster autoscaling tunables and cost-optimization strategies.
- Chaos engineering on Kubernetes (LitmusChaos, PowerfulSeal).

## Diagram Ideas
- Control plane vs worker node architecture diagram.
- Deployment rollout timeline showing replicas, readiness probes, and service selector updates.
- Network flow: ingress → service → pod, highlighting CNI path and policies.

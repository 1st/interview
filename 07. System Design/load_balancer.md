# Load Balancer Deep Dive

Use this guide to explain load balancers quickly, cover common follow-up questions, and show awareness of real-world trade-offs.

## Cheat Sheet
- **Why it matters:** Evenly distribute traffic, tolerate instance failures, and provide a single entry point for clients.
- **Key knobs:** Layer 4 (TCP/UDP) vs Layer 7 (HTTP), health checks, stickiness, connection draining, traffic splitting.
- **Trade-offs:** Simplicity vs flexibility, latency overhead, stateful features vs stateless scaling.
- **Interview hook:** Describe one incident or migration where LB configuration saved or harmed reliability.

## Quick Refresh
- **Core function:** Accept client connections, select a healthy backend, and proxy the request/response.
- **Edge integration:** Assume upstream CDN/WAF handles DDoS scrubbing before traffic reaches the load balancer; ensure health checks and rate limits align across layers.
- **Algorithms:** Round-robin, least connections, weighted, IP hash, random with two choices. Know when each applies.
- **Health Monitoring:** TCP pings vs HTTP health endpoints; consider warmup time, circuit breaking, auto-removal.
- **Session Affinity:** Cookie-based or IP-based stickiness to support stateful backends; discuss downsides (hot spots, failover).
- **TLS Termination:** Offload cert management to the load balancer or re-encrypt to backend for end-to-end security.
- **Blue/Green & Canary:** Use weighted routing or header-based rules to shift traffic safely.

## Patterns & Trade-Offs

### Layer 4 vs Layer 7
- **Layer 4:** Faster, protocol-agnostic (TCP/UDP), minimal inspection. Ideal for raw throughput and non-HTTP protocols.
- **Layer 7:** Understands HTTP headers, paths, cookies. Enables routing by URL, A/B testing, auth integration.
- **Trade-off:** L7 adds latency and complexity but unlocks smarter routing and observability.

### Active vs Passive Health Checks
- **Active:** Periodic probes detect failures proactively; risk false positives if backend warmup is slow.
- **Passive:** Observe real traffic responses to mark backends unhealthy; slower to react but lower overhead.
- **Combine both** to balance sensitivity and stability.

### Horizontal vs Vertical Scaling
- **Horizontal:** Multiple load balancer instances behind DNS or anycast; remove single point of failure.
- **Vertical:** Beefier single appliance—simpler but risky. Prefer managed services (AWS ALB/NLB, GCP LB, nginx/HAProxy clusters).

### Global Traffic Management
- **DNS-based:** Geo or latency routing at the DNS layer; slower failover (TTL dependent).
- **Anycast:** Same IP advertised from multiple regions; requires resilient routing and consistent configs.
- **Hybrid:** DNS directs to regional LBs, which handle local distribution.

## Example Anecdotes
- **Canary gone wrong:** Weighted routing misconfigured, sending 50% traffic to a canary that needed 5%. Lesson: start with tiny percents and monitor closely.
- **Sticky sessions and outages:** Application relied on in-memory sessions; LB failover sent users to cold nodes, causing login loops. Solution: shared session store or stateless design.
- **TLS certificate expiration:** Centralized termination meant one missed renewal impacted entire service. Mitigation: automate renewals, add monitoring, or use managed certs.
- **Auto-scaling mismatch:** Load balancer health checks marked instances healthy before warmup, routing traffic too early. Fix: custom health endpoints that verify dependencies and caches.

## Interview Prompts
- Explain how you’d add a new service behind an existing load balancer (DNS updates, health checks, rollout).
- Contrast using a managed cloud LB vs running nginx/HAProxy yourself.
- Describe how you diagnose uneven load distribution across backends.
- Discuss how load balancing changes in a multi-region or hybrid-cloud design.

## Deep Dive Later
- Review vendor docs: AWS ALB/NLB, Google Cloud LB, Azure Front Door.
- Experiment with HAProxy or Envoy configs locally; practice weighted routing and health checks.
- Study SRE postmortems involving load balancing misconfigurations to gather storytelling ammo.

## Diagram Ideas
- Sequence diagram: client → DNS → load balancer → healthy backend with health-check feedback loop.
- Architecture sketch: cross-zone load balancers feeding auto-scaled instances, highlighting blue/green weights.
- Failure timeline: unhealthy node detection, removal, and reintegration after health checks pass.

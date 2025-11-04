# DDoS Response Playbook

A reusable checklist for preparing, detecting, and responding to distributed denial-of-service attacks in production environments.

## Preparation
- **Architecture:** Route all public traffic through CDN/WAF layers with automatic DDoS scrubbing; restrict direct access to origin/load balancer IPs.
- **Capacity Planning:** Understand baseline traffic (per region, per endpoint) and establish automated scaling limits for edge providers and origin infrastructure.
- **Controls:** Configure global and per-client rate limits in the API gateway; enable anomaly detection, bot filtering, and geo/IP reputation lists.
- **Runbooks & Ownership:** Document escalation paths, communication templates, and decision trees; assign an incident commander and supporting roles.
- **Testing:** Conduct load and chaos simulations, including failover to secondary CDN providers or scrubbing services; validate alerting thresholds.

## Detection
- **Monitoring:** Track sudden spikes in requests, connection attempts, or error rates; leverage dashboards for edge/provider metrics and origin health.
- **Alerting:** Trigger alerts on defined thresholds (e.g., 2× baseline RPS, elevated SYN packets, elevated 5xx). Include context about impacted edge POPs or regions.
- **Classification:** Determine attack type (volumetric, protocol, application-layer) by examining traffic signatures and comparing against historical patterns.

## Mitigation
- **Edge Actions:** Activate or tighten WAF/DDoS policies (challenge/deny), enable scrubbing centers, and apply geo/IP blocks or rate limiting. Reference vendor playbooks (AWS Shield Advanced, Cloudflare Magic Transit) for canned responses.
- **Gateway Controls:** Increase throttling, enforce stricter authentication challenges, or degrade non-essential endpoints/features. Disable high-cost endpoints temporarily.
- **Origin Hardening:** Scale out stateless services, shed low-priority workloads, and ensure backpressure (circuit breakers, queue length thresholds) is active.
- **Traffic Steering:** Shift load across regions/providers if available; coordinate with ISPs for null routing or traffic scrubbing when malicious segments persist.

## Communication
- **Internal:** Keep engineering, SRE, security, support, and leadership informed via incident channel and status updates (timeline, actions, risks).
- **External:** Update status pages, customer communications, and, if necessary, external partners/ISPs. Provide guidance on expected impact and mitigation progress.

## Recovery & Postmortem
- **Validation:** Confirm attack subsided, revert temporary policies cautiously, and monitor for secondary waves.
- **Data Capture:** Preserve logs, traffic captures, and timeline for forensic analysis; document decisions, tooling effectiveness, and gaps.
- **Follow-Up:** File action items (automation, tooling improvements, provider contracts, playbook refinements) and schedule a blameless postmortem review.

## References & Tooling
- **Providers:** AWS Shield/CloudFront, Azure Front Door, Google Cloud Armor, Cloudflare, Akamai Kona.
- **Detection:** Prometheus/Grafana dashboards, ELK/Loki logging, packet captures, provider analytics.
- **Testing:** DDoS simulation platforms, load-testing tools (k6, Locust), chaos engineering frameworks.

## Provider Quick Notes
- **AWS Shield Advanced:** Automatic detection with Route53/CloudFront integration; use AWS Firewall Manager for centralized rules.
- **Cloudflare:** Turn on "Under Attack" mode, set zone-level rate limits, leverage Magic Transit for network-layer attacks.
- **Google Cloud Armor:** Apply security policies with preconfigured WAF rules, enable adaptive protection for ML-based anomaly detection.
- **Akamai:** Coordinate with SOC for scrubbing, deploy Kona site defender rules tuned to application patterns.

## Diagram Ideas
- Timeline of detection → mitigation actions → recovery.
- Layered architecture showing traffic flow through CDN/WAF, load balancer, services, and data stores.
- Decision tree for choosing mitigation tactics based on attack type (volumetric vs application-layer).

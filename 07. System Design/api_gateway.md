# API Gateway Deep Dive

Highlight how API gateways centralize cross-cutting concerns, simplify client integrations, and enable rapid iteration across microservices.

## Cheat Sheet
- **Purpose:** Single entry point that handles routing, authentication, authorization, rate limiting, request/response transformation, observability, and monetization.
- **Contrast:** Complements (not replaces) load balancers; gateways operate at Layer 7 with business-aware policies, while LBs focus on traffic distribution.
- **When to introduce:** Multiple clients (web, mobile, partners), numerous backend services, need for consistent auth/policies, or monetized APIs.
- **Trade-offs:** Added latency, potential bottlenecks, operational complexity, risk of overloading with business logic.

## Quick Refresh
- **Routing:** Path-based, method-based, header-based routing to different services or versions.
- **Authentication & Authorization:** JWT validation, OAuth2 flows, API keys, mTLS, custom scopes.
- **Rate Limiting & Quotas:** Protect downstream services via token buckets, leaky bucket, or fixed window algorithms; support per-client quotas.
- **Request Transformation:** Rewrite headers, aggregate responses, perform protocol translation (REST ↔ gRPC ↔ SOAP).
- **Caching & Compression:** Offload response caching or payload compression for frequently accessed endpoints.
- **Observability:** Centralized logging, tracing, metrics, correlation IDs, and threat detection (WAF).

## Patterns & Trade-Offs

### API Gateway vs Backend For Frontend (BFF)
- **Gateway:** One gateway serving multiple clients; central policy engine.
- **BFF:** Dedicated service per client type (web, mobile) to tailor responses. Reduces payload bloat and client logic but increases service count.
- **Combination:** Gateway handles auth/rate limiting, then routes to client-specific BFFs.

### Managed vs Self-Hosted
- **Managed (AWS API Gateway, Apigee, Kong Cloud):** Faster setup, built-in analytics, auto-scaling; less control over customization and cost structure.
- **Self-hosted (Kong OSS, Tyk, Envoy, NGINX):** Greater flexibility, control over latency and extensions; requires ops expertise.
- **Decision factors:** Traffic scale, compliance needs, customization, team skill set.

### Security Posture
- **Threat protection:** WAF rules, bot detection, rate limiting, schema validation.
- **Zero-trust:** Combine mTLS, JWT verification, and per-route policies.
- **Secrets:** Rotate API keys/tokens, integrate with secret managers, log access patterns for anomaly detection.

### Versioning & Lifecycle
- **URL versioning (`/v1/`), header-based, or query-param based** depending on client capabilities.
- **Graceful deprecations:** Route old clients to legacy adapters, communicate timelines, monitor usage.
- **Canary releases:** Route a fraction of traffic to new versions using header flags or token targeting.

## Example Anecdotes
- **Partner integration:** Gateway enforced partner-specific rate limits and analytics, enabling monetized APIs while protecting core services.
- **gRPC adoption:** Gateway translated external REST calls to internal gRPC, allowing gradual client migration.
- **Security incident:** Missing auth on an internal endpoint exposed via gateway; incident response added default-deny policies and automated contract tests.
- **Latency regression:** Custom business logic in the gateway increased latency; refactor pushed heavy computation downstream to microservices.

## Interview Prompts
- When would you choose an API gateway versus direct service-to-service communication?
- How do you secure and monitor third-party integrations through the gateway?
- Explain how you’d handle rolling out a new version of an API while supporting old clients.
- Discuss strategies for rate limiting noisy clients without harming mission-critical users.

## Deep Dive Later
- Evaluate gateway offerings (AWS API Gateway, Kong, Apigee, Azure API Management) and pricing models.
- Prototype a lightweight gateway with Kong or Envoy; experiment with plugins for auth and rate limiting.
- Study case studies of API monetization and developer portal management for storytelling content.

## Diagram Ideas
- Request flow diagram: client → API gateway (auth, rate limiting, routing) → multiple microservices/BFFs.
- Component view: gateway integrating WAF, analytics, developer portal, and service discovery.
- Deployment topology: managed gateway vs self-hosted cluster with control plane/data plane separation.

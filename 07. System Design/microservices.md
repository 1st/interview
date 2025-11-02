# Microservices Architecture Deep Dive

Understand how to decompose, deploy, and operate services that collaborate without collapsing under complexity.

## Cheat Sheet
- **Why microservices?** Independent deployment, focused ownership, and heterogeneous stacks for fast iteration.
- **When to avoid?** Small teams, simple domains, or when DevOps maturity and observability tooling are lacking.
- **Core building blocks:** Service boundaries, contracts (APIs/events), discovery, observability, resilience patterns.
- **Interview hook:** Share a migration success or pain point from monolith to microservices.

## Quick Refresh
- **Service Boundaries:** Slice by business capability or bounded contexts. Minimize shared databases. Define contract-first APIs and versioning strategy.
- **Communication Patterns:** Synchronous REST/gRPC for request/response; asynchronous messaging/streaming for decoupling and backpressure.
- **Service Discovery:** Use registry (Consul, etcd, Eureka) or platform (Kubernetes DNS, service mesh). Highlight health checks and circuit breakers; revisit deployment primitives in [Kubernetes Operations](kubernetes.md).
- **Data Ownership:** Each service owns its datastore. Handle cross-service queries via composition, CQRS, or data replication.
- **Observability:** Standardize logging, metrics, tracing (OpenTelemetry). Implement correlation IDs across calls.
- **Resilience:** Employ retries with jitter, circuit breakers, bulkheads, load shedding, and graceful degradation.
- **Governance:** Maintain API guidelines, shared libraries, security policies, and guardrails for proliferation.

## Patterns & Trade-Offs

### Monolith to Microservices Migration
- **Strangler Fig:** Incrementally peel features into services behind routing rules.
- **Modular Monolith First:** Enforce module boundaries before splitting processes.
- **Parallel Change:** Dual-write or mirror traffic to new services for validation.

### Communication Styles
- **REST/gRPC:** Simplicity, widespread tooling, but risk of chatty I/O.
- **Messaging/Event-driven:** Loose coupling and eventual consistency; added complexity in ordering, replay, and idempotency.
- **GraphQL/BFF:** Tailored responses per client; introduces federation/aggregation services.

### Operational Footprint
- **DevOps Requirements:** Automated CI/CD, infrastructure-as-code, standardized observability.
- **Platform Support:** Kubernetes, ECS, Nomad, or PaaS for deployment orchestration (see [Kubernetes Operations](kubernetes.md)).
- **Security:** Zero-trust posture with mTLS, JWT, policy-as-code (OPA), secret management.

## Example Anecdotes
- **Release velocity:** Post-migration, teams shipped weekly vs quarterly but required investment in CI/CD and feature flagging.
- **Incident response:** A cascading failure caused by synchronous dependencies; implementing circuit breakers and async queues reduced blast radius.
- **Data consistency:** Event-driven replication introduced lag; eventually added read models and compensation workflows.
- **Ownership clarity:** Microservices exposed unclear domain boundaries; adopting DDD workshops realigned service scopes.

## Interview Prompts
- When would you choose microservices over a monolith, and what prerequisites must be in place?
- How do you manage data consistency across services that own different data stores?
- Describe strategies for breaking a legacy monolith into microservices without halting feature delivery.
- How do you debug a user request spanning multiple services?

## Deep Dive Later
- Domain-driven design (DDD) for boundary identification.
- Service meshes (Istio, Linkerd) for traffic management and policy enforcement.
- Event sourcing, CQRS, and saga patterns for distributed transactions.
- Team topology patterns (Conway’s Law) and platform engineering approaches.

## Diagram Ideas
- Context map showing bounded contexts and service interactions.
- Sequence diagram of user request traversing gateway, multiple services, and data stores.
- Deployment topology: services on Kubernetes/ECS with discovery, mesh, and observability sidecars.

### Diagram Prep Notes
1. Context map: note bounded contexts (e.g., Orders, Payments, Catalog) and shared components (gateway, discovery, observability stack).
2. Request journey: map synchronous calls vs async events; label tracing spans to show propagation.

Drafts: context map (`diagrams/microservices_context.md`) and request journey (`diagrams/microservices_request_sequence.md`).

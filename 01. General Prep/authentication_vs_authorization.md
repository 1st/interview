# Authentication vs Authorization

Authentication and authorization work together to guard access, but they solve different problems:

- **Authentication** answers *“Who are you?”* by verifying identity through credentials such as passwords, tokens, or biometrics.
- **Authorization** answers *“What are you allowed to do?”* by checking permissions after identity is verified.

## Cheat Sheet
- AuthN verifies identity; AuthZ checks permissions after identity is known.
- Mention MFA + secure credential storage as baseline hygiene.
- Tie authorization back to least privilege with explicit role or policy examples.

## Quick Refresh
- Confirm you can explain the flow: login → identity established → permission checks.
- Know common mechanisms: OAuth 2.0, JWTs, sessions, role-based access control (RBAC), attribute-based access control (ABAC).
- Highlight typical pitfalls: credential leakage, improper session management, over-permissive roles.
- Keep a simple sequence diagram in mind: user → identity provider → application → resource service.

## Scenario Snapshots
- **Public marketing site with admin portal:** Anonymous visitors authenticate only when accessing `/admin`; authorization enforces editor vs reviewer roles with fine-grained permissions on content actions.
- **Multi-tenant SaaS dashboard:** Central identity provider issues tokens containing tenant and role claims. Downstream services authorize requests by validating both tenant ownership and feature entitlements to prevent cross-tenant data leakage.
- **Internal microservice mesh:** mTLS authenticates services, while sidecar policy engines (e.g., OPA) evaluate authorization rules per endpoint, reducing logic duplication and enabling audit trails.

## Diagram Checklist
- Use a login flow sequence diagram: `Client → Auth Service → Identity Provider → Token` and return path to `Resource Server`.
- Include swimlanes for `User`, `App`, `Auth Provider`, and downstream `API` to highlight trust boundaries.
- Annotate where tokens are issued, stored, refreshed, and validated; call out failure paths (expired token, missing scope).

## Deep Dive Later
- Compare session-based vs token-based authentication and when to use each.
- Outline secure password storage (hashing, salting, peppering) and MFA strategies.
- Explore least privilege design, privilege escalation prevention, and audit logging patterns.
- Review how cloud providers (AWS IAM, GCP IAM, Azure AD) implement auth/authz flows.

## Interview Prompts
- Describe an end-to-end login flow for a web app and how you would secure it.
- Discuss how you would add a new microservice to an ecosystem while reusing existing auth.
- Explain debugging steps when a user reports unauthorized access or unexpected denial.

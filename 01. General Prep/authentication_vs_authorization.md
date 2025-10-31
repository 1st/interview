# Authentication vs Authorization

Authentication and authorization work together to guard access, but they solve different problems:

- **Authentication** answers *“Who are you?”* by verifying identity through credentials such as passwords, tokens, or biometrics.
- **Authorization** answers *“What are you allowed to do?”* by checking permissions after identity is verified.

## Quick Refresh
- Confirm you can explain the flow: login → identity established → permission checks.
- Know common mechanisms: OAuth 2.0, JWTs, sessions, role-based access control (RBAC), attribute-based access control (ABAC).
- Highlight typical pitfalls: credential leakage, improper session management, over-permissive roles.

## Deep Dive Later
- Compare session-based vs token-based authentication and when to use each.
- Outline secure password storage (hashing, salting, peppering) and MFA strategies.
- Explore least privilege design, privilege escalation prevention, and audit logging patterns.
- Review how cloud providers (AWS IAM, GCP IAM, Azure AD) implement auth/authz flows.

## Interview Prompts
- Describe an end-to-end login flow for a web app and how you would secure it.
- Discuss how you would add a new microservice to an ecosystem while reusing existing auth.
- Explain debugging steps when a user reports unauthorized access or unexpected denial.

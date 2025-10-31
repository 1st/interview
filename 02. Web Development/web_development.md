# Web Development Interview Refresh

Re-center on fundamental web platform concepts so you can confidently explain request flows, security risks, and modern service communication patterns.

## Cheat Sheet
- Trace the full HTTP request path including DNS, TLS, CDN, app, and database layers.
- Define XSS variants and prevention techniques (encode output, CSP, sanitization).
- Compare REST vs gRPC and note why teams adopt HTTP/2 streaming for microservices.

## Quick Refresh
- Map the HTTP request lifecycle, including DNS, TLS, proxies, and caching layers.
- Distinguish between transport (TCP) and application (HTTP) responsibilities.
- Recall common web security pitfalls such as XSS and how to mitigate them.
- Summarize service-to-service communication options, including REST and gRPC over HTTP/2.

## Interview Prompts
- **Explain HTTP vs TCP:** Clarify layering (OSI/Internet stack), reliability, connection management, and how HTTP leverages TCP streams. Be ready to touch on HTTP/2 multiplexing.
- **What is XSS and how do you prevent it?** Describe reflected, stored, and DOM-based variants. Emphasize output encoding, CSP, input validation, and protected templating systems. Reference real-world examples:
  - Injected `<script>` via search results that echo raw user input.
  - Malicious profile data on social platforms leaking session data.
  - SPA rendering unescaped client-side templates.
- **How does the web work end-to-end?** Walk through URL entry → DNS resolution → TCP/TLS handshake → HTTP request → load balancer/CDN → application → persistence tiers.
- **What is gRPC?** Highlight Protocol Buffers, HTTP/2 streaming, contract-first development, and typical use cases inside microservice ecosystems.

## Deep Dive Later
- [Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) and [Transmission Control Protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) for protocol internals.
- [How the web works](http://www.garshol.priv.no/download/text/http-tut.html) and [How the domain name system works](http://wiki.bravenet.com/How_the_domain_name_system_works) for lifecycle walkthroughs.
- Revisit gRPC guides for auth, load balancing, and code generation best practices.

# Interview Questions for Web developer


This chapter will help you to get answers on typical interview questions for **Web developers**.


## Questions


### What are HTTP and TCP

- Read [Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) on wikipedia
- Read [Transmission Control Protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)


### What is `XSS`?

[XSS (Cross-site scripting)](http://en.wikipedia.org/wiki/Cross-site_scripting) is a type of computer security vulnerability. `XSS` enables attackers to inject client-side script into Web pages viewed by other users. A cross-site scripting vulnerability may be used by attackers to bypass access controls such as the same origin policy.

**Example #1:** user send form with search query with `<script>` tag in it, and this page shows entered by user query without escaping it. In result we have injected JavaScript from external website. Attacher can share link to search results via email or own website.

**Example 2:** attacher can enter `<script>` tag in some field of personal profile on social network website. Whe user visiting page with attacker profile - JavaScript executes and can collect your personal information and send it to attacher email or website.

**Example 3 (DOM-based XSS):** when user visit website with SPA (single-page application) the JavaScript can render content without escaping data that comes from user input - and it can result in the same problem as described above.


### How's the web works?

* [How the web works](http://www.garshol.priv.no/download/text/http-tut.html)
* [How the domain name system works](http://wiki.bravenet.com/How_the_domain_name_system_works)


### What is gRPC?

**gRPC** is a high-performance, open-source RPC _(Remote Procedure Call)_ framework developed by Google. It allows services to communicate efficiently across networks using HTTP/2 and supports multiple programming languages.

It uses Protocol Buffers (ProtoBuf) as its default data serialization format, which is more compact and efficient than XML or JSON. gRPC enables features like bidirectional streaming, authentication, load balancing, and automatic code generation from .proto files.

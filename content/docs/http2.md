---
title: HTTP/2.0
menu: docs_proto
weight: 250
---

`actix-web` automatically upgrades connections to *HTTP/2.0* if possible.

# Negotiation

*HTTP/2.0* protocol over tls without prior knowledge requires [tls alpn][tlsalpn].

> Currently, only `rust-openssl` has support.

`alpn` negotiation requires enabling the feature. When enabled, `HttpServer` provides the
[bind_ssl][bindssl] method.

```toml
[dependencies]
actix-web = { version = "{{< actix-version "actix-web" >}}", features = ["ssl"] }
openssl = { version = "0.10", features = ["v110"] }
```
{{< include-example example="http2" file="main.rs" section="main" >}}

Upgrades to *HTTP/2.0* schema described in [rfc section 3.2][rfcsection32] is not
supported.  Starting *HTTP/2* with prior knowledge is supported for both clear text
connection and tls connection. [rfc section 3.4][rfcsection34].

> Check out [examples/tls][examples] for a concrete example.

[rfcsection32]: https://http2.github.io/http2-spec/#rfc.section.3.2
[rfcsection34]: https://http2.github.io/http2-spec/#rfc.section.3.4
[bindssl]: https://docs.rs/actix-web/1.0.2/actix_web/struct.HttpServer.html#method.bind_ssl
[tlsalpn]: https://tools.ietf.org/html/rfc7301
[examples]: https://github.com/actix/examples/tree/master/tls

# HTTP(S)

**HTTP (Hypertext Transfer Protocol)** is a protocol used for transmitting hypertext (such as HTML) over the internet. It is the foundation of any data exchange on the Web and it is a protocol used for transmitting documents in a hypertext format. HTTP follows a client-server model where the client makes a request and the server provides a response.

**HTTPS (Hypertext Transfer Protocol Secure)** is an extension of HTTP. It is used for secure communication over a computer network, and is widely used on the Internet. In HTTPS, the communication protocol is encrypted using Transport Layer Security (TLS) or, formerly, Secure Sockets Layer (SSL).

## History of HTTP and HTTPS

1. **HTTP/0.9 (1991)**: The first version of HTTP, a simple protocol for raw data transfer across the internet.
2. **HTTP/1.0 (1996)**: Introduced in RFC 1945, it added metadata (headers) to requests and responses.
3. **HTTP/1.1 (1997)**: Introduced in RFC 2068 and later updated in RFC 2616, it brought persistent connections, chunked transfer encoding, and more.
4. **HTTPS (1994)**: Netscape Communications created HTTPS for its Netscape Navigator web browser. It used SSL for encryption.
5. **HTTP/2 (2015)**: Introduced in RFC 7540, it improved performance by allowing multiple concurrent exchanges on the same connection.
6. **HTTP/3 (2020)**: Introduced in RFC 9000, it uses QUIC (Quick UDP Internet Connections) instead of TCP for improved performance and security.

## Examples

**HTTP Example:**

```http
GET /index.html HTTP/1.1
Host: www.example.com
```

**HTTPS Example:**

```http
GET /index.html HTTP/1.1
Host: www.example.com
```

In HTTPS, the above request would be encrypted using TLS, ensuring that the data cannot be read by third parties.

## Intermediate Examples

**HTTP POST Request:**

```http
POST /submit-form HTTP/1.1
Host: www.example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

name=John&age=30
```

**HTTPS POST Request:**

```http
POST /submit-form HTTP/1.1
Host: www.example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

name=John&age=30
```

Again, in HTTPS, the above request would be encrypted, providing confidentiality and integrity.

**HTTP/2 Example:**

HTTP/2 allows multiplexing, where multiple requests and responses can be in flight at the same time over a single connection.

```http
:method = GET
:path = /index.html
:scheme = https
:authority = www.example.com
```

**HTTP/3 Example:**

HTTP/3 uses QUIC, which is built on UDP, for faster and more reliable connections.

```http
:method = GET
:path = /index.html
:scheme = https
:authority = www.example.com
```

In summary, HTTP and HTTPS are essential protocols for web communication, with HTTPS providing a secure layer over HTTP. The evolution from HTTP/0.9 to HTTP/3 has brought significant improvements in performance, security, and reliability.




## References

- [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [List of HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
- [RFC 7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://tools.ietf.org/html/rfc7231)
- [RFC 7232 - Hypertext Transfer Protocol (HTTP/1.1): Conditional Requests](https://tools.ietf.org/html/rfc7232)
- [RFC 7233 - Hypertext Transfer Protocol (HTTP/1.1): Range Requests](https://tools.ietf.org/html/rfc7233)
- [RFC 7235 - Hypertext Transfer Protocol (HTTP/1.1): Authentication](https://tools.ietf.org/html/rfc7235)
- [RFC 5789 - PATCH Method for HTTP](https://tools.ietf.org/html/rfc5789)
- [RFC 7230 - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing](https://tools.ietf.org/html/rfc7230)
- [RFC 7234 - Hypertext Transfer Protocol (HTTP/1.1): Caching](https://tools.ietf.org/html/rfc7234)
- [RFC 7236 - Hypertext Transfer Protocol (HTTP/1.1): Authentication Scheme Registrations](https://tools.ietf.org/html/rfc7236)
- [RFC 7237 - Hypertext Transfer Protocol (HTTP/1.1): Method Definitions](https://tools.ietf.org/html/rfc7237)
- [RFC 7238 - Hypertext Transfer Protocol (HTTP/1.1): Permanent Redirect](https://tools.ietf.org/html/rfc7238)
- [RFC 7239 - Forwarded HTTP Extension](https://tools.ietf.org/html/rfc7239)
- [RFC 7540 - Hypertext Transfer Protocol Version 2 (HTTP/2)](https://tools.ietf.org/html/rfc7540)
- [RFC 7615 - HTTP Authentication-Info and Proxy-Authentication-Info Response Header Fields](https://tools.ietf.org/html/rfc7615)
- [RFC 7694 - Hypertext Transfer Protocol (HTTP) Client-Initiated Content-Encoding](https://tools.ietf.org/html/rfc7694)
- [RFC 7807 - Problem Details for HTTP APIs](https://tools.ietf.org/html/rfc7807)
- [RFC 7838 - HTTP Alternative Services](https://tools.ietf.org/html/rfc7838)
- [RFC 8297 - An HTTP Status Code for Indicating Hints](https://tools.ietf.org/html/rfc8297)
- [RFC 8470 - Using Early Data in HTTP](https://tools.ietf.org/html/rfc8470)
- [RFC 8473 - Token Binding over HTTP](https://tools.ietf.org/html/rfc8473)
- [RFC 8478 - Zstandard Compression and Decompression in Content-Encoding](https://tools.ietf.org/html/rfc8478)
- [RFC 8479 - Using Early Data in HTTP](https://tools.ietf.org/html/rfc8479)
- [RFC 8484 - DNS Queries over HTTPS (DoH)](https://tools.ietf.org/html/rfc8484)
- [RFC 8499 - DNS Terminology](https://tools.ietf.org/html/rfc8499)
- [RFC 8615 - Well-Known URIs](https://tools.ietf.org/html/rfc8615)
- [RFC 8670 - Deprecating the "X-" Prefix and Similar Constructs in Application Protocols](https://tools.ietf.org/html/rfc8670)

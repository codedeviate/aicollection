# Methods

HTTP methods are a set of request methods used by HTTP clients to indicate the desired action to be performed on a given resource. Here are the most commonly used HTTP methods:

## 1. GET
The `GET` method requests a representation of the specified resource. Requests using `GET` should only retrieve data and have no other effect.

### Example (GET)
```http
GET /users HTTP/1.1
Host: example.com
```

## 2. POST
The `POST` method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server.

### Example (POST)
```http
POST /users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

## 3. PUT
The `PUT` method replaces all current representations of the target resource with the request payload.

### Example (PUT)
```http
PUT /users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

## 4. DELETE
The `DELETE` method deletes the specified resource.

### Example (DELETE)
```http
DELETE /users/1 HTTP/1.1
Host: example.com
```

## 5. PATCH
The `PATCH` method is used to apply partial modifications to a resource.

### Example (PATCH)
```http
PATCH /users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "email": "john.new@example.com"
}
```

## 6. HEAD
The `HEAD` method asks for a response identical to that of a `GET` request, but without the response body.

### Example (HEAD)
```http
HEAD /users HTTP/1.1
Host: example.com
```

## 7. OPTIONS
The `OPTIONS` method is used to describe the communication options for the target resource.

### Example (OPTIONS)
```http
OPTIONS /users HTTP/1.1
Host: example.com
```

## 8. TRACE
The `TRACE` method performs a message loop-back test along the path to the target resource.

### Example (TRACE)
```http
TRACE /users HTTP/1.1
Host: example.com
```

## 9. CONNECT
The `CONNECT` method is used to establish a tunnel to the server identified by the target resource. It is primarily used for setting up a network connection to a resource through a proxy server, often for SSL (HTTPS) connections.

### Example (CONNECT)
```http
CONNECT server.example.com:443 HTTP/1.1
Host: server.example.com:443
```

## Safe, idempotent, and cacheable request methods

The following table lists HTTP request methods and their categorization in terms of safety, cacheability, and idempotency.

| Method  | Safe | Idempotent | Cacheable    |
|---------|------|------------|--------------|
| GET     | Yes  | Yes        | Yes          |
| HEAD    | Yes  | Yes        | Yes          |
| OPTIONS | Yes  | Yes        | No           |
| TRACE   | Yes  | Yes        | No           |
| PUT     | No   | Yes        | No           |
| DELETE  | No   | Yes        | No           |
| POST    | No   | No         | Conditional* |
| PATCH   | No   | No         | Conditional* |
| CONNECT | No   | No         | No           |

\* POST and PATCH are cacheable when responses explicitly include freshness information and a matching Content-Location header.

## HTTP/1.1 vs. HTTP/2: Request Methods

HTTP/1.1 and HTTP/2 support the same set of request methods, including GET, POST, PUT, DELETE, PATCH, OPTIONS, HEAD, TRACE, and CONNECT. However, there are some differences in how these methods are handled and optimized in HTTP/2 compared to HTTP/1.1:

1. **Multiplexing**: HTTP/2 allows multiple requests and responses to be sent simultaneously over a single connection, reducing latency and improving performance. In HTTP/1.1, each request/response pair requires a separate connection or the use of pipelining, which can lead to head-of-line blocking.

2. **Header Compression**: HTTP/2 uses HPACK compression for headers, which reduces the overhead of sending repetitive header fields. HTTP/1.1 does not have built-in header compression, leading to larger request and response sizes.

3. **Binary Framing**: HTTP/2 uses a binary framing layer, which makes it more efficient in parsing and processing requests and responses. HTTP/1.1 uses a text-based format, which can be more verbose and slower to process.

4. **Server Push**: HTTP/2 introduces the concept of server push, allowing the server to send resources to the client proactively. This feature is not available in HTTP/1.1.

5. **Stream Prioritization**: HTTP/2 allows clients to prioritize streams, enabling more important resources to be delivered first. HTTP/1.1 does not have built-in support for stream prioritization.

Despite these differences, the core request methods and their semantics remain the same between HTTP/1.1 and HTTP/2.

## HTTP/1.1 vs. HTTP/3: Request Methods

HTTP/1.1 and HTTP/3 support the same set of request methods, including GET, POST, PUT, DELETE, PATCH, OPTIONS, HEAD, TRACE, and CONNECT. However, there are some differences in how these methods are handled and optimized in HTTP/3 compared to HTTP/1.1:

1. **Transport Protocol**: HTTP/3 uses QUIC as its transport protocol, which is built on UDP, whereas HTTP/1.1 uses TCP. This change improves connection establishment times and reduces latency.

2. **Multiplexing**: Similar to HTTP/2, HTTP/3 allows multiple requests and responses to be sent simultaneously over a single connection, reducing latency and improving performance. HTTP/1.1 requires separate connections or pipelining, which can lead to head-of-line blocking.

3. **Header Compression**: HTTP/3 uses QPACK for header compression, which is designed to work efficiently with QUIC. HTTP/1.1 does not have built-in header compression, leading to larger request and response sizes.

4. **Binary Framing**: HTTP/3, like HTTP/2, uses a binary framing layer, making it more efficient in parsing and processing requests and responses. HTTP/1.1 uses a text-based format, which can be more verbose and slower to process.

5. **Connection Migration**: HTTP/3 supports connection migration, allowing connections to continue seamlessly even if the client's IP address changes. This feature is not available in HTTP/1.1.

Despite these differences, the core request methods and their semantics remain the same between HTTP/1.1 and HTTP/3.

## HTTP/2 vs. HTTP/3: Request Methods

HTTP/2 and HTTP/3 support the same set of request methods, including GET, POST, PUT, DELETE, PATCH, OPTIONS, HEAD, TRACE, and CONNECT. However, there are some differences in how these methods are handled and optimized in HTTP/3 compared to HTTP/2:

1. **Transport Protocol**: HTTP/3 uses QUIC as its transport protocol, which is built on UDP, whereas HTTP/2 uses TCP. This change improves connection establishment times and reduces latency.

2. **Header Compression**: HTTP/3 uses QPACK for header compression, which is designed to work efficiently with QUIC. HTTP/2 uses HPACK for header compression.

3. **Connection Migration**: HTTP/3 supports connection migration, allowing connections to continue seamlessly even if the client's IP address changes. This feature is not available in HTTP/2.

Despite these differences, the core request methods and their semantics remain the same between HTTP/2 and HTTP/3.

## Conclusion
Understanding HTTP methods is essential for designing and interacting with web APIs. Each method serves a specific purpose and helps in performing various operations on resources.


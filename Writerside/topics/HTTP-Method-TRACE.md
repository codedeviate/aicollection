# TRACE

The `TRACE` method is used to perform a message loop-back test along the path to the target resource. It allows the client to see what is being received at the other end of the request chain and can be useful for debugging purposes.

## Basic Syntax
```http
TRACE /path/to/resource HTTP/1.1
Host: example.com
```

## Key Characteristics
- **Safe**: `TRACE` requests do not alter the state of the server.
- **Idempotent**: Multiple identical `TRACE` requests should have the same effect as a single request.
- **Not Cacheable**: Responses to `TRACE` requests are not typically cached.

## Parameters
- **Headers**: `TRACE` requests can include headers to specify metadata.
  ```http
  Max-Forwards: 5
  ```

## Examples

1. **Basic TRACE Request**
   ```http
   TRACE /users HTTP/1.1
   Host: example.com
   ```
   This request performs a loop-back test for the `/users` resource.

2. **TRACE Request with Max-Forwards Header**
   ```http
   TRACE /users HTTP/1.1
   Host: example.com
   Max-Forwards: 5
   ```
   This request performs a loop-back test for the `/users` resource with a `Max-Forwards` header set to 5, limiting the number of hops the request can take.

## Conclusion
The `TRACE` method is essential for debugging and diagnostic purposes, allowing clients to see the request path and what is being received at the server. Understanding its characteristics and how to use headers allows you to effectively troubleshoot and interact with web APIs.
# OPTIONS

The `OPTIONS` method is used to describe the communication options for the target resource. It allows the client to determine the capabilities of a server and the requirements for interacting with a resource. This method is often used for CORS (Cross-Origin Resource Sharing) preflight requests.

## Basic Syntax
```http
OPTIONS /path/to/resource HTTP/1.1
Host: example.com
```

## Key Characteristics
- **Safe**: `OPTIONS` requests do not alter the state of the server.
- **Idempotent**: Multiple identical `OPTIONS` requests should have the same effect as a single request.
- **Cacheable**: Responses to `OPTIONS` requests can be cached by the client and intermediate proxies.

## Parameters
- **Headers**: `OPTIONS` requests can include headers to specify metadata.
  ```http
  Access-Control-Request-Method: POST
  Access-Control-Request-Headers: Content-Type
  ```

## Examples

1. **Basic OPTIONS Request**
   ```http
   OPTIONS /users HTTP/1.1
   Host: example.com
   ```
   This request retrieves the communication options for the `/users` resource.

2. **OPTIONS Request with CORS Headers**
   ```http
   OPTIONS /users HTTP/1.1
   Host: example.com
   Access-Control-Request-Method: POST
   Access-Control-Request-Headers: Content-Type
   Origin: http://example-client.com
   ```
   This request checks the CORS policy for the `/users` resource, specifically for a `POST` request with a `Content-Type` header from the origin `http://example-client.com`.

## Conclusion
The `OPTIONS` method is essential for discovering the communication options and requirements for a resource. Understanding its characteristics and how to use headers allows you to effectively manage resource interactions and handle CORS preflight requests.
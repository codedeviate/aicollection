# CONNECT

The `CONNECT` method is used to establish a tunnel to the server identified by the target resource. It is primarily used for setting up a network connection to a resource through a proxy server, often for SSL (HTTPS) connections.

## Basic Syntax
```http
CONNECT server.example.com:443 HTTP/1.1
Host: server.example.com:443
```

## Key Characteristics
- **Not Safe**: `CONNECT` requests can change the state of the server.
- **Not Idempotent**: Multiple identical `CONNECT` requests may have different effects.
- **Not Cacheable**: Responses to `CONNECT` requests are not typically cached.

## Parameters
- **Headers**: `CONNECT` requests can include headers to specify metadata.
  ```http
  Proxy-Authorization: Basic dXNlcjpwYXNzd29yZA==
  ```

## Examples

1. **Basic CONNECT Request**
   ```http
   CONNECT server.example.com:443 HTTP/1.1
   Host: server.example.com:443
   ```
   This request establishes a tunnel to `server.example.com` on port 443.

2. **CONNECT Request with Proxy Authorization**
   ```http
   CONNECT server.example.com:443 HTTP/1.1
   Host: server.example.com:443
   Proxy-Authorization: Basic dXNlcjpwYXNzd29yZA==
   ```
   This request establishes a tunnel to `server.example.com` on port 443 and includes a proxy authorization header.

## Conclusion
The `CONNECT` method is essential for establishing a network tunnel through a proxy server, often used for HTTPS connections. Understanding its characteristics and how to use headers allows you to effectively manage secure connections and interact with web APIs.
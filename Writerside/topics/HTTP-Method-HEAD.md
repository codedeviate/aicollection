# HEAD

The `HEAD` method is used to retrieve the headers of a resource without fetching the body. It is similar to the `GET` method, but the server does not return the message body in the response. This method is useful for checking what a `GET` request will return before actually making the `GET` request, such as checking for the existence of a resource or its metadata.

## Basic Syntax
```http
HEAD /path/to/resource HTTP/1.1
Host: example.com
```

## Key Characteristics
- **Safe**: `HEAD` requests do not alter the state of the server.
- **Idempotent**: Multiple identical `HEAD` requests should have the same effect as a single request.
- **Cacheable**: Responses to `HEAD` requests can be cached by the client and intermediate proxies.

## Parameters
- **Headers**: `HEAD` requests can include headers to specify metadata.
  ```http
  Authorization: Bearer token
  ```

## Examples

1. **Basic HEAD Request**
   ```http
   HEAD /users HTTP/1.1
   Host: example.com
   ```
   This request retrieves the headers for the list of users.

2. **HEAD Request with Headers**
   ```http
   HEAD /users HTTP/1.1
   Host: example.com
   Authorization: Bearer token
   ```
   This request retrieves the headers for the list of users and includes an authorization header.

## Conclusion
The `HEAD` method is essential for retrieving metadata about a resource without fetching the entire content. Understanding its characteristics and how to use headers allows you to effectively check resource information and interact with web APIs.
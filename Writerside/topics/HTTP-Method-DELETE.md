# DELETE

The `DELETE` method is used to delete a specified resource. It is one of the fundamental methods in HTTP and is used to remove resources from a server.

## Basic Syntax
```http
DELETE /path/to/resource HTTP/1.1
Host: example.com
```

## Key Characteristics
- **Idempotent**: Multiple identical `DELETE` requests should have the same effect as a single request.
- **Not Safe**: `DELETE` requests can change the state of the server.
- **Not Cacheable**: Responses to `DELETE` requests are not typically cached.

## Parameters
- **Headers**: `DELETE` requests can include headers to specify metadata.
  ```http
  Authorization: Bearer token
  ```

## Examples

1. **Basic DELETE Request**
   ```http
   DELETE /users/1 HTTP/1.1
   Host: example.com
   ```
   This request deletes the user with ID 1 from the server.

2. **DELETE Request with Headers**
   ```http
   DELETE /users/1 HTTP/1.1
   Host: example.com
   Authorization: Bearer token
   ```
   This request deletes the user with ID 1 and includes an authorization header.

## Conclusion
The `DELETE` method is essential for removing resources from a server. Understanding its characteristics and how to use headers allows you to effectively manage resource deletion and interact with web APIs.
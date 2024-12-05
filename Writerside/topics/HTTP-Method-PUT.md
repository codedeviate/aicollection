# PUT

The `PUT` method is used to update or replace a resource at a specified URI. It is often used to update an existing resource or create a new resource if it does not exist.

## Basic Syntax
```http
PUT /path/to/resource HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "key1": "value1",
  "key2": "value2"
}
```

## Key Characteristics
- **Idempotent**: Multiple identical `PUT` requests should have the same effect as a single request.
- **Not Safe**: `PUT` requests can change the state of the server.
- **Not Cacheable**: Responses to `PUT` requests are not typically cached.

## Parameters
- **Request Body**: `PUT` requests often include a body containing the data to be sent to the server.
  ```json
  {
    "key1": "value1",
    "key2": "value2"
  }
  ```
- **Headers**: `PUT` requests can include headers to specify the content type and other metadata.
  ```http
  Content-Type: application/json
  ```

## Examples

1. **Basic PUT Request**
   ```http
   PUT /users/1 HTTP/1.1
   Host: example.com
   Content-Type: application/json

   {
     "name": "John Doe",
     "email": "john.doe@example.com"
   }
   ```
   This request updates the user with ID 1 with the specified name and email.

2. **PUT Request to Create a Resource**
   ```http
   PUT /users/2 HTTP/1.1
   Host: example.com
   Content-Type: application/json

   {
     "name": "Jane Doe",
     "email": "jane.doe@example.com"
   }
   ```
   This request creates a new user with ID 2 if it does not already exist.

3. **PUT Request with Headers**
   ```http
   PUT /users/1 HTTP/1.1
   Host: example.com
   Content-Type: application/json
   Authorization: Bearer token

   {
     "name": "John Doe",
     "email": "john.doe@example.com"
   }
   ```
   This request updates the user with ID 1 and includes an authorization header.

## Conclusion
The `PUT` method is essential for updating or replacing resources on a server. Understanding its characteristics and how to use request bodies and headers allows you to effectively manage resources and interact with web APIs.
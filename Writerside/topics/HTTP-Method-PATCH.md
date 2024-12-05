# PATCH

The `PATCH` method is used to apply partial modifications to a resource. Unlike the `PUT` method, which replaces the entire resource, `PATCH` only updates the specified fields.

## Basic Syntax
```http
PATCH /path/to/resource HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "key1": "new_value1"
}
```

## Key Characteristics
- **Non-idempotent**: Multiple identical `PATCH` requests may have different effects.
- **Not Safe**: `PATCH` requests can change the state of the server.
- **Not Cacheable**: Responses to `PATCH` requests are not typically cached.

## Parameters
- **Request Body**: `PATCH` requests often include a body containing the data to be updated.
  ```json
  {
    "key1": "new_value1"
  }
  ```
- **Headers**: `PATCH` requests can include headers to specify the content type and other metadata.
  ```http
  Content-Type: application/json
  ```

## Examples

1. **Basic PATCH Request**
   ```http
   PATCH /users/1 HTTP/1.1
   Host: example.com
   Content-Type: application/json

   {
     "email": "john.new@example.com"
   }
   ```
   This request updates the email of the user with ID 1.

2. **PATCH Request with Multiple Fields**
   ```http
   PATCH /users/1 HTTP/1.1
   Host: example.com
   Content-Type: application/json

   {
     "name": "John New",
     "email": "john.new@example.com"
   }
   ```
   This request updates both the name and email of the user with ID 1.

3. **PATCH Request with Headers**
   ```http
   PATCH /users/1 HTTP/1.1
   Host: example.com
   Content-Type: application/json
   Authorization: Bearer token

   {
     "email": "john.new@example.com"
   }
   ```
   This request updates the email of the user with ID 1 and includes an authorization header.

## Conclusion
The `PATCH` method is essential for making partial updates to resources on a server. Understanding its characteristics and how to use request bodies and headers allows you to effectively manage resource updates and interact with web APIs.
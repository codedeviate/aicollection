# GET

The `GET` method is one of the most commonly used HTTP methods. It is used to request data from a specified resource. Requests using `GET` should only retrieve data and have no other effect on the resource.

## Basic Syntax
```http
GET /path/to/resource HTTP/1.1
Host: example.com
```

## Key Characteristics
- **Safe**: `GET` requests do not alter the state of the server.
- **Idempotent**: Multiple identical `GET` requests should have the same effect as a single request.
- **Cacheable**: Responses to `GET` requests can be cached by the client and intermediate proxies.

## Parameters
- **Query Parameters**: `GET` requests can include query parameters to filter or modify the request.
  ```http
  GET /users?name=John HTTP/1.1
  Host: example.com
  ```

## Examples

1. **Basic GET Request**
   ```http
   GET /users HTTP/1.1
   Host: example.com
   ```
   This request retrieves a list of users from the server.

2. **GET Request with Query Parameters**
   ```http
   GET /users?name=John&age=30 HTTP/1.1
   Host: example.com
   ```
   This request retrieves users named John who are 30 years old.

3. **GET Request with Headers**
   ```http
   GET /users HTTP/1.1
   Host: example.com
   Accept: application/json
   ```
   This request retrieves a list of users and specifies that the client expects a JSON response.

## Conclusion
The `GET` method is essential for retrieving data from a server. Understanding its characteristics and how to use query parameters and headers allows you to effectively request and filter data from web APIs.
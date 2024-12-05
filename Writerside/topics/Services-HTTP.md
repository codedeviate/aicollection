# HTTP


The Hypertext Transfer Protocol (HTTP) is an application-layer protocol used for transmitting hypermedia documents, such as HTML. It is the foundation of data communication on the World Wide Web. HTTP follows a client-server model where the client makes requests and the server sends responses.

## Key Concepts of HTTP

- **Client-Server Model**: HTTP operates on a client-server model where the client (usually a web browser) sends requests to the server, and the server responds with the requested resources.
- **Stateless Protocol**: HTTP is stateless, meaning each request from a client to a server is independent, and the server does not retain any state information between requests.
- **Methods**: HTTP defines several request methods to indicate the desired action to be performed on the identified resource.

## HTTP Methods

- **GET**: Requests a representation of the specified resource. Requests using GET should only retrieve data.
- **POST**: Submits data to be processed to a specified resource.
- **PUT**: Replaces all current representations of the target resource with the request payload.
- **DELETE**: Deletes the specified resource.
- **HEAD**: Asks for a response identical to a GET request, but without the response body.
- **OPTIONS**: Describes the communication options for the target resource.
- **PATCH**: Applies partial modifications to a resource.

## HTTP Status Codes

- **1xx (Informational)**: Request received, continuing process.
- **2xx (Success)**: The action was successfully received, understood, and accepted.
    - **200 OK**: The request has succeeded.
    - **201 Created**: The request has been fulfilled and resulted in a new resource being created.
- **3xx (Redirection)**: Further action needs to be taken to complete the request.
    - **301 Moved Permanently**: The resource has been moved to a new URL permanently.
    - **302 Found**: The resource has been found at a different URL temporarily.
- **4xx (Client Error)**: The request contains bad syntax or cannot be fulfilled.
    - **400 Bad Request**: The server could not understand the request due to invalid syntax.
    - **401 Unauthorized**: The client must authenticate itself to get the requested response.
    - **404 Not Found**: The server can not find the requested resource.
- **5xx (Server Error)**: The server failed to fulfill a valid request.
    - **500 Internal Server Error**: The server has encountered a situation it doesn't know how to handle.
    - **503 Service Unavailable**: The server is not ready to handle the request.

## Example: Making HTTP Requests Using Python's `requests` Library

Here is an example of making HTTP requests using Python's `requests` library:

```python
import requests

# GET request
response = requests.get('https://api.example.com/data')
print(response.status_code)
print(response.json())

# POST request
data = {'key': 'value'}
response = requests.post('https://api.example.com/data', json=data)
print(response.status_code)
print(response.json())

# PUT request
data = {'key': 'new_value'}
response = requests.put('https://api.example.com/data/1', json=data)
print(response.status_code)
print(response.json())

# DELETE request
response = requests.delete('https://api.example.com/data/1')
print(response.status_code)
```

## Relevant Switches and Parameters

### Common `requests` Methods
- `requests.get(url, params=None, **kwargs)`: Sends a GET request.
- `requests.post(url, data=None, json=None, **kwargs)`: Sends a POST request.
- `requests.put(url, data=None, **kwargs)`: Sends a PUT request.
- `requests.delete(url, **kwargs)`: Sends a DELETE request.

Understanding HTTP and its associated methods and status codes is crucial for implementing and troubleshooting web services.
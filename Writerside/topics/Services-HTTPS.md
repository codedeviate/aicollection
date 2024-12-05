# HTTPS

The Hypertext Transfer Protocol Secure (HTTPS) is an extension of HTTP. It is used for secure communication over a computer network and is widely used on the Internet. HTTPS uses Transport Layer Security (TLS) or its predecessor, Secure Sockets Layer (SSL), to encrypt the data exchanged between the client and the server.

## Key Concepts of HTTPS

- **Encryption**: HTTPS encrypts the data exchanged between the client and the server, ensuring that it cannot be read by third parties.
- **Authentication**: HTTPS uses certificates to authenticate the server, ensuring that the client is communicating with the intended server.
- **Integrity**: HTTPS ensures that the data exchanged between the client and the server is not tampered with during transmission.

## HTTPS Methods

HTTPS uses the same methods as HTTP, including:

- **GET**: Requests a representation of the specified resource.
- **POST**: Submits data to be processed to a specified resource.
- **PUT**: Replaces all current representations of the target resource with the request payload.
- **DELETE**: Deletes the specified resource.
- **HEAD**: Asks for a response identical to a GET request, but without the response body.
- **OPTIONS**: Describes the communication options for the target resource.
- **PATCH**: Applies partial modifications to a resource.

## HTTPS Status Codes

HTTPS uses the same status codes as HTTP, including:

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

## Example: Making HTTPS Requests Using Python's `requests` Library

Here is an example of making HTTPS requests using Python's `requests` library:

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

Understanding HTTPS and its associated methods and status codes is crucial for implementing and troubleshooting secure web services.
# 201

HTTP status code 201 indicates that the request has been fulfilled and has resulted in the creation of a new resource. The response should include a `Location` header field containing the URL of the newly created resource.

To handle a 201 status code in PHP, you can set the HTTP response code and provide the location of the new resource. Here is an example:

```php
<?php
// Set the HTTP response code to 201
http_response_code(201);

// Provide the location of the new resource
header('Location: https://www.example.com/new-resource');
exit;
```

This code sets the HTTP response code to 201 and includes a `Location` header with the URL of the newly created resource. This informs the client that the request was successful and a new resource has been created.

When encountering a 201 status code, the client can access the newly created resource using the provided URL. This status code is commonly used for successful creation requests, such as when submitting a form to create a new resource on the server. It is important to include the `Location` header to provide the client with the URL of the newly created resource.
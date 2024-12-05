# 404

HTTP status code 404 indicates that the server cannot find the requested resource. This status code is used when the server cannot locate the requested URL.

To handle a 404 status code in PHP, you can set the HTTP response code and display an error message. Here is an example:

```php
<?php
// Set the HTTP response code to 404
http_response_code(404);

// Display an error message
echo 'Not Found: The requested resource could not be found on this server.';
```


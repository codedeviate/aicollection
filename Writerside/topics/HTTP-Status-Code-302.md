# 302

HTTP status code 302 indicates that the requested resource has been temporarily moved to a different URL. This status code is used for temporary URL redirection.

To handle a 302 status code in PHP, you can set the HTTP response code and provide the new location URL. Here is an example:

```php
<?php
// Set the HTTP response code to 302
http_response_code(302);

// Redirect to the new URL
header('Location: https://www.temporary-url.com');
exit;
```

This code sets the HTTP response code to 302 and redirects the user to the new URL. This informs the client that the requested resource has been temporarily moved and provides the new location for the resource.

When encountering a 302 status code, the client should follow the redirection to access the resource at the new URL. This status code is commonly used for temporary URL changes and can be used for scenarios such as maintenance or testing of a different URL. It is important to note that the client should not cache the redirection as the resource may move back to the original URL in the future.
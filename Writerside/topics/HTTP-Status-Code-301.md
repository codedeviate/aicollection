# 301

HTTP status code 301 indicates that the requested resource has been permanently moved to a new URL. This status code is used for URL redirection.

To handle a 301 status code in PHP, you can set the HTTP response code and provide the new location URL. Here is an example:

```php
<?php
// Set the HTTP response code to 301
http_response_code(301);

// Redirect to the new URL
header('Location: https://www.new-url.com');
exit;
```

This code sets the HTTP response code to 301 and redirects the user to the new URL. This informs the client that the requested resource has been permanently moved and provides the new location for the resource.

When encountering a 301 status code, the client should update its bookmarks or links to the old URL to the new URL. This status code is commonly used for SEO purposes to redirect users and search engines to the new location of a resource. It is important to use 301 redirects for permanent URL changes to maintain search engine rankings and user experience.
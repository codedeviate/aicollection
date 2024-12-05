# Status codes

[100-199](#100-199) | [200-299](#200-299) | [300-399](#300-399) | [400-499](#400-499) | [500-599](#500-599) | [Other Status Codes](#other-status-codes)

## 100-199

HTTP status codes starting with 1 (1xx) are informational responses. These codes indicate that the request was received and understood, and the client should continue with the request or ignore the response if the request is already finished. Here are the specific codes:

| Code                           | Description         |
|--------------------------------|---------------------|
| [100](HTTP-Status-Code-100.md) | Continue            |
| 101                            | Switching Protocols |
| 102                            | Processing          |
| 103                            | Early Hints         |
    

## 200-299

HTTP status codes starting with 2 (2xx) indicate successful responses. These codes mean that the client's request was successfully received, understood, and accepted. Here are the specific codes:

| Code                           | Description                   |
|--------------------------------|-------------------------------|
| [200](HTTP-Status-Code-200.md) | OK                            |
| [201](HTTP-Status-Code-201.md) | Created                       |
| 202                            | Accepted                      |
| 203                            | Non-Authoritative Information |
| 204                            | No Content                    |
| 205                            | Reset Content                 |
| 206                            | Partial Content               |
| 207                            | Multi-Status                  |
| 208                            | Already Reported              |
| 226                            | IM Used                       |

## 300-399

HTTP status codes starting with 3 (3xx) indicate redirection responses. These codes inform the client that the requested resource is located elsewhere, and the client should take additional action to complete the request. Here are the specific codes:

| Code                           | Description                   |
|--------------------------------|-------------------------------|
| 300                            | Multiple Choices              |
| [301](HTTP-Status-Code-301.md) | Moved Permanently             |
| [302](HTTP-Status-Code-302.md) | Found                         |
| 303                            | See Other                     |
| 304                            | Not Modified                  |
| 305                            | Use Proxy (deprecated)        |
| 306                            | Switch Proxy (no longer used) |
| 307                            | Temporary Redirect            |
| 308                            | Permanent Redirect            |

## 400-499

HTTP status codes starting with 4 (4xx) indicate client errors. These codes are returned when the client's request contains incorrect syntax, cannot be fulfilled, or encounters authorization issues. Here are the specific codes:

| Code                           | Description                                      |
|--------------------------------|--------------------------------------------------|
| [400](HTTP-Status-Code-400.md) | Bad Request                                      |
| [401](HTTP-Status-Code-401.md) | Unauthorized                                     |
| [402](HTTP-Status-Code-402.md) | Payment Required                                 |
| [403](HTTP-Status-Code-403.md) | Forbidden                                        |
| [404](HTTP-Status-Code-404.md) | Not Found                                        |
| [405](HTTP-Status-Code-405.md) | Method Not Allowed                               |
| 406                            | Not Acceptable                                   |
| 407                            | Proxy Authentication Required                    |
| 408                            | Request Timeout                                  |
| 409                            | Conflict                                         |
| 410                            | Gone                                             |
| 411                            | Length Required                                  |
| 412                            | Precondition Failed                              |
| 413                            | Payload Too Large                                |
| 414                            | URI Too Long                                     |
| 415                            | Unsupported Media Type                           |
| 416                            | Range Not Satisfiable                            |
| 417                            | Expectation Failed                               |
| 418                            | I'm a teapot                                     |
| 419                            | Page Expired                                     |
| 420                            | Enhance Your Calm (Twitter/X)                    |
| 421                            | Misdirected Request                              |
| 422                            | Unprocessable Entity                             |
| 423                            | Locked                                           |
| 424                            | Failed Dependency                                |
| 425                            | Too Early                                        |
| 426                            | Upgrade Required                                 |
| 428                            | Precondition Required                            |
| [429](HTTP-Status-Code-429.md) | Too Many Requests                                |
| 431                            | Request Header Fields Too Large                  |
| 444                            | No response (Nginx)                              |
| 450                            | Blocked by Windows Parental Controls (Microsoft) |
| 451                            | Unavailable For Legal Reasons                    |

## 500-599

HTTP status codes starting with 5 (5xx) indicate server errors. These codes are returned when the server encounters an error while processing the request. Here are the specific codes:

| Code                           | Description                                       |
|--------------------------------|---------------------------------------------------|
| 500                            | Internal Server Error                             |
| 501                            | Not Implemented                                   |
| 502                            | Bad Gateway                                       |
| [503](HTTP-Status-Code-503.md) | Service Unavailable                               |
| 504                            | Gateway Timeout                                   |
| 505                            | HTTP Version Not Supported                        |
| 506                            | Variant Also Negotiates                           |
| 507                            | Insufficient Storage                              |
| 508                            | Loop Detected                                     |
| 509                            | Bandwidth Limit Exceeded                          |
| 510                            | Not Extended                                      |
| 511                            | Network Authentication Required                   |
| 520                            | Web Server Returned an Unknown Error (Cloudflare) |
| 521                            | Web Server Is Down (Cloudflare)                   |
| 522                            | Connection Timed Out (Cloudflare)                 |
| 523                            | Origin Is Unreachable (Cloudflare)                |
| 524                            | A Timeout Occurred (Cloudflare)                   |
| 525                            | SSL Handshake Failed (Cloudflare)                 |
| 526                            | Invalid SSL Certificate (Cloudflare)              |
| 527                            | Railgun Error (Cloudflare)                        |
| 530                            | Origin DNS Error (Cloudflare)                     |
| 530                            | Site is frozen (Pantheon)                         |
| 598                            | Network read timeout error (Cloudflare)           |
| 599                            | Network connect timeout error (Cloudflare)        |

## Other Status Codes

There are other status codes that are not part of the standard HTTP/1.1 specification but are used by some servers or frameworks. These codes are typically in the range of 600-699 and are specific to the implementation. Some examples include:

- 600: Unparseable Response
- 601: Unparseable Response Headers
- 602: Unparseable Response Body
- 603: Request Timeout
- 604: Response Timeout
- 605: Request Failed
- 606: Response Failed
- 607: Request Aborted
- 608: Response Aborted
- 609: Request Connection Failed
- 610: Response Connection Failed
- 611: Request Disallowed
- 612: Response Disallowed
- 613: Request Connection Disallowed
- 614: Response Connection Disallowed
- 615: Request Connection Timeout
- 616: Response Connection Timeout
- 617: Request Connection Limit Exceeded
- 618: Response Connection Limit Exceeded
- 619: Request Connection Refused
- 620: Response Connection Refused
- 621: Request Connection Reset
- 622: Response Connection Reset
- 623: Request Connection Closed
- 624: Response Connection Closed
- 625: Request Connection Aborted
- 626: Response Connection Aborted
- 627: Request Connection Disconnected
- 628: Response Connection Disconnected
- 629: Request Connection Unavailable
- 630: Response Connection Unavailable
- 631: Request Connection Unresponsive
- 632: Response Connection Unresponsive
- 633: Request Connection Invalid
- 634: Response Connection Invalid
- 635: Request Connection Insecure
- 636: Response Connection Insecure
- 637: Request Connection Encrypted
- 638: Response Connection Encrypted
- 639: Request Connection Overloaded
- 640: Response Connection Overloaded
- 641: Request Connection Oversubscribed
- 642: Response Connection Oversubscribed
- 643: Request Connection Overused
- 644: Response Connection Overused
- 645: Request Connection Overridden
- 646: Response Connection Overridden

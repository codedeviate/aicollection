# Network Services

In this stage of the course, we focus on building **Network Services**, which are integral to modern computing systems. Network services allow devices to communicate and share resources over a network, forming the backbone of the internet and corporate IT infrastructures. By creating both clients and servers for these services, you'll gain a deep understanding of how these systems operate and interact.

This section emphasizes creating robust, efficient, and secure network applications. You will explore a range of protocols—HTTP, FTP, SMTP, Telnet, SSH, DNS, and more—while implementing real-world solutions. These projects will enhance your ability to build scalable applications and design complex systems.

---

## Tools We Will Build

### 1. HTTP Client
[Go to lesson](Go-Tools-HTTP-Client.md)

An HTTP Client sends requests and processes responses from web servers. In this module, you will:
- Build a client that supports GET, POST, and other HTTP methods.
- Handle headers, cookies, and query parameters.
- Implement timeout and retry mechanisms for reliability.

This project introduces you to the ubiquitous HTTP protocol and its practical applications.

---

### 2. HTTP Server
[Go to lesson](Go-Tools-HTTP-Server.md)

An HTTP Server responds to client requests and serves content. You will:
- Build a web server using Go’s `net/http` package.
- Implement routing to handle different endpoints.
- Add features like logging, static file serving, and API responses.

This tool demonstrates how to set up a basic web application or API backend.

---

### 3. HTTPS Client
[Go to lesson](Go-Tools-HTTPS-Client.md)

An HTTPS Client establishes secure connections to servers, ensuring privacy and integrity. You will:
- Configure TLS for encrypted communication.
- Validate certificates and handle errors gracefully.
- Work with secure APIs and web services.

This module highlights the importance of encryption in modern applications.

---

### 4. HTTPS Server
[Go to lesson](Go-Tools-HTTPS-Server.md)

An HTTPS Server secures web communications for clients. In this project, you will:
- Set up TLS certificates for HTTPS.
- Enforce strong encryption standards.
- Implement best practices for securing your server.

This tool prepares you to build secure, production-ready web applications.

---

### 5. FTP Client
[Go to lesson](Go-Tools-FTP-Client.md)

An FTP Client handles file transfers over the File Transfer Protocol. You will:
- Connect to FTP servers and navigate directories.
- Upload, download, and delete files programmatically.
- Handle authentication and file permissions.

This project provides practical experience with legacy yet widely-used protocols.

---

### 6. FTP Server
[Go to lesson](Go-Tools-FTP-Server.md)

An FTP Server facilitates file sharing and management for clients. You will:
- Implement user authentication and access control.
- Manage file uploads, downloads, and directory operations.
- Log client activity for monitoring purposes.

This project teaches you server-side file handling and user management.

---

### 7. FTPS Client & 8. FTPS Server
[Go to lesson](Go-Tools-FTPS-Client.md) [Go to lesson](Go-Tools-FTPS-Server.md)

FTPS (FTP Secure) adds encryption to the FTP protocol. In these modules, you will:
- Integrate TLS with your FTP client and server.
- Secure file transfers against interception and tampering.
- Ensure backward compatibility with traditional FTP systems.

These tools emphasize the importance of securing legacy protocols.

---

### 9. SMTP Client & 10. SMTP Server
[Go to lesson](Go-Tools-SMTP-Client.md) [Go to lesson](Go-Tools-SMTP-Server.md)

The Simple Mail Transfer Protocol (SMTP) is used for sending and relaying emails. You will:
- Build an SMTP client to compose and send emails programmatically.
- Create an SMTP server to receive and route emails.
- Implement features like email attachments and authentication.

These projects explore the fundamentals of email communication.

---

### 11. Telnet Client & 12. Telnet Server
[Go to lesson](Go-Tools-Telnet-Client.md) [Go to lesson](Go-Tools-Telnet-Server.md)

Telnet provides text-based remote access to servers. You will:
- Implement a client to connect and communicate with Telnet servers.
- Build a server that handles remote sessions.
- Address security considerations for Telnet, such as plain-text communication risks.

These tools introduce the basics of terminal-based remote communication.

---

### 13. SSH Client & 14. SSH Server
[Go to lesson](Go-Tools-SSH-Client.md) [Go to lesson](Go-Tools-SSH-Server.md)

SSH (Secure Shell) offers secure remote access. In these modules, you will:
- Create an SSH client to authenticate and execute remote commands.
- Build a secure SSH server for managing remote sessions.
- Implement features like key-based authentication.

These tools are crucial for secure remote administration and automation.

---

### 15. DNS Client & 16. DNS Server
[Go to lesson](Go-Tools-DNS-Client.md) [Go to lesson](Go-Tools-DNS-Server.md)

DNS translates domain names into IP addresses. You will:
- Build a client to query DNS records (A, MX, TXT, etc.).
- Create a server to handle and resolve DNS requests.
- Explore caching and load balancing techniques.

This project provides insight into domain resolution and traffic management.

---

### 17. DHCP Client & 18. DHCP Server
[Go to lesson](Go-Tools-DHCP-Client.md) [Go to lesson](Go-Tools-DHCP-Server.md)

DHCP dynamically assigns IP addresses to devices on a network. You will:
- Implement a DHCP client to request and renew IP leases.
- Build a DHCP server to allocate and manage IP addresses.
- Handle address conflicts and lease expiration.

These tools demonstrate how networks dynamically configure devices.

---

### 19. VPN Client & 20. VPN Server
[Go to lesson](Go-Tools-VPN-Client.md) [Go to lesson](Go-Tools-VPN-Server.md)

VPNs (Virtual Private Networks) secure communication over untrusted networks. You will:
- Build a client to connect to VPN servers and establish secure tunnels.
- Create a server to manage VPN connections.
- Implement encryption and routing for secure data transmission.

These projects explore advanced networking concepts like tunneling and security.

---

## Why This Section Matters

By the end of this section, you will have gained:
- A deep understanding of client-server communication.
- Proficiency in implementing a wide range of network protocols.
- The ability to build secure, reliable, and scalable network services.

These skills are essential for modern application development and prepare you for the final stage of the course: **Security Tools**.
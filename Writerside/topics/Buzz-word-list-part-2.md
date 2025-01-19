# Buzz word list part 2

<include from="_ai.md" element-id="disclaimer" />

### 6. DHCP (Dynamic Host Configuration Protocol)

#### Introduction (DHCP)
**DHCP** is a network protocol used to automatically assign IP addresses to devices within a network. This eliminates the need for manual IP address configuration, simplifying network administration.

#### How DHCP Works
When a device (such as a computer or smartphone) connects to a network, it sends a broadcast message requesting an IP address. A DHCP server responds with an available IP address, subnet mask, gateway, and DNS settings. The device then configures itself with the provided information and can begin communicating on the network.

#### Example of DHCP:
- Your home router often acts as a DHCP server, assigning IP addresses like `192.168.0.100` to devices that connect to the Wi-Fi.

---

### 7. Router

#### Introduction (Router)
A **router** is a networking device that forwards data packets between different networks. It helps direct traffic from one network to another based on IP addresses, typically between a local network (LAN) and a wide-area network (WAN) such as the internet.

#### Functions of a Router
- **Routing**: A router examines the destination IP address of incoming data packets and determines the best route for them to travel.
- **Firewall**: Some routers come with built-in firewall features to filter traffic.
- **Network Address Translation (NAT)**: Routers often use NAT to allow multiple devices in a local network to share a single public IP address.

#### Example of a Router:
- Your home router routes internet traffic between your local devices (e.g., laptops, smartphones) and the internet.

---

### 8. Switch

#### Introduction (Switch)
A **switch** is a network device that connects devices within a LAN, forwarding data packets based on MAC addresses. Unlike a hub, which broadcasts data to all connected devices, a switch sends data only to the specific device it’s intended for.

#### How a Switch Works
When a switch receives a data packet, it looks at the destination MAC address and forwards the packet to the appropriate device within the network. Switches operate at the Data Link Layer (Layer 2) of the OSI model.

#### Example of a Switch:
- In a corporate office, a switch connects multiple computers, printers, and servers, ensuring that data is sent only to the device that needs it.

---

### 9. Hub

#### Introduction (Hub)
A **hub** is a simple networking device that connects multiple devices in a LAN. Unlike a switch, a hub broadcasts incoming data to all devices, even those not intended to receive the data.

#### How Hubs Work
Hubs transmit data packets to all devices connected to them, regardless of the destination address. This can lead to network inefficiency and increased collisions.

#### Example of a Hub:
- Hubs were once commonly used in home and office networks but have been largely replaced by more efficient switches.

---

### 10. Bridge

#### Introduction (Bridge)
A **bridge** is a networking device that connects two or more separate network segments and filters traffic based on MAC addresses. Bridges operate at the Data Link Layer (Layer 2) of the OSI model and can help reduce network traffic by segmenting the network.

#### How a Bridge Works
A bridge receives data from one network segment and forwards it to the appropriate segment based on the MAC address, improving network performance and reducing collisions.

#### Example of a Bridge:
- A bridge can be used to connect two LANs in different buildings, ensuring devices on both networks can communicate.

---

### 11. Firewall

#### Introduction (Firewall)
A **firewall** is a security device that monitors and controls the incoming and outgoing network traffic based on predetermined security rules. Firewalls can be hardware-based, software-based, or a combination of both.

#### Types of Firewalls
- **Packet-filtering firewalls**: Examine packets for specific attributes like IP addresses and ports.
- **Stateful firewalls**: Keep track of the state of active connections and make decisions based on connection context.
- **Proxy firewalls**: Act as intermediaries between clients and servers, providing an additional layer of security.

#### Example of a Firewall:
- A company may deploy a firewall to block unauthorized access to its internal network from external sources.

---

### 12. Proxy Server

#### Introduction (Proxy Server)
A **proxy server** is an intermediary server that sits between a client (e.g., a user’s computer) and a destination server (e.g., a website). It can be used to improve security, filter content, and improve performance by caching data.

#### How Proxy Servers Work
When a client makes a request (e.g., requesting a webpage), the proxy server forwards the request to the destination server. The destination server responds to the proxy, which then sends the response back to the client.

#### Example of a Proxy Server:
- A company might use a proxy server to restrict access to certain websites or to hide its internal network from the internet for security reasons.

---

### 13. VPN (Virtual Private Network)

#### Introduction (VPN)
A **VPN** creates a secure, encrypted connection between two networks or between a device and a network over the internet. It ensures that data transmitted over public networks remains private and secure.

#### How VPNs Work
A VPN establishes a secure tunnel for data by encrypting it before transmission. This ensures that even if the data is intercepted, it cannot be read without the decryption key.

#### Example of a VPN:
- When accessing corporate resources remotely, employees use a VPN to securely connect to the company’s network over the internet.

---

### 14. ISP (Internet Service Provider)

#### Introduction (ISP)
An **ISP** is a company or organization that provides internet access to consumers and businesses. ISPs offer various services such as broadband, fiber, DSL, or wireless internet.

#### Role of an ISP
ISPs connect users to the internet, providing the necessary infrastructure and routing for data to travel to and from the internet.

#### Example of an ISP:
- Companies like Comcast, AT&T, and Verizon are ISPs that provide home internet services.

---

### 15. TCP/IP (Transmission Control Protocol/Internet Protocol)

#### Introduction (TCP/IP)
**TCP/IP** is a set of protocols that govern communication over the internet. TCP is responsible for ensuring reliable transmission of data, while IP handles the addressing and routing of data.

#### How TCP/IP Works
- **TCP** divides data into packets, ensures they are received in order, and handles retransmission in case of packet loss.
- **IP** provides the addressing and routing information, ensuring that packets reach the correct destination.

#### Example of TCP/IP:
- Web traffic (HTTP/HTTPS) relies on TCP/IP to ensure data is transmitted between web servers and browsers reliably.

---

### 16. HTTP (HyperText Transfer Protocol)

#### Introduction (HTTP)
**HTTP** is a protocol used for transferring web pages and resources on the internet. It defines how messages are formatted and transmitted between clients (such as web browsers) and servers.

#### How HTTP Works
When a user enters a website address, the browser sends an HTTP request to the server. The server responds with an HTTP response containing the requested data (such as a webpage).

#### Example of HTTP:
- When you access `https://www.example.com`, your browser uses HTTP to request the webpage from the server hosting that domain.

---

### 17. HTTPS (HyperText Transfer Protocol Secure)

#### Introduction (HTTPS)
**HTTPS** is a secure version of HTTP. It uses SSL/TLS encryption to secure the communication between a client and a server, ensuring that data remains private and protected from eavesdropping.

#### How HTTPS Works
- HTTPS adds an encryption layer to HTTP using SSL/TLS. This ensures that data transmitted between a web server and a browser is encrypted and protected from interception.

#### Example of HTTPS:
- When accessing banking websites or online stores, HTTPS ensures that personal and financial information remains secure.

---

### 18. FTP (File Transfer Protocol)

#### Introduction (FTP)
**FTP** is a standard network protocol used to transfer files between a client and a server over a TCP/IP network. It allows for uploading and downloading files.

#### How FTP Works
FTP operates on the client-server model. The client requests files from a server, and the server sends the requested files over the network.

#### Example of FTP:
- Website developers use FTP to upload files to a web server for hosting.

---

### 19. SMTP (Simple Mail Transfer Protocol)

#### Introduction (SMTP)
**SMTP** is the protocol used for sending email messages between servers. It is responsible for handling the email transmission process.

#### How SMTP Works
SMTP allows an email client to send messages to an SMTP server, which then routes the message to the recipient’s mail server for delivery.

#### Example of SMTP:
- An email client (like Outlook or Gmail) uses SMTP to send outgoing emails.

---

### 20. POP3 (Post Office Protocol version 3)

#### Introduction (POP3)
**POP3** is an email protocol used to retrieve emails from a mail server. It downloads emails to a local device and removes them from the server by default.

#### How POP3 Works
When an email client connects to the mail server, POP3 downloads all new emails to the client and removes them from the server, making them available for offline reading.

#### Example of POP3:
- Many users access their emails through POP3, where their messages are downloaded to their local devices.

# Basic Network Tools

In the first stage of this course, we will focus on building **Basic Network Tools**—fundamental utilities that are essential for diagnosing and troubleshooting network-related issues. These tools form the backbone of network administration and provide a strong foundation for understanding more advanced networking concepts.

Through this section, you will learn how to implement classic tools that interact with network protocols, execute basic commands, and retrieve essential information about hosts, networks, and connections. Each tool we build will be a hands-on project that introduces key features of Go, such as working with network sockets, handling input/output, and implementing concurrency for efficient execution.

---

## Tools We Will Build

### 1. Ping
[Go to lesson](Go-Tools-Ping.md)

The Ping tool sends ICMP echo requests to a target host and measures the response time. It is widely used to verify the availability and responsiveness of a host. In this module, you will:
- Learn how to send ICMP packets in Go.
- Measure round-trip time (RTT) for network communication.
- Handle timeouts and packet loss scenarios.

By the end, you'll have created a basic yet powerful utility to check the health of network connections.

---

### 2. Whois
[Go to lesson](Go-Tools-Whois.md)

Whois queries retrieve domain registration and ownership details. This tool is invaluable for network administrators and security professionals. You will:
- Understand how the Whois protocol works.
- Connect to Whois servers using TCP in Go.
- Parse and display registration details in a user-friendly format.

This project will enhance your understanding of text-based protocols and server communication.

---

### 3. Dig/nslookup
[Go to lesson](Go-Tools-Dig-nslookup.md)

Dig (Domain Information Groper) and Nslookup are tools for querying DNS records. These tools help you understand domain-to-IP resolution and DNS record types like A, MX, and TXT. You will:
- Use Go's standard libraries to interact with DNS servers.
- Parse and display DNS query responses.
- Explore practical use cases like troubleshooting DNS propagation.

These skills are critical for working with domain names and diagnosing DNS issues.

---

### 4. Traceroute
[Go to lesson](Go-Tools-Traceroute.md)

Traceroute maps the path packets take to reach a destination, showing intermediate hops along the way. This tool provides insights into network topology and potential bottlenecks. You will:
- Implement Traceroute using ICMP and/or UDP packets.
- Analyze and visualize packet routing paths.
- Handle varying TTL (Time-to-Live) values to trace each hop.

Creating this tool will deepen your understanding of packet routing and network debugging.

---

### 5. Netstat
[Go to lesson](Go-Tools-Netstat.md)

Netstat displays active network connections and their statuses. It is a versatile tool for monitoring network activity. You will:
- Learn to list open ports and active connections on your system.
- Implement filtering options for protocols (TCP, UDP) and states.
- Display connection details such as source/destination IPs and ports.

This project will familiarize you with socket programming and system-level networking concepts.

---

### 6. Netscan
[Go to lesson](Go-Tools-Netscan.md)

Network scanning involves discovering active hosts and devices on a network. This tool is useful for network mapping and monitoring. You will:
- Scan a given IP range to identify live hosts.
- Use techniques like ARP (Address Resolution Protocol) and ICMP pings.
- Optimize your tool for efficiency and scalability.

Building a network scanner will introduce you to concepts like subnetting and host discovery.

---

### 7. Ifinfo
[Go to lesson](Go-Tools-Ifinfo.md)

Ifinfo lists network interfaces and their associated IP addresses on a system. This tool provides valuable information for network configuration and troubleshooting. You will:
- Retrieve interface details using Go's `net` package.
- Display interface names, IP addresses, and other network settings.
- Enhance the tool with filtering and formatting options.
- Explore advanced features like MAC address retrieval and interface status.

By creating Ifinfo, you'll gain insights into network interface management and system-level networking.

---

### 8. Subsystem
[Go to lesson](Go-Tools-Subsystem.md)

Subsystem detection involves identifying technologies (e.g., web servers, programming languages) running on a remote host. This tool is useful for reconnaissance and security assessments. You will:
- Fetch HTTP headers from a URL to extract server information.
- Identify server software, versions, and other subsystems.
- Analyze response headers for clues about the target system.
- Extend the tool to detect common web technologies like PHP, Python, and more.

Building a Subsystem detector will sharpen your web security skills and deepen your understanding of HTTP headers.

---


By completing the "Basic Network Tools" section, you’ll not only gain practical experience in Go programming but also develop a deep appreciation for the utility and simplicity of these essential tools. This stage sets the foundation for building more complex and feature-rich applications in the subsequent sections.
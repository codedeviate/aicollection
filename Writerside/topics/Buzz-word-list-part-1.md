# Buzz word list part 1

<include from="_ai.md" element-id="disclaimer" />

### 1. **IP Address**

#### Introduction (IP Address)
An **IP address** (Internet Protocol address) is a unique identifier for devices connected to a network. It is necessary for devices to communicate with each other over the internet or within a local area network (LAN). Every device, whether it's a computer, smartphone, or printer, requires an IP address to send and receive data.

#### Types of IP Addresses
There are two primary types of IP addresses:
- **IPv4 (Internet Protocol Version 4)**: This is the older version of the protocol and uses a 32-bit address format (e.g., 192.168.1.1). It provides around 4 billion unique addresses, which are now being exhausted due to the growing number of devices on the internet.
- **IPv6 (Internet Protocol Version 6)**: IPv6 uses a 128-bit address format (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334), providing a vastly larger address space, making it future-proof as IPv4 addresses run out.

#### How IP Addresses Work
An IP address serves two main functions:
1. **Host or network identification**: It identifies the source or destination of data in a network.
2. **Location addressing**: It provides information about where a device is located within a network.

#### Example of an IP Address:
- A computer in your office might have the IP address `192.168.0.101`. This address allows other devices on the same network to communicate with it.

---

### 2. **Netmask**

#### Introduction (Netmask)
A **netmask** (also called a subnet mask) is a 32-bit address used to divide an IP address into two parts: one part identifying the network and the other part identifying the host. Netmasks are essential for creating **subnets** within a network.

#### How Netmask Works
The netmask operates by "masking" a portion of the IP address to identify which part of the address represents the network. For example, a common netmask is `255.255.255.0`. The first three octets (`255.255.255`) specify the network, while the last octet (`0`) is used to define the host range.

#### Example of Netmask:
- **IP Address**: `192.168.1.5`
- **Netmask**: `255.255.255.0`
    - The network portion is `192.168.1`.
    - The host portion is `5`.

#### Importance:
- Netmasks help route packets within networks, directing them to the correct subnet.
- By splitting a network into smaller subnets, organizations can reduce congestion and improve security.

---

### 3. **Gateway**

#### Introduction (Gateway)
A **gateway** is a network device that acts as an intermediary between different networks, enabling data to flow from one network to another. It is typically used to connect a local network (LAN) to a larger network, such as the internet (WAN).

#### Function of a Gateway
Gateways route traffic from one network to another. They work by examining the destination IP address of a packet and forwarding it to the correct network. In home networks, the router usually serves as the gateway.

#### Example of a Gateway:
- In a home network, the gateway might be your router, which connects your local devices (PC, smartphone, etc.) to the internet.

#### Types of Gateways:
1. **Default Gateway**: This is the gateway used by devices when they need to communicate with devices outside their local network.
2. **Network Gateway**: It connects two distinct networks and translates data from one protocol to another, such as from an IP-based network to a Frame Relay network.

---

### 4. **DNS (Domain Name System)**

#### Introduction (DNS)
The **Domain Name System** (DNS) is the system that translates domain names, such as `www.example.com`, into IP addresses, such as `192.168.1.1`. DNS acts as the "phonebook" of the internet, enabling users to access websites using human-readable names instead of complex numerical IP addresses.

#### How DNS Works
When you type a web address into your browser, the browser sends a query to a DNS server. The DNS server looks up the IP address associated with the domain name and returns it. The browser then uses this IP address to connect to the website's server and retrieve the requested content.

#### Example of DNS:
- If you enter `www.google.com` in your browser, DNS will resolve this to an IP address (such as `142.250.72.238`) to allow your browser to make a connection.

#### DNS Records:
DNS uses different types of records to store information:
- **A Record**: Maps a domain name to an IP address (IPv4).
- **AAAA Record**: Maps a domain name to an IPv6 address.
- **MX Record**: Specifies the mail server for a domain.
- **CNAME Record**: Provides an alias for a domain.

---

### 5. **Subnet**

#### Introduction (Subnet)
A **subnet** is a smaller network that is part of a larger network. Subnets are used to partition networks for better organization, improved performance, and enhanced security.

#### Purpose of Subnetting
Subnetting is used to divide a large network into smaller, manageable segments. This can help reduce network congestion, improve network performance, and provide better control over traffic. Additionally, subnets can be used for security purposes by isolating traffic within different segments.

#### Example of Subnetting:
- A company with a large IP range, such as `192.168.1.0/24`, can subnet this into multiple smaller subnets like `192.168.1.0/26`, `192.168.1.64/26`, etc. Each subnet will have its own range of IP addresses.

#### Subnet Mask:
A subnet mask is used to define the size of a subnet. The netmask `255.255.255.0` means that the first three octets are used for the network, and the last octet is used for host addresses.


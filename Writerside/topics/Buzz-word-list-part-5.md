# Buzz word list part 5

<include from="_ai.md" element-id="disclaimer" />

### 56. **Non-Root Admin User**

#### Introduction (Non-Root Admin User)
A **non-root admin user** is a user account in a Unix-like operating system (such as Linux) that has administrative privileges, but is not the root user. This account can perform tasks like installing software or modifying system settings but does not have the unrestricted access that the root account has.

#### How It Works (Non-Root Admin User)
Non-root admin users are typically granted administrative privileges using `sudo`, which allows them to execute certain commands with elevated permissions when necessary.

#### Example (Non-Root Admin User):
- A non-root admin user might be allowed to add users or change system configurations, but they would need to use `sudo` to gain root-level access for critical tasks like system updates.

---

### 57. **Root User**

#### Introduction (Root User)
The **root user** is the highest level of user in Unix-like operating systems. It has unrestricted access to all commands, files, and resources on the system.

#### How It Works (Root User)
The root user can perform any action on the system, from installing software to modifying system files and configurations. Due to the high level of access, it is typically recommended to use the root account sparingly to minimize the risk of accidental system damage.

#### Example (Root User):
- The root user can add or remove users, change system configurations, or alter system files that are inaccessible to other users.

---

### 58. **Sudo**

#### Introduction (Sudo)
**Sudo** (SuperUser Do) is a command-line utility that allows a permitted user to execute a command as the root user or another user. It is commonly used in Unix-like systems to grant administrative privileges to non-root users.

#### How It Works (Sudo)
When a user issues a command with `sudo`, the system asks for the user’s password to confirm their identity. If the user is authorized, the command is executed with elevated privileges.

#### Example (Sudo):
- A non-root user may use `sudo apt-get update` to update the system, as the task requires administrative access.

---

### 59. **Su (Substitute User)**

#### Introduction (Su)
The `su` (substitute user) command is used in Unix-like systems to switch users or elevate to the root user. The most common usage is `su` alone, which switches to the root user.

#### How It Works (Su)
When you run `su`, you are prompted for the target user's password (root password for switching to the root user). After authentication, you gain the privileges of that user, allowing you to execute commands as them.

#### Example (Su):
- Running `su` and entering the root password allows you to perform system-wide administrative tasks.

---

### 60. **Passwd**

#### Introduction (Passwd)
The `passwd` command is used to change a user's password in Unix-like operating systems. It allows both regular users to change their own password and administrators (root) to change others' passwords.

#### How It Works (Passwd)
When a user runs `passwd`, they are prompted to enter their current password (for security) and then the new password. The system then updates the password hash in the system files.

#### Example (Passwd):
- A user might run `passwd` to change their password to something more secure.

---

### 61. **Systemctl**

#### Introduction (Systemctl)
`systemctl` is a command used to interact with the systemd system and service manager. It is used to manage services (start, stop, restart) and control the system’s initialization process.

#### How It Works (Systemctl)
With `systemctl`, you can control system services and manage the system's state. For example, you can start or stop network services, reboot the system, or change the system’s run level.

#### Example (Systemctl):
- To restart a service like Apache, you can use `sudo systemctl restart apache2`.

---

### 62. **Journalctl**

#### Introduction (Journalctl)
`journalctl` is a command used to query and view logs that are managed by `systemd`'s journal service. It allows users and administrators to view logs related to system services, kernel events, and user processes.

#### How It Works (Journalctl)
`journalctl` can display logs, filter them based on time, service, or severity, and even monitor logs in real-time as they are generated.

#### Example (Journalctl):
- Running `journalctl -u apache2` shows logs related to the Apache service.

---

### 63. **/etc/shadow**

#### Introduction (Shadow File)
The **/etc/shadow** file in Unix-like systems stores user password information and other security-related data. It contains the password hashes and details about password expiration.

#### How It Works (Shadow File)
Only privileged users (such as root) can read the contents of `/etc/shadow`. The file contains one line per user account, with information like the password hash, last password change date, and password expiration policy.

#### Example (Shadow File):
- Administrators can view the `/etc/shadow` file to check password expiration dates or modify user account settings.

---

### 64. **/etc/passwd**

#### Introduction (Passwd File)
The **/etc/passwd** file is a system file that contains essential information about user accounts on the system, including usernames, user IDs (UIDs), and group IDs (GIDs).

#### How It Works (Passwd File)
This file allows system processes to access basic user information such as the username, login shell, home directory, and account expiration date.

#### Example (Passwd File):
- The `/etc/passwd` file is used by various system utilities to determine user details and authentication.

---

### 65. **/etc/group**

#### Introduction (Group File)
The **/etc/group** file contains information about user groups in Unix-like systems. It lists group names, group IDs (GIDs), and the users who belong to each group.

#### How It Works (Group File)
Each line in the file corresponds to a group and includes the group’s name, GID, and a comma-separated list of usernames.

#### Example (Group File):
- If a user belongs to the `admin` group, their name would appear in the `admin` entry in `/etc/group`.

---

### 66. **/etc/sudoers**

#### Introduction (Sudoers File)
The **/etc/sudoers** file defines the sudo privileges for users and groups. It determines which users can execute commands as root or other users and under what conditions.

#### How It Works (Sudoers File)
The `/etc/sudoers` file is read by the `sudo` command to check whether a user is allowed to run a particular command with elevated privileges. It also contains security configurations like timestamp settings.

#### Example (Sudoers File):
- An entry like `john ALL=(ALL) ALL` would allow the user `john` to run any command as any user, including root.

---

### 67. **/etc/hosts**

#### Introduction (Hosts File)
The **/etc/hosts** file is used to map hostnames to IP addresses on Unix-like systems. It is part of the system’s local name resolution mechanism, providing a simple way to resolve hostnames before querying DNS.

#### How It Works (Hosts File)
When an application or user requests to connect to a hostname, the system first checks `/etc/hosts` to see if the name is mapped to an IP address. If no entry exists, it will query a DNS server.

#### Example (Hosts File):
- You might add an entry to `/etc/hosts` to map a custom hostname to an IP address for local testing: `127.0.0.1 mywebsite.local`.

---

### 68. **/etc/resolv.conf**

#### Introduction (Resolv.conf File)
The **/etc/resolv.conf** file in Unix-like systems contains DNS server information. It defines the nameservers that should be used to resolve domain names into IP addresses.

#### How It Works (Resolv.conf File)
The file typically includes one or more `nameserver` entries, each pointing to the IP address of a DNS server that will be used for name resolution.

#### Example (Resolv.conf File):
- A typical `/etc/resolv.conf` file might contain entries like `nameserver 8.8.8.8` for Google's public DNS.

---

### 69. **/etc/network/interfaces**

#### Introduction (Network Interfaces File)
The **/etc/network/interfaces** file in Debian-based Linux distributions is used to configure network interfaces. It contains settings such as static IP addresses, DHCP configurations, and more.

#### How It Works (Network Interfaces File)
When the system boots, the settings in `/etc/network/interfaces` are applied to configure the network interfaces, enabling connectivity to local networks or the internet.

#### Example (Network Interfaces File):
- A typical entry might look like:
  ```
  iface eth0 inet static
      address 192.168.1.100
      netmask 255.255.255.0
      gateway 192.168.1.1
  ```

---

### 70. **/etc/hostname**

#### Introduction (Hostname File)
The **/etc/hostname** file contains the system's hostname, which is the name that identifies the machine on a network.

#### How It Works (Hostname File)
This file holds a single line that contains the system’s hostname. This name is used by networking tools and system processes to identify the machine in a networked environment.

#### Example (Hostname File):
- An entry might be `myserver` to assign the hostname "myserver" to the system.

---

### 71. **Motd (Message of the Day)**

#### Introduction (Motd)
The **motd** (Message of the Day) is a file that displays messages to users when they log in to a Unix-like system. These messages are often used to provide information or warnings.

#### How It Works (Motd)
The `/etc/motd` file is read when a user logs in via a terminal, and its contents are displayed. Administrators use this file to communicate important notices to users.

#### Example (Motd):
- A system administrator might use `/etc/motd` to display maintenance windows or login reminders.

---

### 72. **NDIS (Network Driver Interface Specification)**

#### Introduction (NDIS)
**NDIS** is a Microsoft specification for network drivers that allows network hardware to communicate with the operating system. It acts as an abstraction layer between the network device drivers and the network protocols.

#### How It Works (NDIS)
NDIS provides a standard interface for drivers, enabling network devices to be compatible with a range of network protocols. It is commonly used in Windows environments.

#### Example (NDIS):
- NDIS is used by network card drivers in Windows to facilitate communication between the network hardware and the operating system.


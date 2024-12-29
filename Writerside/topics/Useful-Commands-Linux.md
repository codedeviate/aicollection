# Linux Command Guide

Here’s a list of some of the most useful Linux commands, organized by purpose, with descriptions and examples.

---

## File and Directory Management
- **`ls`**: Lists files and directories.
    - **Example**: `ls -l` (detailed view with permissions and sizes)

- **`cd`**: Changes the current directory.
    - **Example**: `cd /home/user/Documents`

- **`mkdir`**: Creates a new directory.
    - **Example**: `mkdir new_folder`

- **`rm`**: Removes files or directories.
    - **Example**: `rm file.txt` (removes a file), `rm -r folder_name` (removes a directory and its contents)

- **`cp`**: Copies files or directories.
    - **Example**: `cp file.txt /backup/`

- **`mv`**: Moves or renames files or directories.
    - **Example**: `mv old_name.txt new_name.txt`

- **`pwd`**: Prints the current directory path.
    - **Example**: `pwd` (outputs the current working directory)

---

## File Viewing and Editing
- **`cat`**: Displays file content.
    - **Example**: `cat file.txt`

- **`less`**: Views file content one screen at a time.
    - **Example**: `less longfile.txt`

- **`head`**: Displays the first few lines of a file.
    - **Example**: `head -n 10 file.txt` (shows the first 10 lines)

- **`tail`**: Displays the last few lines of a file.
    - **Example**: `tail -n 10 file.txt` (shows the last 10 lines)

- **`nano`/`vim`**: Text editors for editing files.
    - **Example**: `nano file.txt` (opens a file for editing using Nano)

---

## File and Disk Management
- **`df`**: Shows disk space usage.
    - **Example**: `df -h` (shows human-readable sizes)

- **`du`**: Displays directory and file size.
    - **Example**: `du -sh folder_name` (shows size of a folder)

- **`find`**: Searches for files and directories.
    - **Example**: `find /home -name "file.txt"`

- **`locate`**: Quickly finds files using an indexed database.
    - **Example**: `locate file.txt`

- **`stat`**: Displays detailed information about a file.
    - **Example**: `stat file.txt`

- **`touch`**: Creates an empty file.
    - **Example**: `touch newfile.txt`

- **`ln`**: Creates links to files.
    - **Example**: `ln -s /path/to/file link_name`

- **`file`**: Determines file type.
    - **Example**: `file file.txt`
    - Read more about `file` [here](Useful-Commands-file.md).

---

## System Information
- **`top`/`htop`**: Displays running processes and system usage.
    - **Example**: `top` (real-time process monitoring)

- **`uname`**: Displays system information.
    - **Example**: `uname -a` (detailed system info)

- **`uptime`**: Shows how long the system has been running.
    - **Example**: `uptime`

- **`free`**: Shows memory usage.
    - **Example**: `free -h` (human-readable format)

- **`who`**: Lists users currently logged in.
    - **Example**: `who`

---

## Networking
- **`ping`**: Checks network connectivity to a host.
    - **Example**: `ping google.com`

- **`curl`/`wget`**: Downloads files from the internet.
    - **Example**: `curl -O http://example.com/file.txt`

- **`netstat`**: Displays network connections (deprecated, use `ss`).
    - **Example**: `netstat -tuln`

- **`ssh`**: Connects to a remote server via SSH.
    - **Example**: `ssh user@192.168.1.1`

---

## File Permissions
- **`chmod`**: Changes file permissions.
    - **Example**: `chmod 755 file.txt`

- **`chown`**: Changes file ownership.
    - **Example**: `chown user:group file.txt`

- **`ls -l`**: Shows detailed file permissions.
    - **Example**: `ls -l`

---

## Process Management
- **`ps`**: Displays running processes.
    - **Example**: `ps aux` (shows all processes)

- **`kill`**: Terminates processes by ID.
    - **Example**: `kill 1234` (kills process with ID 1234)

- **`jobs`**: Lists background jobs.
    - **Example**: `jobs`

- **`bg`/`fg`**: Resumes background jobs in the foreground or background.
    - **Example**: `fg %1` (brings job 1 to the foreground)

---

## Package Management (Varies by Distribution)
- **`apt-get`/`apt`**: For Debian-based systems (e.g., Ubuntu).
    - **Example**: `sudo apt update && sudo apt upgrade`

- **`yum`/`dnf`**: For Red Hat-based systems.
    - **Example**: `sudo yum install package_name`

- **`pacman`**: For Arch-based systems.
    - **Example**: `sudo pacman -S package_name`

---

## Archiving and Compression
- **`tar`**: Archives files.
    - **Example**: `tar -czvf archive.tar.gz folder_name`

- **`gzip`/`gunzip`**: Compresses or decompresses files.
    - **Example**: `gzip file.txt`, `gunzip file.txt.gz`

- **`zip`/`unzip`**: Compresses or decompresses zip files.
    - **Example**: `zip archive.zip file1 file2`

---

## Utilities
- **`man`**: Displays the manual for a command.
    - **Example**: `man ls`

- **`alias`**: Creates shortcuts for commands.
    - **Example**: `alias ll='ls -la'`

- **`echo`**: Prints text to the terminal.
    - **Example**: `echo "Hello, World!"`

- **`history`**: Shows the history of commands.
    - **Example**: `history`

- **`grep`**: Searches for patterns in files.
    - **Example**: `grep "error" log.txt`

---

## Peripheral and System Status Commands

### Hardware Information
- **`lscpu`**: Displays detailed CPU architecture information.
    - **Example**: `lscpu`

- **`lsblk`**: Lists information about block devices (disks, partitions, etc.).
    - **Example**: `lsblk`

- **`lspci`**: Lists all PCI devices and their details.
    - **Example**: `lspci`
    - Read more about `lspci` [here](Useful-Commands-lspci.md).

- **`lsusb`**: Lists USB devices connected to the system.
    - **Example**: `lsusb`

- **`lshw`**: Displays detailed information about the system's hardware (requires superuser privileges).
    - **Example**: `sudo lshw`

### Disk and Storage
- **`blkid`**: Displays UUIDs and labels of storage devices.
    - **Example**: `blkid`

- **`fdisk`**: Partition table editor, useful for managing disk partitions.
    - **Example**: `sudo fdisk /dev/sda`

- **`parted`**: Advanced disk partitioning tool.
    - **Example**: `sudo parted /dev/sda`

- **`mount`**: Shows mounted filesystems.
    - **Example**: `mount`

- **`umount`**: Unmounts mounted filesystems.
    - **Example**: `umount /mnt`

### Memory and CPU
- **`free`**: Shows available and used memory (RAM and swap).
    - **Example**: `free -h`

- **`vmstat`**: Displays system performance statistics (memory, processes, I/O).
    - **Example**: `vmstat 5`

- **`mpstat`**: Displays CPU usage statistics (from the `sysstat` package).
    - **Example**: `mpstat`

- **`top`** / **`htop`**: Shows a real-time view of system processes and resource usage.
    - **Example**: `top`, `htop`

### Network and Devices
- **`ifconfig`** (deprecated, replaced by `ip`): Displays network interfaces and their configurations.
    - **Example**: `ifconfig`

- **`ip addr`**: Shows IP address configuration for network interfaces.
    - **Example**: `ip addr`

- **`ip link`**: Displays information about network links/devices.
    - **Example**: `ip link`

- **`ethtool`**: Displays or changes Ethernet device settings.
    - **Example**: `ethtool eth0`

- **`iwconfig`**: Shows or configures wireless network interfaces.
    - **Example**: `iwconfig wlan0`

- **`ping`**: Tests network connectivity to a host.
    - **Example**: `ping google.com`

- **`ss`**: Displays active network connections and listening ports.
    - **Example**: `ss -tuln`

- **`netstat`**: Shows network connections, routing tables, and interface statistics.
    - **Example**: `netstat -rn`

- **`route`**: Displays or modifies the IP routing table.
    - **Example**: `route -n`

- **`traceroute`**: Traces the route
    - **Example**: `traceroute google.com`

- **`mtr`**: Combines `ping` and `traceroute` functionality.
    - **Example**: `mtr google.com`

- **`arp`**: Displays or modifies the ARP cache.
    - **Example**: `arp -a`

- **`hostname`**: Shows the system's hostname.
    - **Example**: `hostname`

- **`dig`**: DNS lookup utility.
    - **Example**: `dig example.com`

- **`nslookup`**: Another DNS lookup utility.
    - **Example**: `nslookup example.com`

### System Logs and Status
- **`dmesg`**: Displays kernel message buffer, useful for diagnosing hardware issues.
    - **Example**: `dmesg | grep error`

- **`journalctl`**: Views systemd logs, including boot logs and service-related information.
    - **Example**: `journalctl -xe`

- **`uptime`**: Shows how long the system has been running and the load average.
    - **Example**: `uptime`

- **`sysctl`**: Views or modifies kernel parameters at runtime.
    - **Example**: `sysctl -a`

- **`iostat`**: Displays CPU, I/O, and disk usage statistics (from the `sysstat` package).
    - **Example**: `iostat`

### Battery and Power
- **`acpi`**: Shows battery status and AC adapter information (requires `acpi` package).
    - **Example**: `acpi`

- **`upower -i`**: Displays detailed battery information.
    - **Example**: `upower -i /org/freedesktop/UPower/devices/battery_BAT0`

- **`powertop`**: Analyzes power usage and suggests optimizations.
    - **Example**: `sudo powertop`


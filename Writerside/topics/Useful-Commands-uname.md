# uname

The `uname` command is a standard Unix utility used to display system information. It provides details about the operating system, kernel version, and hardware architecture.

## How `uname` Works

The `uname` command retrieves information from the system's kernel and displays it. It can show various pieces of information depending on the options used.

## Key Features

- **Basic Usage**: By default, `uname` displays the operating system name.
- **Options**:
    - `-a`: Displays all available system information.
    - `-s`: Displays the kernel name.
    - `-n`: Displays the network node hostname.
    - `-r`: Displays the kernel release.
    - `-v`: Displays the kernel version.
    - `-m`: Displays the machine hardware name.
    - `-p`: Displays the processor type (if available).
    - `-i`: Displays the hardware platform (if available).
    - `-o`: Displays the operating system.

## Example Usage

```sh
# Basic usage
uname

# Display all system information
uname -a

# Display the kernel name
uname -s

# Display the network node hostname
uname -n

# Display the kernel release
uname -r

# Display the kernel version
uname -v

# Display the machine hardware name
uname -m

# Display the processor type
uname -p

# Display the hardware platform
uname -i

# Display the operating system
uname -o
```

## Supported Systems

The `uname` command is available on most Unix-like operating systems, including:

- **Linux**: Commonly available on various Linux distributions.
- **macOS**: Included in macOS by default.
- **FreeBSD**: Available as part of the base system.
- **NetBSD**: Included in the base system.
- **OpenBSD**: Part of the base system.

It is not natively available on Windows, but similar functionality can be achieved using third-party tools like Cygwin or Windows Subsystem for Linux (WSL).
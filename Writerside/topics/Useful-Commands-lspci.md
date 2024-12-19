# lspci

`lspci` is a command-line utility in Unix-like operating systems that displays detailed information about all PCI (Peripheral Component Interconnect) buses and devices in the system. It is part of the `pciutils` package.

## How `lspci` Works

1. **Scanning PCI Buses**: `lspci` scans the PCI buses in the system to identify all connected PCI devices. It reads the PCI configuration space of each device to gather information.
2. **Reading Configuration Space**: The PCI configuration space contains registers that provide details about the device, such as vendor ID, device ID, class code, and more.
3. **Decoding Information**: `lspci` decodes the raw data from the configuration space into human-readable information. It uses a database of known vendor and device IDs to provide meaningful names.
4. **Displaying Information**: The utility displays the information in a structured format, showing details like the bus number, device number, function number, vendor, device name, and more.

## Key Features

- **Basic Information**: By default, `lspci` shows a summary of each PCI device.
- **Detailed Information**: Using the `-v` (verbose) option, `lspci` provides more detailed information about each device.
- **Tree View**: The `-t` option displays the devices in a tree format, showing the hierarchy of buses and devices.
- **Database Lookup**: The `-nn` option includes both numeric and textual IDs for vendors and devices.
- **Kernel Drivers**: The `-k` option shows the kernel drivers handling each device.

## Example Usage

```sh
# Basic usage
lspci

# Verbose output
lspci -v

# Tree view
lspci -t

# Include numeric and textual IDs
lspci -nn

# Show kernel drivers
lspci -k
```

## Supported Systems

`lspci` works on Unix-like operating systems, including:

- **Linux**: Commonly used on various Linux distributions.
- **FreeBSD**: Available as part of the `pciutils` package.
- **NetBSD**: Supported with the `pciutils` package.
- **OpenBSD**: Available with the `pciutils` package.

It is not natively available on Windows or macOS, but similar functionality can be achieved using other tools specific to those operating systems.
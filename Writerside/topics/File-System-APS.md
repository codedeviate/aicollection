# APS (Apple Partition Scheme)

APS, or the Apple Partition Scheme, is a disk partitioning scheme used in older Apple Macintosh systems. It predates the modern GUID Partition Table (GPT) and is specifically designed to manage storage devices in systems running classic Mac OS and early versions of macOS. Here's a detailed look at APS and its features:

---

## Structure of the APS Partition Scheme

### 1. Partition Map:
The partition map is the core of the APS structure:

- **Partition Map Block**:
    - Contains metadata about each partition on the disk.
- **Partition Entries**:
    - Describe individual partitions, including their type, size, and location.

### 2. Partition Types:
APS supports multiple partition types:

- **HFS (Hierarchical File System)**:
    - The primary file system used for data storage.
- **Driver Partitions**:
    - Contain firmware or drivers required for the system to access the disk.
- **Free Partitions**:
    - Reserved space for future use or unallocated space.

### 3. Boot Blocks:
Located at the beginning of the disk, boot blocks contain essential information for system startup:

- **Boot Code**:
    - Instructions for loading the operating system.
- **System Identifier**:
    - Indicates the operating system compatible with the partition.

### 4. Endianess:
APS uses big-endian format, consistent with the architecture of classic Macintosh systems.

---

## Features of APS

- **Backward Compatibility**:
    - Designed to work with classic Mac OS and early macOS versions.
- **Multiple Partition Support**:
    - Enables dividing a disk into multiple partitions for specific purposes.
- **Driver Storage**:
    - Stores disk drivers directly on the disk, ensuring compatibility with older hardware.
- **Simple Design**:
    - Straightforward partitioning scheme with minimal overhead.

---

## Limitations of APS

- **Obsolete**:
    - Replaced by GPT in modern macOS systems.
- **Volume Size Limitations**:
    - Limited to a maximum volume size of 2 TB.
- **Compatibility**:
    - Not supported by modern systems without emulation or legacy support.
- **No Redundancy**:
    - Lacks features like checksums or redundancy for error detection and recovery.

---

## Tools and Commands for APS

- **`pdisk`**:
    - A command-line utility for managing APS partitions.

- **Disk Utility**:
    - The graphical tool in macOS for partition management (legacy support for APS).

- **Third-Party Tools**:
    - Utilities like Drive Genius for advanced partition management.

---

## Example Usage

### Using pdisk:
```bash
# List existing partitions on a disk
sudo pdisk /dev/diskX -l

# Create a new partition
sudo pdisk /dev/diskX
Command (? for help): C

# Delete a partition
sudo pdisk /dev/diskX
Command (? for help): D
```

### Using Disk Utility:
1. Open Disk Utility.
2. Select the target disk.
3. Use the partitioning tool to create or modify APS partitions.

---

## Use Cases for APS

- **Classic Macintosh Systems**:
    - Used for managing storage in older Mac OS environments.
- **Retro Computing**:
    - Preferred by enthusiasts working with vintage Apple hardware.
- **Driver Storage**:
    - Essential for systems requiring on-disk drivers for booting.

---

APS was a foundational partitioning scheme for Apple systems, enabling flexible and reliable disk management during its era. While it has been replaced by GPT in modern systems, it remains significant in the history of file systems and is still relevant for vintage computing projects.
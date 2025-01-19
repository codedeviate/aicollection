# FATX (Xbox File Allocation Table)

FATX, or the Xbox File Allocation Table, is a file system developed by Microsoft for use on the original Xbox and Xbox 360 consoles. It is a derivative of the FAT (File Allocation Table) file system, modified to meet the specific requirements of gaming consoles. Here's a detailed look at FATX and its features:

---

## Structure of FATX

### 1. Partition Layout:
FATX partitions are structured to optimize gaming and system performance:

- **Boot Partition**:
    - Contains system files required to boot the Xbox console.
- **Game Data Partition**:
    - Stores saved games, user profiles, and downloaded content.
- **Cache Partition**:
    - Provides temporary storage for cached game data.

### 2. Directory and File Structure:
FATX organizes files and directories with specific limitations:

- **Directory Entries**:
    - Metadata for files and directories, including name, size, and location.
- **File Naming**:
    - Supports up to 42 characters with a restricted character set.
- **File Size Limits**:
    - Individual files are limited to 4 GB.

### 3. Allocation Mechanism:
FATX uses a simplified file allocation table:

- **Cluster-Based Storage**:
    - Files are stored in clusters, with a table tracking cluster usage.
- **Fragmentation Handling**:
    - Designed to minimize fragmentation for consistent performance.

### 4. Compatibility:
FATX is specifically tailored for Xbox consoles and is not natively supported by most operating systems without third-party tools.

---

## Features of FATX

- **Optimized for Gaming**:
    - Designed to handle game data efficiently with minimal latency.
- **Simple Structure**:
    - Lightweight file system optimized for console hardware.
- **Fast Access Times**:
    - Reduces overhead for quick loading of game assets.
- **Partitioning for System Stability**:
    - Separates game data, system files, and cached content for better organization.

---

## Limitations of FATX

- **File Size Restrictions**:
    - Maximum file size of 4 GB due to its FAT roots.
- **Volume Size Limits**:
    - Cannot handle volumes larger than 2 TB.
- **Limited Compatibility**:
    - Requires specialized tools to access on non-Xbox platforms.
- **Lack of Advanced Features**:
    - No support for journaling, compression, or encryption.

---

## Tools and Commands for FATX

- **`FATXplorer`**:
    - A third-party tool for accessing and managing FATX partitions on a PC.

- **`xboxdrv`**:
    - A Linux driver that provides read-only access to FATX partitions.

- **`HDDHackr`**:
    - Used to modify non-Xbox drives for use with Xbox consoles.

---

## Example Usage

### Accessing FATX on a PC:
```bash
# Use FATXplorer to explore Xbox partitions
fatxplorer

# Mount a FATX partition (Linux with xboxdrv)
sudo mount -t fatx /dev/sdX /mnt/xbox

# Unmount the partition
sudo umount /mnt/xbox
```

---

## Use Cases for FATX

- **Gaming Consoles**:
    - Native file system for storing game data, profiles, and downloadable content on Xbox and Xbox 360.
- **Modding and Homebrew**:
    - Popular among enthusiasts for customizing and extending console functionality.
- **Data Recovery**:
    - Recovering lost or corrupted game data from Xbox drives.

---

FATX is a specialized file system tailored for Xbox consoles, balancing simplicity and performance for gaming environments. While it has limitations compared to modern file systems, its focused design serves the specific needs of the Xbox platform effectively.
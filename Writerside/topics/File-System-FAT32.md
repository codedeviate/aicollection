# FAT32 (File Allocation Table 32-bit)

FAT32 is an improved version of the FAT file system, designed to support larger storage devices and partitions compared to FAT16. It uses 32-bit entries in the File Allocation Table, allowing for a much larger number of clusters and greater storage capacity. Here's a breakdown of the FAT32 structure and how to interpret its contents:

---

## Structure of the FAT32 Header

The FAT32 file system header, located in the boot sector of the volume, typically contains the following fields:

1. **Boot Sector**:
    - **`Jump Instruction`** (3 bytes):
        - The initial instruction to jump to the boot code.
    - **`OEM Name`** (8 bytes):
        - Identifies the system that formatted the volume.
    - **`Bytes Per Sector`** (2 bytes):
        - Specifies the size of a sector (commonly 512 bytes).
    - **`Sectors Per Cluster`** (1 byte):
        - Specifies the number of sectors per cluster.
    - **`Reserved Sectors`** (2 bytes):
        - Number of sectors reserved for the boot record and FAT table.
    - **`Number of FATs`** (1 byte):
        - Number of FAT tables (usually 2 for redundancy).
    - **`Total Sectors`** (4 bytes):
        - Total number of sectors in the volume.
    - **`Media Descriptor`** (1 byte):
        - Describes the media type (e.g., `0xF8` for hard disks).
    - **`Sectors Per FAT`** (4 bytes):
        - Number of sectors occupied by each FAT table.
    - **`Sectors Per Track`** (2 bytes):
        - Number of sectors per track (for CHS addressing).
    - **`Number of Heads`** (2 bytes):
        - Number of heads (for CHS addressing).
    - **`Hidden Sectors`** (4 bytes):
        - Number of sectors before the start of the FAT volume.
    - **`Root Cluster`** (4 bytes):
        - Starting cluster number of the root directory.
    - **`FS Info`** (2 bytes):
        - Points to the FS Information Sector, which holds free cluster and next free cluster data.
    - **`Boot Code`**:
        - Bootstrapping code executed during system startup.

---

## FAT32 Table

The FAT32 table is a map of clusters on the disk. Each entry is 32 bits long and represents the status of a cluster:

- **Available Cluster**: Marked as `0x00000000`.
- **Reserved Cluster**: Reserved clusters have specific values (e.g., `0xFFFFFFF0` - `0xFFFFFFF6`).
- **Bad Cluster**: Marked as `0xFFFFFFF7`.
- **End-of-Cluster Chain**: Marked as `0xFFFFFFFF`.
- **Used Cluster**: Points to the next cluster in the chain.

---

## Directory Structure

Directories in FAT32 are stored as arrays of 32-byte directory entries:

1. **File Name** (8 bytes):
    - Contains the file name (padded with spaces if shorter).
2. **Extension** (3 bytes):
    - File extension.
3. **Attributes** (1 byte):
    - File attributes (e.g., read-only, hidden, system).
4. **Reserved** (10 bytes):
    - Reserved for future use.
5. **Time and Date** (4 bytes):
    - Time and date of file creation or modification.
6. **Starting Cluster** (4 bytes):
    - Starting cluster of the file's data.
7. **File Size** (4 bytes):
    - Size of the file in bytes.

---

## Finding Where Data Begins

To locate file data:

1. **Calculate the Data Region Offset**:
    - Use the formula:
      ```
      DataRegionOffset = ReservedSectors + (NumberOfFATs * SectorsPerFAT)
      ```
    - Unlike FAT16, the root directory in FAT32 is located in the data region and does not have a fixed size.

2. **Locate the Cluster**:
    - Use the starting cluster from the directory entry.
    - Follow the cluster chain in the FAT table to retrieve file data.

---

## Commands to Analyze FAT32 File Systems

- **`fsck.fat`**:
  Checks and repairs FAT32 file systems.

- **`fatcat`**:
  Extracts data from FAT32 partitions.

- **`mmls`**:
  Displays partition layouts, including FAT32.

- **`blkcat`**:
  Reads raw data from specific sectors.

---

## Example

```bash
# Display information about the FAT32 volume
fsck.fat -v /dev/sdX

# Extract data from the FAT32 file system
fatcat /dev/sdX

# Analyze the raw sectors
blkcat /dev/sdX 0 512

# Inspect partition layouts
mmls /dev/sdX
```

These tools can help you analyze FAT32 file systems and understand how files and directories are stored and accessed.


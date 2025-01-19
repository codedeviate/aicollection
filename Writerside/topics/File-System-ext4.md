# ext4 (Fourth Extended File System)

ext4 is a modern journaling file system for Linux, introduced as an improvement over ext3. It offers enhanced performance, scalability, and reliability while remaining backward compatible with ext3. Here's a detailed look at the ext4 file system and its features:

---

## Structure of the ext4 File System

### 1. Boot Sector:
The boot sector contains metadata about the file system, including:

- **`Inode Count`**:
    - Total number of inodes in the file system.
- **`Block Count`**:
    - Total number of blocks in the file system.
- **`Reserved Block Count`**:
    - Number of blocks reserved for the root user.
- **`Free Block Count`**:
    - Number of free blocks available.
- **`Free Inode Count`**:
    - Number of free inodes available.
- **`First Data Block`**:
    - Block number of the first data block.
- **`Block Size`**:
    - Size of each block (commonly 1024, 2048, or 4096 bytes).
- **`Journal Information`**:
    - Metadata related to the journaling feature.

### 2. Inode Structure:
Each file or directory in ext4 is represented by an inode, which contains:

- **File Type and Permissions**:
    - Indicates if it's a file, directory, or special type.
- **File Size**:
    - Size of the file in bytes.
- **Timestamps**:
    - Tracks file creation, modification, and access times with nanosecond precision.
- **Pointers to Data Blocks**:
    - Includes direct, indirect, double indirect, and triple indirect pointers to data blocks.

### 3. Directory Structure:
Directories are implemented as files containing a list of directory entries. Each entry includes:

- **Inode Number**:
    - Points to the inode representing the file or subdirectory.
- **Entry Length**:
    - Length of the directory entry.
- **File Name Length**:
    - Length of the file name.
- **File Name**:
    - The actual name of the file or subdirectory.

---

## Features of ext4

- **Backward Compatibility**:
    - Fully compatible with ext3; ext3 file systems can be converted to ext4.
- **Delayed Allocation**:
    - Optimizes block allocation to reduce fragmentation and improve performance.
- **Extents**:
    - Replaces traditional block mapping with extents, which describe a range of contiguous blocks.
- **Journal Checksumming**:
    - Protects the integrity of the journal by adding checksums.
- **Large File and Volume Support**:
    - Supports volumes up to 1 EB and files up to 16 TB (with appropriate block sizes).
- **64-bit Storage**:
    - Allows for larger files and file systems.
- **Multiblock Allocation**:
    - Allocates multiple blocks at once, improving performance for large files.

---

## Journaling Modes

1. **Writeback**:
    - Only metadata is journaled, offering high performance but lower reliability.
2. **Ordered** (default):
    - Metadata is journaled, and file data is written to disk before metadata updates.
3. **Journal**:
    - Both metadata and file data are journaled, providing maximum reliability.

---

## Tools and Commands for ext4

- **`fsck.ext4`**:
    - Checks and repairs ext4 file systems.

- **`mkfs.ext4`**:
    - Creates an ext4 file system.

- **`tune2fs`**:
    - Adjusts tunable file system parameters, such as enabling or disabling journaling.

- **`mount`**:
    - Mounts the ext4 file system, with options to specify journaling modes and features.

---

## Example

```bash
# Check and repair an ext4 file system
fsck.ext4 /dev/sdX

# Create an ext4 file system
mkfs.ext4 /dev/sdX

# Mount an ext4 file system with journaling mode
mount -o data=journal /dev/sdX /mnt

# Convert an ext3 file system to ext4
tune2fs -O extents,uninit_bg,dir_index /dev/sdX
```

ext4 combines reliability with modern performance optimizations, making it a default choice for many Linux distributions.


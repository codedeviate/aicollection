# ISO 9660 (CD-ROM File System)

ISO 9660 is an international standard file system designed for optical disc media, such as CD-ROMs. It ensures compatibility across different operating systems, enabling consistent data access on various platforms. Here's a detailed look at ISO 9660 and its features:

---

## Structure of the ISO 9660 File System

### 1. Primary Volume Descriptor (PVD):
The PVD contains metadata about the file system:

- **`Volume Identifier`**:
    - The name of the volume as displayed to the user.
- **`Volume Space Size`**:
    - Total number of logical blocks in the file system.
- **`Logical Block Size`**:
    - Size of each block, typically 2048 bytes.
- **`Root Directory Record`**:
    - Points to the root directory of the file system.
- **`Path Table`**:
    - Provides a quick lookup mechanism for directory paths.

### 2. Directory Structure:
ISO 9660 organizes files and directories in a hierarchical structure:

- **Root Directory**:
    - Contains all files and subdirectories.
- **Directory Entries**:
    - Each entry stores metadata such as file name, size, and location.
- **Levels of Compliance**:
    - Supports different levels (Level 1, 2, and 3) for varying file name lengths and directory depths.

### 3. File Naming:
ISO 9660 imposes strict naming conventions:

- **Level 1**:
    - File names are limited to 8 characters, a period, and a 3-character extension (e.g., `FILE.TXT`).
- **Level 2**:
    - Allows file names up to 31 characters.
- **Level 3**:
    - Permits fragmented files for improved compatibility.

### 4. Extensions:
ISO 9660 can be extended with additional specifications for enhanced functionality:

- **Joliet**:
    - Adds support for Unicode file names and longer file name lengths.
- **Rock Ridge**:
    - Provides POSIX-compatible metadata, such as permissions and symbolic links.

---

## Features of ISO 9660

- **Cross-Platform Compatibility**:
    - Ensures consistent data access across different operating systems.
- **Hierarchical Structure**:
    - Supports directories and subdirectories for organized storage.
- **Extensibility**:
    - Allows extensions like Joliet and Rock Ridge for enhanced functionality.
- **Standardized Block Size**:
    - Optimized for optical media with a typical block size of 2048 bytes.

---

## Limitations of ISO 9660

- **File Name Restrictions**:
    - Strict naming conventions limit file name length and character usage.
- **No Journaling**:
    - Lacks features for ensuring metadata consistency.
- **Limited Scalability**:
    - Designed for optical media, with limitations on file sizes and volume capacity.
- **Read-Only**:
    - Primarily designed for read-only media, although write-once extensions exist.

---

## Tools and Commands for ISO 9660

- **`mkisofs`**:
    - Creates an ISO 9660 file system image.

- **`mount`**:
    - Mounts an ISO 9660 volume for access.

- **`isoinfo`**:
    - Displays information about ISO 9660 images.

- **`dd`**:
    - Copies ISO images to storage devices.

---

## Example Usage

```bash
# Create an ISO 9660 file system image
mkisofs -o mydisk.iso /path/to/files

# Mount an ISO 9660 file system
mount -o loop mydisk.iso /mnt

# Display information about an ISO 9660 image
isoinfo -d -i mydisk.iso

# Copy an ISO image to a device
dd if=mydisk.iso of=/dev/sdX bs=4M
```

ISO 9660 remains a widely used standard for optical media, ensuring compatibility and reliability across platforms. Its extensibility with specifications like Joliet and Rock Ridge allows it to meet modern needs while retaining backward compatibility. 
# NTFS (New Technology File System)

NTFS is a robust and modern file system introduced by Microsoft with Windows NT. It supports large storage devices, advanced metadata, security features, and file system journaling. Here's a breakdown of the NTFS structure and how to interpret its contents:

---

## Structure of the NTFS Header

The NTFS file system header, located in the boot sector of the volume, typically contains the following fields:

1. **Boot Sector**:
    - **`Jump Instruction`** (3 bytes):
        - The initial instruction to jump to the boot code.
    - **`OEM ID`** (8 bytes):
        - Identifies the file system as NTFS.
    - **`Bytes Per Sector`** (2 bytes):
        - Specifies the size of a sector (commonly 512 or 4096 bytes).
    - **`Sectors Per Cluster`** (1 byte):
        - Specifies the number of sectors per cluster.
    - **`Reserved Sectors`** (2 bytes):
        - Reserved sectors, typically 0 for NTFS.
    - **`Media Descriptor`** (1 byte):
        - Describes the media type (e.g., `0xF8` for hard disks).
    - **`Total Sectors`** (8 bytes):
        - Total number of sectors in the volume.
    - **`MFT Cluster`** (8 bytes):
        - Starting cluster number of the Master File Table (MFT).
    - **`MFTMirr Cluster`** (8 bytes):
        - Starting cluster number of the MFT Mirror.
    - **`Clusters Per File Record Segment`** (1 byte):
        - Size of file record segments.
    - **`Clusters Per Index Buffer`** (1 byte):
        - Size of index buffers.
    - **`Volume Serial Number`** (8 bytes):
        - Unique identifier for the volume.
    - **`Boot Code`**:
        - Bootstrapping code executed during system startup.

---

## NTFS Metadata Files

NTFS uses a set of system files to manage its structure and metadata:

1. **`$MFT` (Master File Table)**:
    - Central database containing metadata for all files and directories.
    - Each file has a corresponding record in the MFT.

2. **`$MFTMirr` (MFT Mirror)**:
    - Backup of critical MFT records.

3. **`$LogFile`**:
    - Contains a transaction log for file system recovery.

4. **`$Bitmap`**:
    - Tracks the allocation status of clusters on the volume.

5. **`$Boot`**:
    - Contains the boot sector and boot code.

6. **`$BadClus`**:
    - Tracks bad clusters on the disk.

7. **`$Secure`**:
    - Stores security descriptors for files and directories.

---

## File Record Structure

Each file or directory in NTFS is represented by a record in the Master File Table (MFT):

1. **Header**:
    - Includes the signature `FILE`, update sequence number, and record size.

2. **Standard Information Attribute**:
    - Contains timestamps, file permissions, and flags.

3. **File Name Attribute**:
    - Stores the file name, parent directory reference, and name length.

4. **Data Attribute**:
    - Points to the actual file data, either stored directly in the MFT (resident) or in clusters (non-resident).

5. **Index Root and Allocation Attributes** (for directories):
    - Manage directory contents and indexing.

---

## NTFS Features

- **Journaling**:
    - NTFS uses a transaction log (`$LogFile`) to ensure file system consistency.
- **Security**:
    - Supports Access Control Lists (ACLs) for granular file permissions.
- **Compression and Encryption**:
    - Allows transparent compression and encryption of files.
- **Sparse Files**:
    - Supports efficient storage of large files with empty regions.
- **Hard Links and Reparse Points**:
    - Enables advanced file and directory management features.

---

## Commands to Analyze NTFS File Systems

- **`ntfsfix`**:
  Repairs minor NTFS inconsistencies.

- **`ntfsinfo`**:
  Displays detailed information about an NTFS volume.

- **`ntfsls`**:
  Lists files and directories in an NTFS partition.

- **`ntfsundelete`**:
  Recovers deleted files from an NTFS volume.

- **`mmls`**:
  Displays partition layouts, including NTFS.

---

## Example

```bash
# Display information about the NTFS volume
ntfsinfo /dev/sdX

# List files and directories in the NTFS partition
ntfsls /dev/sdX

# Recover deleted files from an NTFS partition
ntfsundelete /dev/sdX

# Inspect partition layouts
mmls /dev/sdX
```

These tools can help you analyze NTFS file systems and understand how files and directories are stored and accessed.


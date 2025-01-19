# File systems

This document provides a comprehensive list of file systems, including modern, legacy, and specialized ones used across different operating systems and storage devices.

---

## 1. Modern File Systems

### Modern Windows:
- **NTFS (New Technology File System)**:
    - Robust, supports journaling, ACLs, and large volumes.
- **exFAT (Extended File Allocation Table)**:
    - Optimized for flash drives and supports large files without journaling.
- **FAT32 (File Allocation Table 32-bit)**:
    - Commonly used on portable drives and older systems.

### Modern Linux/Unix:
- **ext4 (Fourth Extended File System)**:
    - Widely used on Linux, supports journaling and large volumes.
- **XFS**:
    - High-performance journaling file system.
- **Btrfs (B-tree File System)**:
    - Features copy-on-write, snapshots, and self-healing.
- **ZFS (Zettabyte File System)**:
    - Known for scalability, data integrity, and snapshots.

### Modern macOS:
- **APFS (Apple File System)**:
    - Optimized for flash storage, supports snapshots and cloning.
- **HFS+ (Hierarchical File System Plus)**:
    - Older macOS file system, now replaced by APFS.

---

## 2. Legacy File Systems

### Legacy Windows:
- **FAT16 (File Allocation Table 16-bit)**:
    - Used on DOS and early Windows systems.
- **FAT12 (File Allocation Table 12-bit)**:
    - Designed for floppy disks and small storage devices.
- **HPFS (High-Performance File System)**:
    - Used on OS/2, briefly supported by Windows NT.

### Legacy Linux/Unix:
- **ext2 (Second Extended File System)**:
    - Predecessor to ext3, no journaling.
- **ext3 (Third Extended File System)**:
    - Added journaling to ext2.
- **ReiserFS**:
    - Journaling file system, popular in early Linux distributions.
- **UFS (Unix File System)**:
    - Common on older Unix systems.

### Legacy macOS:
- **MFS (Macintosh File System)**:
    - Original Mac file system, replaced by HFS.
- **HFS (Hierarchical File System)**:
    - Predecessor to HFS+.

---

## 3. Specialized File Systems

- **ISO 9660**:
    - Standard for optical disc media (CD/DVD).
- **UDF (Universal Disk Format)**:
    - Successor to ISO 9660, supports rewritable media.
- **JFFS2 (Journaling Flash File System 2)**:
    - Designed for flash memory.
- **YAFFS (Yet Another Flash File System)**:
    - Optimized for NAND flash.
- **F2FS (Flash-Friendly File System)**:
    - Designed specifically for flash storage.
- **tmpfs**:
    - Temporary file system stored in RAM.

---

## 4. Distributed File Systems

- **NFS (Network File System)**:
    - Allows file sharing across networks.
- **CIFS (Common Internet File System)**:
    - Used for file sharing in Windows environments.
- **AFS (Andrew File System)**:
    - Distributed file system with strong authentication.
- **CephFS**:
    - Scalable file system designed for distributed storage.
- **GlusterFS**:
    - High-performance, distributed file system.

---

## 5. Older or Niche File Systems

- **a.out**:
    - Early Unix executable format.
- **COFF (Common Object File Format)**:
    - Used in early Unix and embedded systems.
- **MZ (DOS Executable Format)**:
    - Used on DOS `.exe` files.
- **LE/LX**:
    - Used in OS/2 for device drivers.
- **PEF (Preferred Executable Format)**:
    - Used on classic Mac OS (PowerPC).
- **XCOFF (Extended COFF)**:
    - IBM AIX-specific file format.
- **FATX**:
    - Used on Xbox consoles.

---

## Example Commands for File System Analysis

- **`fsck`**:
    - Repairs file system inconsistencies.
- **`mount`**:
    - Mounts file systems for use.
- **`lsblk`**:
    - Lists information about block devices.
- **`file`**:
    - Identifies file types and formats.
- **`blkid`**:
    - Displays UUIDs and types of file systems on devices.

This list provides an overview of file systems and their contexts.


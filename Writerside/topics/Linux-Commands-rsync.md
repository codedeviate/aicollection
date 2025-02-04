# rsync

## Introduction to `rsync`

`rsync` is a powerful command-line tool for efficiently transferring and synchronizing files between two locations, either on the same machine or over a network. Unlike traditional file copy utilities, `rsync` minimizes data transfer by only copying the differences between the source and the destination, making it faster and more efficient, particularly when dealing with large files or directories.

Developed by Andrew Tridgell and Paul Mackerras, `rsync` is widely used for backups, file synchronization, and disaster recovery tasks. It’s especially useful for maintaining mirror copies of data and managing incremental backups.

---

## Basic Syntax of `rsync`

The basic syntax for using `rsync` is as follows:

```
rsync [options] source destination
```

- **source**: The source file or directory that you want to copy or synchronize.
- **destination**: The destination file or directory where you want the source to be copied.

Both the source and destination can be local or remote:
- **Local transfer**: `rsync /path/to/source /path/to/destination`
- **Remote transfer**: `rsync user@remotehost:/path/to/source /path/to/destination`

If you are transferring data over a network, `rsync` uses SSH by default for secure communication.

---

## Common `rsync` Examples

1. **Copying a File from Local to Remote**
   ```bash
   rsync -avz localfile.txt user@remotehost:/path/to/destination/
   ```
   This command will copy `localfile.txt` from the local machine to the remote machine, preserving file attributes and compressing the data during the transfer.

2. **Synchronizing Directories (Local to Remote)**
   ```bash
   rsync -avz /path/to/local/dir/ user@remotehost:/path/to/remote/dir/
   ```
   This command will synchronize the contents of the local directory with the remote directory, copying only the differences.

3. **Copying Files Between Two Remote Hosts**
   ```bash
   rsync -avz user1@remotehost1:/path/to/source/ user2@remotehost2:/path/to/destination/
   ```
   This will transfer files directly between two remote hosts, without involving the local machine.

4. **Dry Run to Preview the Changes**
   ```bash
   rsync -avzn /path/to/source/ /path/to/destination/
   ```
   The `-n` option makes `rsync` perform a dry run, which will show you what changes would be made without actually performing them.

---

## Detailed Explanation of `rsync` Flags (Options)

`rsync` offers a wide variety of flags and options to customize the file transfer process. Below is a detailed breakdown of the most commonly used flags.

### 1. -a (Archive Mode)

The `-a` flag enables "archive mode," which is a combination of several other flags. It is commonly used for backups or file synchronization as it ensures that file attributes (permissions, timestamps, symbolic links, etc.) are preserved.

Example:
```bash
rsync -a source/ destination/
```
This copies all files from the `source` directory to `destination`, maintaining permissions, symbolic links, and timestamps.

### 2. -v (Verbose)

The `-v` flag increases verbosity, making `rsync` print information about the file transfer process. This is particularly useful when troubleshooting or when you want to monitor the progress of the transfer.

Example:
```bash
rsync -avz source/ destination/
```
The `-v` will output detailed information about the files being transferred.

### 3. -z (Compression)

The `-z` flag compresses the data during the transfer. This is useful when transferring files over a slow network as it reduces the amount of data sent.

Example:
```bash
rsync -avz source/ user@remotehost:/path/to/destination/
```
This will copy the files from the local `source` directory to the remote destination while compressing the data during transfer.

### 4. -r (Recursive)

The `-r` flag copies directories recursively. This is necessary when transferring directories and subdirectories. While `-a` (archive mode) already includes recursion, `-r` can also be used by itself.

Example:
```bash
rsync -r source/ destination/
```
This command copies all files and directories from `source` to `destination`.

### 5. -n (Dry Run)

The `-n` flag performs a dry run, showing what actions would be taken without actually transferring any files. This is useful for previewing the changes and ensuring the command will work as expected.

Example:
```bash
rsync -avzn source/ destination/
```
This will display what files would be copied or updated, but no actual changes will be made.

### 6. --delete

The `--delete` flag removes files from the destination that are no longer present in the source directory. This is useful for maintaining a true mirror of the source.

Example:
```bash
rsync -avz --delete source/ destination/
```
This command will synchronize `source` to `destination`, deleting files from the destination that are no longer in the source directory.

### 7. --exclude

The `--exclude` flag allows you to specify files or directories that should not be copied during the transfer. You can provide patterns to match the files to exclude.

Example:
```bash
rsync -avz --exclude '*.log' source/ destination/
```
This will exclude all `.log` files from being copied from `source` to `destination`.

### 8. --progress

The `--progress` flag shows the progress of each file during the transfer, including information about the file size, amount transferred, and transfer speed.

Example:
```bash
rsync -avz --progress source/ destination/
```
This provides a detailed progress report for each file being transferred.

### 9. -e (Specify Remote Shell)

The `-e` option is used to specify the remote shell to use. By default, `rsync` uses SSH, but you can use this flag to change the remote shell if needed.

Example:
```bash
rsync -avz -e ssh source/ user@remotehost:/path/to/destination/
```
In this example, `rsync` is instructed to use `ssh` for the remote connection, though it’s the default.

### 10. --bwlimit

The `--bwlimit` flag limits the bandwidth used during the transfer. This can be useful if you don’t want `rsync` to saturate your network connection.

Example:
```bash
rsync -avz --bwlimit=1000 source/ destination/
```
This limits the transfer to 1000 KB/s (1 MB/s).

### 11. --checksum

The `--checksum` flag forces `rsync` to use checksums (instead of just file size and timestamp) to determine if a file needs to be transferred. This is slower but more accurate, especially if the timestamp or file size of a file has changed, but its content hasn't.

Example:
```bash
rsync -avz --checksum source/ destination/
```
This command compares files using checksums, ensuring that only truly modified files are transferred.

### 12. **--partial**

The `--partial` flag allows `rsync` to keep partially transferred files if the transfer is interrupted. This is useful for resuming transfers without starting from scratch.

Example:
```bash
rsync -avz --partial source/ destination/
```
This ensures that incomplete files are preserved and can be resumed if the transfer is interrupted.

---

## `rsync` vs Other File Transfer Methods

- **`rsync` vs `scp`**: While both `rsync` and `scp` are used for transferring files over SSH, `rsync` offers more flexibility and efficiency. It only transfers changes made to files, making it much faster when updating large datasets. `scp` is simpler and typically used for straightforward file copying, while `rsync` can be used for more complex file synchronization, including backups and mirroring.

- **`rsync` vs `sftp`**: Both `rsync` and `sftp` use SSH for file transfer, but `rsync` is more efficient in terms of bandwidth because it only transfers modified parts of files. `sftp` is better for interactive file management and is typically used when you need more control over file permissions and management.

---

## Conclusion

`rsync` is an indispensable tool for anyone needing to transfer, synchronize, or back up files efficiently. With its ability to perform incremental transfers, its versatility with a wide range of options, and its use of compression and checksums, `rsync` stands out as one of the most powerful file transfer utilities available. Understanding the different flags allows you to tailor your file synchronization process to meet your specific needs, whether you're performing local backups, maintaining remote mirrors, or simply keeping multiple systems in sync.
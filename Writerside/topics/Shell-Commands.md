# Commands

Shell commands are instructions that you can type into a command-line interface (CLI) to perform various tasks on your operating system. These commands can be used to navigate the file system, manage files and directories, control processes, and more.

## Basic Shell Commands

### Navigation

- `pwd`: Print the current working directory.
- `cd [directory]`: Change the current directory to the specified directory.
- `ls`: List the contents of the current directory.

### File and Directory Management

- `touch [filename]`: Create a new empty file.
- `mkdir [directory]`: Create a new directory.
- `rm [filename]`: Remove a file.
- `rmdir [directory]`: Remove an empty directory.
- `cp [source] [destination]`: Copy a file or directory.
- `mv [source] [destination]`: Move or rename a file or directory.

### Viewing and Editing Files

- `cat [filename]`: Display the contents of a file.
- `nano [filename]`: Open a file in the Nano text editor.
- `vi [filename]`: Open a file in the Vi text editor.

### Process Management

- `ps`: Display a list of currently running processes.
- `top`: Display real-time system information and a list of running processes.
- `kill [PID]`: Terminate a process by its process ID (PID).

### System Information

- `uname -a`: Display detailed information about the system.
- `df -h`: Display disk space usage.
- `free -h`: Display memory usage.

### Networking

- `ping [hostname]`: Check the network connection to a host.
- `ifconfig`: Display network interface configuration.
- `netstat`: Display network connections, routing tables, and interface statistics.

## Example Shell Script

Here is an example of a shell script that uses some of these commands to create a backup of a directory:

```sh
#!/bin/bash
source_dir="/path/to/source"
backup_dir="/path/to/backup"
timestamp=$(date +%Y%m%d%H%M%S)
backup_file="$backup_dir/backup_$timestamp.tar.gz"

# Create a backup
tar -czf $backup_file $source_dir
echo "Backup created at $backup_file"
```

This script compresses the contents of the source directory into a tar.gz file and saves it in the backup directory with a timestamp.
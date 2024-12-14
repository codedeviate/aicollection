# Bourne Again Shell (bash)

## History

The Bourne Again Shell (Bash) is a Unix shell and command language written by Brian Fox for the GNU Project as a free software replacement for the Bourne Shell (sh). First released in 1989, Bash has become the default shell on many Linux distributions and macOS.

## Features

- **Command History**: Allows users to recall and edit previous commands.
- **Tab Completion**: Automatically completes file names and commands.
- **Scripting**: Supports writing scripts to automate tasks.
- **Job Control**: Manages multiple processes within a single shell session.
- **Aliases**: Creates shortcuts for frequently used commands.

## Basic Commands

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

## Scripting

### Basic Script

```sh
#!/bin/bash
# This is a comment
echo "Hello, World!"
```

### Variables

```sh
#!/bin/bash
name="John"
echo "Hello, $name!"
```

### Conditional Statements

```sh
#!/bin/bash
number=10
if [ $number -gt 5 ]; then
  echo "The number is greater than 5"
else
  echo "The number is 5 or less"
fi
```

### Loops

#### For Loop

```sh
#!/bin/bash
for i in {1..5}; do
  echo "Iteration $i"
done
```

#### While Loop

```sh
#!/bin/bash
counter=1
while [ $counter -le 5 ]; do
  echo "Counter: $counter"
  ((counter++))
done
```

### Functions

```sh
#!/bin/bash
greet() {
  echo "Hello, $1!"
}

greet "Alice"
greet "Bob"
```

### File Operations

#### Creating a File

```sh
#!/bin/bash
echo "This is a new file" > newfile.txt
```

#### Reading a File

```sh
#!/bin/bash
while IFS= read -r line; do
  echo "$line"
done < newfile.txt
```

#### Deleting a File

```sh
#!/bin/bash
rm newfile.txt
```

### Example: Backup Script

```sh
#!/bin/bash
source_dir="/path/to/source"
backup_dir="/path/to/backup"
timestamp=$(date +%Y%m%d%H%M%S)
backup_file="$backup_dir/backup_$timestamp.tar.gz"

tar -czf $backup_file $source_dir
echo "Backup created at $backup_file"
```

This script compresses the contents of the source directory into a tar.gz file and saves it in the backup directory with a timestamp.
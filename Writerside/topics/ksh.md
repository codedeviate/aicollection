# Korn Shell (ksh)

## History

The Korn Shell (ksh) was developed by David Korn at AT&T Bell Laboratories in the early 1980s. It was designed to be a comprehensive, high-performance shell that combined the best features of the Bourne Shell (sh) and the C Shell (csh). Korn Shell is known for its scripting capabilities, performance, and compatibility with both Bourne and C Shell scripts.

## Features

- **Scripting**: Supports advanced scripting capabilities.
- **Command History**: Allows users to recall and edit previous commands.
- **Job Control**: Manages multiple processes within a single shell session.
- **Aliases**: Creates shortcuts for frequently used commands.
- **Arithmetic Operations**: Supports built-in arithmetic operations.
- **Arrays**: Provides support for one-dimensional arrays.

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

```shell
#!/bin/ksh
# This is a comment
echo "Hello, World!"
```

### Variables

```shell
#!/bin/ksh
name="John"
echo "Hello, $name!"
```

### Conditional Statements

```shell
#!/bin/ksh
number=10
if [[ $number -gt 5 ]]; then
  echo "The number is greater than 5"
else
  echo "The number is 5 or less"
fi
```

### Loops

#### For Loop

```shell
#!/bin/ksh
for i in {1..5}; do
  echo "Iteration $i"
done
```

#### While Loop

```shell
#!/bin/ksh
counter=1
while [[ $counter -le 5 ]]; do
  echo "Counter: $counter"
  ((counter++))
done
```

### Functions

```shell
#!/bin/ksh
greet() {
  echo "Hello, $1!"
}

greet "Alice"
greet "Bob"
```

### File Operations

#### Creating a File

```shell
#!/bin/ksh
echo "This is a new file" > newfile.txt
```

#### Reading a File

```shell
#!/bin/ksh
while IFS= read -r line; do
  echo "$line"
done < newfile.txt
```

#### Deleting a File

```shell
#!/bin/ksh
rm newfile.txt
```

### Example: Backup Script

```shell
#!/bin/ksh
source_dir="/path/to/source"
backup_dir="/path/to/backup"
timestamp=$(date +%Y%m%d%H%M%S)
backup_file="$backup_dir/backup_$timestamp.tar.gz"

tar -czf $backup_file $source_dir
echo "Backup created at $backup_file"
```

This script compresses the contents of the source directory into a tar.gz file and saves it in the backup directory with a timestamp.
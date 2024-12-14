# Bourne Shell (sh)

## History

The Bourne Shell (sh) was developed by Stephen Bourne at AT&T Bell Laboratories and released in 1979 as the default Unix shell in Version 7 Unix. It was designed to be a command interpreter and scripting language, providing a way to automate tasks and manage system operations. The Bourne Shell has influenced many other shells, including the Korn Shell (ksh) and the Bourne Again Shell (bash).

## Features

- **Scripting**: Supports writing scripts to automate tasks.
- **Command Substitution**: Allows the output of a command to replace the command itself.
- **Control Structures**: Provides constructs for conditional execution and loops.
- **Variables**: Supports the use of variables to store data.
- **Redirection**: Allows input and output redirection for commands.
- **Pipelines**: Supports chaining commands together using pipes.

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
#!/bin/sh
# This is a comment
echo "Hello, World!"
```

### Variables

```sh
#!/bin/sh
name="John"
echo "Hello, $name!"
```

### Conditional Statements

```sh
#!/bin/sh
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
#!/bin/sh
for i in 1 2 3 4 5; do
  echo "Iteration $i"
done
```

#### While Loop

```sh
#!/bin/sh
counter=1
while [ $counter -le 5 ]; do
  echo "Counter: $counter"
  counter=$((counter + 1))
done
```

### Functions

```sh
#!/bin/sh
greet() {
  echo "Hello, $1!"
}

greet "Alice"
greet "Bob"
```

### File Operations

#### Creating a File

```sh
#!/bin/sh
echo "This is a new file" > newfile.txt
```

#### Reading a File

```sh
#!/bin/sh
while IFS= read -r line; do
  echo "$line"
done < newfile.txt
```

#### Deleting a File

```sh
#!/bin/sh
rm newfile.txt
```

### Example: Backup Script

```sh
#!/bin/sh
source_dir="/path/to/source"
backup_dir="/path/to/backup"
timestamp=$(date +%Y%m%d%H%M%S)
backup_file="$backup_dir/backup_$timestamp.tar.gz"

tar -czf $backup_file $source_dir
echo "Backup created at $backup_file"
```

This script compresses the contents of the source directory into a tar.gz file and saves it in the backup directory with a timestamp.
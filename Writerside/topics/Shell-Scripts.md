# Scripts

Shell scripting involves writing a series of commands for the shell to execute. Shell scripts can automate repetitive tasks, manage system operations, and perform complex operations by combining multiple commands.

## Basic Shell Script Example

Here is a simple example of a shell script that prints "Hello, World!" to the terminal:

```sh
#!/bin/bash
# This is a comment
echo "Hello, World!"
```

## Variables

Variables in shell scripts are used to store data that can be referenced and manipulated throughout the script.

```sh
#!/bin/bash
name="John"
echo "Hello, $name!"
```

## Conditional Statements

Conditional statements allow the script to make decisions based on certain conditions.

```sh
#!/bin/bash
number=10
if [ $number -gt 5 ]; then
  echo "The number is greater than 5"
else
  echo "The number is 5 or less"
fi
```

## Loops

Loops are used to repeat a set of commands multiple times.

### For Loop

```sh
#!/bin/bash
for i in {1..5}; do
  echo "Iteration $i"
done
```

### While Loop

```sh
#!/bin/bash
counter=1
while [ $counter -le 5 ]; do
  echo "Counter: $counter"
  ((counter++))
done
```

## Functions

Functions in shell scripts allow you to group commands into reusable blocks.

```sh
#!/bin/bash
greet() {
  echo "Hello, $1!"
}

greet "Alice"
greet "Bob"
```

## File Operations

Shell scripts can perform various file operations such as creating, reading, and deleting files.

### Creating a File

```sh
#!/bin/bash
echo "This is a new file" > newfile.txt
```

### Reading a File

```sh
#!/bin/bash
while IFS= read -r line; do
  echo "$line"
done < newfile.txt
```

### Deleting a File

```sh
#!/bin/bash
rm newfile.txt
```

## Example: Backup Script

Here is an example of a shell script that creates a backup of a directory:

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
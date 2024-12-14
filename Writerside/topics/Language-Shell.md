# Shell

## Overview

Shell scripting is a method of writing scripts using a shell, which is a command-line interpreter that provides a user interface for the operating system. Shell scripts automate repetitive tasks, manage system operations, and perform complex sequences of commands.

## Common Shells

- **Bourne Shell (sh)**: Developed by Stephen Bourne at AT&T Bell Laboratories in 1979.
- **Bourne Again Shell (bash)**: An enhanced version of the Bourne Shell, widely used in Linux.
- **C Shell (csh)**: Developed by Bill Joy with C-like syntax.
- **Korn Shell (ksh)**: Combines features of the Bourne and C Shells, developed by David Korn.
- **Z Shell (zsh)**: An extended Bourne Shell with many improvements, created by Paul Falstad.

## Features

### Scripting

Shell scripts are text files containing a sequence of commands. They can include control structures, variables, functions, and more.

### Command Substitution

Allows the output of a command to replace the command itself.

```sh
current_date=$(date)
echo "Today's date is $current_date"
```

### Control Structures

#### Conditional Statements

```sh
#!/bin/sh
number=10
if [ $number -gt 5 ]; then
  echo "The number is greater than 5"
else
  echo "The number is 5 or less"
fi
```

#### Loops

##### For Loop

```sh
#!/bin/sh
for i in 1 2 3 4 5; do
  echo "Iteration $i"
done
```

##### While Loop

```sh
#!/bin/sh
counter=1
while [ $counter -le 5 ]; do
  echo "Counter: $counter"
  counter=$((counter + 1))
done
```

### Variables

Variables store data that can be used and manipulated within the script.

```sh
#!/bin/sh
name="John"
echo "Hello, $name!"
```

### Functions

Functions allow you to group commands into reusable blocks.

```sh
#!/bin/sh
greet() {
  echo "Hello, $1!"
}

greet "Alice"
greet "Bob"
```

### Redirection

Redirects input and output of commands.

```sh
# Redirect output to a file
echo "This is a new file" > newfile.txt

# Append output to a file
echo "This is another line" >> newfile.txt

# Redirect input from a file
while IFS= read -r line; do
  echo "$line"
done < newfile.txt
```

### Pipelines

Chains commands together using pipes.

```sh
# List files and count the number of lines
ls | wc -l
```

## Example: Backup Script

This script compresses the contents of a source directory into a tar.gz file and saves it in the backup directory with a timestamp.

```sh
#!/bin/sh
source_dir="/path/to/source"
backup_dir="/path/to/backup"
timestamp=$(date +%pct%Y%pct%m%pct%d%pct%H%pct%M%pct%S)
backup_file="$backup_dir/backup_$timestamp.tar.gz"

tar -czf $backup_file $source_dir
echo "Backup created at $backup_file"
```

Shell scripting is a versatile and essential skill for system administrators and developers, enabling efficient task automation and system management.
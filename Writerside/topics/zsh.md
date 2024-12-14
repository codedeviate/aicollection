# Z Shell (zsh)

## History

The Z Shell (zsh) was created by Paul Falstad in 1990. It was designed to be an extended Bourne Shell (sh) with many improvements, including features from other shells like the Korn Shell (ksh) and the C Shell (csh). Over time, zsh has become popular for its powerful scripting capabilities, user-friendly features, and extensive customization options.

## Features

- **Command Line Editing**: Supports advanced command line editing with Emacs and Vi modes.
- **Tab Completion**: Provides powerful and customizable tab completion for commands, file names, and more.
- **Scripting**: Supports advanced scripting capabilities.
- **Job Control**: Manages multiple processes within a single shell session.
- **Aliases**: Creates shortcuts for frequently used commands.
- **Prompt Customization**: Allows extensive customization of the shell prompt.
- **History Mechanism**: Enables users to recall and edit previous commands.
- **Globbing**: Supports advanced pattern matching for file names.

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
#!/bin/zsh
# This is a comment
echo "Hello, World!"
```

### Variables

```shell
#!/bin/zsh
name="John"
echo "Hello, $name!"
```

### Conditional Statements

```shell
#!/bin/zsh
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
#!/bin/zsh
for i in {1..5}; do
  echo "Iteration $i"
done
```

#### While Loop

```shell
#!/bin/zsh
counter=1
while [[ $counter -le 5 ]]; do
  echo "Counter: $counter"
  ((counter++))
done
```

### Functions

```shell
#!/bin/zsh
greet() {
  echo "Hello, $1!"
}

greet "Alice"
greet "Bob"
```

### File Operations

#### Creating a File

```shell
#!/bin/zsh
echo "This is a new file" > newfile.txt
```

#### Reading a File

```shell
#!/bin/zsh
while IFS= read -r line; do
  echo "$line"
done < newfile.txt
```

#### Deleting a File

```shell
#!/bin/zsh
rm newfile.txt
```

### Example: Backup Script

```shell
#!/bin/zsh
source_dir="/path/to/source"
backup_dir="/path/to/backup"
timestamp=$(date +%pct%Y%pct%m%pct%d%pct%H%pct%M%pct%S)
backup_file="$backup_dir/backup_$timestamp.tar.gz"

tar -czf $backup_file $source_dir
echo "Backup created at $backup_file"
```

This script compresses the contents of the source directory into a tar.gz file and saves it in the backup directory with a timestamp.
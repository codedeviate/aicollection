# C Shell (csh)

## History

The C Shell (csh) was developed by Bill Joy in the late 1970s at the University of California, Berkeley. It was designed to improve upon the Bourne Shell (sh) by providing a more user-friendly interface and incorporating features inspired by the C programming language, hence the name "C Shell."

## Features

- **C-like Syntax**: The syntax of csh is similar to the C programming language, making it easier for C programmers to use.
- **Job Control**: Allows users to manage multiple processes within a single shell session.
- **History Mechanism**: Enables users to recall and edit previous commands.
- **Aliases**: Allows users to create shortcuts for frequently used commands.
- **Scripting**: Supports writing scripts to automate tasks.

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
#!/bin/csh
# This is a comment
echo "Hello, World!"
```

### Variables

```shell
#!/bin/csh
set name = "John"
echo "Hello, $name!"
```

### Conditional Statements

```shell
#!/bin/csh
set number = 10
if ( $number > 5 ) then
  echo "The number is greater than 5"
else
  echo "The number is 5 or less"
endif
```

### Loops

#### For Loop

```shell
#!/bin/csh
foreach i (1 2 3 4 5)
  echo "Iteration $i"
end
```

#### While Loop

```shell
#!/bin/csh
set counter = 1
while ( $counter <= 5 )
  echo "Counter: $counter"
  @ counter++
end
```

### Functions

```shell
#!/bin/csh
alias greet 'echo Hello, \!*'

greet Alice
greet Bob
```

### File Operations

#### Creating a File

```shell
#!/bin/csh
echo "This is a new file" > newfile.txt
```

#### Reading a File

```shell
#!/bin/csh
foreach line ( `cat newfile.txt` )
  echo $line
end
```

#### Deleting a File

```shell
#!/bin/csh
rm newfile.txt
```

### Example: Backup Script

```shell
#!/bin/csh
set source_dir = "/path/to/source"
set backup_dir = "/path/to/backup"
set timestamp = `date +%Y%m%d%H%M%S`
set backup_file = "$backup_dir/backup_$timestamp.tar.gz"

tar -czf $backup_file $source_dir
echo "Backup created at $backup_file"
```

This script compresses the contents of the source directory into a tar.gz file and saves it in the backup directory with a timestamp.
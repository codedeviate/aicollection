# file

The `file` command is a standard Unix utility used to determine the type of a file. It performs a series of tests on the file to classify it based on its content rather than its name or extension.

## How `file` Works

1. **Magic Number Test**: The `file` command first checks the file's magic number, which is a unique identifier at the beginning of the file. This helps identify the file type.
2. **File System Tests**: It performs various file system tests to check for specific file types like directories, symbolic links, and special files.
3. **Text File Tests**: If the file is not identified by the previous tests, `file` checks if it is a text file and tries to determine the character encoding and language.
4. **Default to ASCII**: If all tests fail, `file` defaults to identifying the file as ASCII text.

## Key Features

- **Basic Usage**: By default, `file` provides a brief description of the file type.
- **Verbose Output**: The `-v` option provides more detailed information.
- **Follow Symlinks**: The `-L` option follows symbolic links to determine the type of the target file.
- **Magic File**: The `-m` option allows specifying a custom magic file for identifying file types.

## Example Usage

```sh
# Basic usage
file filename

# Verbose output
file -v filename

# Follow symbolic links
file -L symlink

# Use a custom magic file
file -m custom_magic_file filename
```

## Supported Systems

The `file` command is available on most Unix-like operating systems, including:

- **Linux**: Commonly available on various Linux distributions.
- **macOS**: Included in macOS by default.
- **FreeBSD**: Available as part of the base system.
- **NetBSD**: Included in the base system.
- **OpenBSD**: Part of the base system.

It is not natively available on Windows, but similar functionality can be achieved using third-party tools like Cygwin or Windows Subsystem for Linux (WSL).
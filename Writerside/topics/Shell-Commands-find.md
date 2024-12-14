# find

`find` is a powerful command-line utility used to search for files and directories in a directory hierarchy based on various criteria. It can perform actions on the found items.

## Basic Syntax

```sh
find [path...] [expression]
```

## Commonly Used Options

- `-name pattern`: Search for files matching the pattern.
- `-iname pattern`: Search for files matching the pattern, case-insensitive.
- `-type type`: Search for a specific type (e.g., `f` for files, `d` for directories).
- `-size n`: Search for files of a specific size (e.g., `+100M` for files larger than 100MB).
- `-mtime n`: Search for files modified `n` days ago.
- `-atime n`: Search for files accessed `n` days ago.
- `-ctime n`: Search for files changed `n` days ago.
- `-user name`: Search for files owned by a specific user.
- `-group name`: Search for files owned by a specific group.
- `-perm mode`: Search for files with specific permissions.
- `-exec command {} \;`: Execute a command on each found item.
- `-delete`: Delete the found files.
- `-maxdepth n`: Limit the search to `n` levels of directories.
- `-mindepth n`: Start the search at `n` levels of directories.

## Examples

### Basic Search

Search for files named "example.txt" in the current directory and subdirectories:

```sh
find . -name 'example.txt'
```

### Case-Insensitive Search

Search for files named "example.txt" (case-insensitive) in the current directory and subdirectories:

```sh
find . -iname 'example.txt'
```

### Search by Type

Search for directories named "backup":

```sh
find . -type d -name 'backup'
```

### Search by Size

Search for files larger than 100MB:

```sh
find . -size +100M
```

### Search by Modification Time

Search for files modified in the last 7 days:

```sh
find . -mtime -7
```

### Search by Access Time

Search for files accessed in the last 7 days:

```sh
find . -atime -7
```

### Search by Change Time

Search for files changed in the last 7 days:

```sh
find . -ctime -7
```

### Search by User

Search for files owned by the user "john":

```sh
find . -user john
```

### Search by Group

Search for files owned by the group "staff":

```sh
find . -group staff
```

### Search by Permissions

Search for files with 755 permissions:

```sh
find . -perm 755
```

### Execute Command on Found Items

Search for files named "example.txt" and delete them:

```sh
find . -name 'example.txt' -exec rm {} \;
```

### Delete Found Files

Search for and delete files named "example.txt":

```sh
find . -name 'example.txt' -delete
```

### Limit Search Depth

Search for files named "example.txt" only in the current directory (no subdirectories):

```sh
find . -maxdepth 1 -name 'example.txt'
```

### Start Search at Specific Depth

Search for files named "example.txt" starting from the second level of directories:

```sh
find . -mindepth 2 -name 'example.txt'
```

## Conclusion

`find` is a versatile tool for searching files and directories based on various criteria. Understanding its options and expressions allows for efficient and powerful file searching and manipulation directly from the command line.
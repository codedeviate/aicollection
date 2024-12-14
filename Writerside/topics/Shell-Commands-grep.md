# grep (Global Regular Expression Print)

`grep` is a powerful command-line utility used for searching plain-text data sets for lines that match a regular expression. It is commonly used for searching through files and output from other commands.

## Basic Syntax

```sh
grep [options] pattern [file...]
```

## Commonly Used Options

- `-i`: Ignore case distinctions in patterns and data.
- `-v`: Invert the sense of matching, to select non-matching lines.
- `-c`: Count the number of matching lines.
- `-l`: List only the names of files with matching lines.
- `-L`: List only the names of files without matching lines.
- `-n`: Prefix each line of output with the line number within its input file.
- `-H`: Print the file name for each match.
- `-h`: Suppress the file name prefix on output.
- `-r` or `-R`: Read all files under each directory, recursively.
- `-w`: Select only those lines containing matches that form whole words.
- `-x`: Select only those matches that exactly match the whole line.
- `-A num`: Print `num` lines of trailing context after matching lines.
- `-B num`: Print `num` lines of leading context before matching lines.
- `-C num`: Print `num` lines of output context (both before and after).

## Examples

### Basic Search

Search for the pattern "foo" in a file:

```sh
grep 'foo' file.txt
```

### Ignore Case

Search for the pattern "foo" in a file, ignoring case:

```sh
grep -i 'foo' file.txt
```

### Invert Match

Search for lines that do not contain the pattern "foo":

```sh
grep -v 'foo' file.txt
```

### Count Matches

Count the number of lines that contain the pattern "foo":

```sh
grep -c 'foo' file.txt
```

### List Matching Files

List the names of files that contain the pattern "foo":

```sh
grep -l 'foo' *.txt
```

### List Non-Matching Files

List the names of files that do not contain the pattern "foo":

```sh
grep -L 'foo' *.txt
```

### Show Line Numbers

Show line numbers for lines that contain the pattern "foo":

```sh
grep -n 'foo' file.txt
```

### Recursive Search

Search for the pattern "foo" in all files under the current directory, recursively:

```sh
grep -r 'foo' .
```

### Whole Word Match

Search for the whole word "foo":

```sh
grep -w 'foo' file.txt
```

### Exact Line Match

Search for lines that exactly match "foo":

```sh
grep -x 'foo' file.txt
```

### Context Lines

Print 2 lines of context before and after matching lines:

```sh
grep -C 2 'foo' file.txt
```

Print 2 lines of context after matching lines:

```sh
grep -A 2 'foo' file.txt
```

Print 2 lines of context before matching lines:

```sh
grep -B 2 'foo' file.txt
```

## Conclusion

`grep` is a versatile tool for searching text using patterns. Understanding its options and commands allows for efficient and powerful text searching directly from the command line.
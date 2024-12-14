# xargs

`xargs` is a command-line utility used to build and execute command lines from standard input. It is commonly used to pass a large number of arguments to a command that does not accept them directly.

## Basic Syntax

```sh
xargs [options] [command [initial-arguments]]
```

## Commonly Used Options

- `-0`: Input items are terminated by a null character instead of whitespace.
- `-a file`: Read items from `file` instead of standard input.
- `-d delim`: Input items are terminated by the specified character.
- `-E eof-str`: Set the end-of-file string to `eof-str`.
- `-I replace-str`: Replace occurrences of `replace-str` in the initial arguments with input items.
- `-L max-lines`: Use at most `max-lines` non-blank input lines per command line.
- `-n max-args`: Use at most `max-args` arguments per command line.
- `-P max-procs`: Run up to `max-procs` processes at a time.
- `-p`: Prompt the user before running each command line.
- `-r`: Do not run the command if the input is empty.
- `-s max-chars`: Use at most `max-chars` characters per command line.
- `-t`: Print the command line on standard error before executing it.

## Examples

### Basic Usage

Pass a list of files to the `rm` command:

```sh
ls *.txt | xargs rm
```

### Using `-n` Option

Run the command with at most 2 arguments at a time:

```sh
echo "file1 file2 file3 file4" | xargs -n 2 echo
```

### Using `-I` Option

Replace occurrences of `{}` with the input items:

```sh
echo "file1 file2" | xargs -I {} mv {} /destination/
```

### Using `-P` Option (1)

Run up to 4 processes at a time:

```sh
cat urls.txt | xargs -P 4 -n 1 wget
```

### Using `-0` Option

Handle input items separated by null characters (useful with `find -print0`):

```sh
find . -name "*.txt" -print0 | xargs -0 rm
```

### Using `-a` Option

Read items from a file:

```sh
xargs -a filelist.txt rm
```

### Using `-d` Option

Specify a custom delimiter:

```sh
echo "item1,item2,item3" | xargs -d ',' echo
```

### Using `-L` Option

Use at most 1 non-blank input line per command line:

```sh
echo -e "line1\nline2\nline3" | xargs -L 1 echo
```

### Using `-p` Option (2)

Prompt the user before running each command line:

```sh
echo "file1 file2" | xargs -p rm
```

### Using `-t` Option

Print the command line before executing it:

```sh
echo "file1 file2" | xargs -t rm
```

## Conclusion

`xargs` is a versatile tool for building and executing command lines from standard input. Understanding its options allows for efficient and powerful command-line operations.
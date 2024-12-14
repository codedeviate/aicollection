# sed (Stream Editor)

`sed` is a powerful stream editor used to perform basic text transformations on an input stream (a file or input from a pipeline). It is commonly used for text substitution, deletion, and insertion.

## Basic Syntax

```sh
sed [options] 'script' [input-file]
```

## Commonly Used Options

- `-e script`: Add the script to the commands to be executed.
- `-f script-file`: Add the contents of the script-file to the commands to be executed.
- `-i[SUFFIX]`: Edit files in place (makes backup if SUFFIX supplied).
- `-n`: Suppress automatic printing of pattern space.
- `-r`: Use extended regular expressions in the script.
- `-s`: Treat files as separate rather than as a single continuous long stream.
- `-u`: Load minimal amounts of data from the input files and flush the output buffers more often.

## Common Commands

- `s/pattern/replacement/flags`: Substitute pattern with replacement.
- `d`: Delete pattern space.
- `p`: Print pattern space.
- `a\ text`: Append text after the current line.
- `i\ text`: Insert text before the current line.
- `c\ text`: Replace the current line with text.
- `y/source/dest`: Transliterate characters in the pattern space.

## Flags for `s` Command

- `g`: Global replacement.
- `p`: Print the line if a replacement was made.
- `w file`: Write the result to a file.
- `number`: Replace only the `number`th occurrence.

## Examples

### Substitute Text

Replace the first occurrence of "foo" with "bar" in each line:

```sh
sed 's/foo/bar/' input.txt
```

Replace all occurrences of "foo" with "bar" in each line:

```sh
sed 's/foo/bar/g' input.txt
```

### Delete Lines

Delete lines containing "foo":

```sh
sed '/foo/d' input.txt
```

Delete the first line of the file:

```sh
sed '1d' input.txt
```

### Print Lines

Print lines containing "foo":

```sh
sed -n '/foo/p' input.txt
```

Print the first 10 lines of the file:

```sh
sed -n '1,10p' input.txt
```

### Insert and Append Text

Insert "Hello" before the first line:

```sh
sed '1i\Hello' input.txt
```

Append "World" after the last line:

```sh
sed '$a\World' input.txt
```

### Replace Entire Line

Replace lines containing "foo" with "bar":

```sh
sed '/foo/c\bar' input.txt
```

### Transliterate Characters

Replace all occurrences of "a" with "A" and "b" with "B":

```sh
sed 'y/ab/AB/' input.txt
```

### In-Place Editing

Replace "foo" with "bar" in the file and save changes:

```sh
sed -i 's/foo/bar/g' input.txt
```

### Using a Script File

Create a script file `script.sed` with the following content:

```sh
s/foo/bar/g
/hello/d
```

Run `sed` with the script file:

```sh
sed -f script.sed input.txt
```

### Using Extended Regular Expressions

Replace all digits with "X":

```sh
sed -r 's/[0-9]/X/g' input.txt
```

## Conclusion

`sed` is a versatile tool for text processing and can be used for a wide range of tasks, from simple substitutions to complex text manipulations. Understanding its options and commands allows for efficient and powerful text editing directly from the command line.
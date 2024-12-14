# tee

`tee` is a command-line utility used to read from standard input and write to standard output and files simultaneously. It is commonly used in pipelines to capture intermediate output.

## Basic Syntax

```sh
tee [options] [file...]
```

## Commonly Used Options

- `-a`, `--append`: Append to the given files, do not overwrite.
- `-i`, `--ignore-interrupts`: Ignore interrupt signals.
- `--output-error[=mode]`: Adjust behavior on write errors. Modes include `warn`, `warn-nopipe`, and `exit`.

## Examples

### Basic Usage

Write the output of a command to a file and display it on the terminal:

```sh
echo "Hello, World!" | tee output.txt
```

### Append to a File

Append the output of a command to a file:

```sh
echo "Additional line" | tee -a output.txt
```

### Use with Pipelines

Capture the output of a command in a file while passing it to another command:

```sh
ls -l | tee filelist.txt | grep ".txt"
```

### Ignore Interrupts

Ignore interrupt signals while writing to a file:

```sh
echo "This will ignore interrupts" | tee -i output.txt
```

### Multiple Files

Write the output to multiple files:

```sh
echo "Hello, multiple files!" | tee file1.txt file2.txt
```

### Handle Write Errors

Adjust behavior on write errors:

```sh
echo "Handle write errors" | tee --output-error=warn output.txt
```

## Conclusion

`tee` is a versatile tool for duplicating the output of a command to both standard output and files. Understanding its options allows for efficient and powerful output management in command-line operations.
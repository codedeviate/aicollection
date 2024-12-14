# awk

`awk` is a powerful programming language and command-line utility for pattern scanning and processing. It is used for manipulating data and generating reports. `awk` processes input line by line and applies a set of rules to each line.

## Basic Syntax

```sh
awk 'pattern { action }' [file...]
```

## Commonly Used Options

- `-F fs`: Set the input field separator to `fs`.
- `-v var=value`: Assign a value to a variable.
- `-f file`: Read the `awk` program from a file.
- `-W`: Enable compatibility with older versions of `awk`.

## Built-in Variables (1)

- `FS`: Input field separator (default is space).
- `OFS`: Output field separator (default is space).
- `RS`: Input record separator (default is newline).
- `ORS`: Output record separator (default is newline).
- `NR`: Number of records (lines) read so far.
- `NF`: Number of fields in the current record.
- `$0`: Entire current record.
- `$1, $2, ...`: Individual fields in the current record.

## Examples

### Basic Print

Print all lines in a file:

```sh
awk '{ print }' file.txt
```

Print the first field of each line:

```sh
awk '{ print $1 }' file.txt
```

### Field Separator

Specify a comma as the field separator:

```sh
awk -F, '{ print $1 }' file.csv
```

### Pattern Matching

Print lines that contain "foo":

```sh
awk '/foo/ { print }' file.txt
```

Print lines where the second field is greater than 10:

```sh
awk '$2 > 10 { print }' file.txt
```

### Built-in Variables (2)

Print the line number and the line itself:

```sh
awk '{ print NR, $0 }' file.txt
```

Print the number of fields and the last field of each line:

```sh
awk '{ print NF, $NF }' file.txt
```

### Arithmetic Operations

Print the sum of the first and second fields:

```sh
awk '{ print $1 + $2 }' file.txt
```

### String Operations

Print the length of the first field:

```sh
awk '{ print length($1) }' file.txt
```

### Using Variables

Assign a value to a variable and use it in the action:

```sh
awk -v threshold=10 '$2 > threshold { print }' file.txt
```

### Using a Script File

Create a script file `script.awk` with the following content:

```awk
BEGIN { FS="," }
{ print $1, $2 }
```

Run `awk` with the script file:

```sh
awk -f script.awk file.csv
```

### Output Field Separator

Set the output field separator to a comma:

```sh
awk 'BEGIN { OFS="," } { print $1, $2 }' file.txt
```

### Conditional Statements

Print "High" if the second field is greater than 10, otherwise print "Low":

```sh
awk '{ if ($2 > 10) print "High"; else print "Low" }' file.txt
```

### Loops

Print the sum of all fields in each line:

```sh
awk '{ sum=0; for (i=1; i<=NF; i++) sum+=$i; print sum }' file.txt
```

## Conclusion

`awk` is a versatile tool for text processing and data extraction. Understanding its options, built-in variables, and syntax allows for efficient and powerful text manipulation directly from the command line.
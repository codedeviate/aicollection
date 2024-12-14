# sort

`sort` is a command-line utility used to sort lines of text files. It can sort data in various ways, such as numerically, alphabetically, or by specific fields.

## Basic Syntax

```sh
sort [options] [file...]
```

## Commonly Used Options

- `-b`: Ignore leading blanks.
- `-d`: Consider only blanks and alphanumeric characters.
- `-f`: Fold lowercase to uppercase characters.
- `-g`: Compare according to general numerical value.
- `-i`: Consider only printable characters.
- `-M`: Compare (unknown) < 'JAN' < ... < 'DEC'.
- `-n`: Compare according to string numerical value.
- `-r`: Reverse the result of comparisons.
- `-k pos1[,pos2]`: Sort by a key.
- `-t char`: Use `char` as the field separator.
- `-u`: Output only the first of an equal run.
- `-o file`: Write result to `file` instead of standard output.
- `-c`: Check for sorted input; do not sort.
- `-C`: Check for sorted input; do not sort, and exit with status 0 if the input is sorted.

## Examples

### Basic Sort

Sort the lines in a file alphabetically:

```sh
sort file.txt
```

### Sort and Save to a File

Sort the lines in a file and save the result to another file:

```sh
sort file.txt -o sorted_file.txt
```

### Numeric Sort

Sort the lines in a file numerically:

```sh
sort -n file.txt
```

### Reverse Sort

Sort the lines in a file in reverse order:

```sh
sort -r file.txt
```

### Sort by a Specific Field

Sort the lines in a file by the second field (assuming fields are separated by spaces):

```sh
sort -k 2 file.txt
```

### Sort by a Specific Field with a Custom Separator

Sort the lines in a file by the second field, using a comma as the field separator:

```sh
sort -t ',' -k 2 file.csv
```

### Ignore Leading Blanks

Sort the lines in a file, ignoring leading blanks:

```sh
sort -b file.txt
```

### Case-Insensitive Sort

Sort the lines in a file, ignoring case differences:

```sh
sort -f file.txt
```

### Unique Sort

Sort the lines in a file and remove duplicates:

```sh
sort -u file.txt
```

### Check if File is Sorted

Check if the lines in a file are sorted:

```sh
sort -c file.txt
```

### Sort by Month

Sort the lines in a file by month name:

```sh
sort -M file.txt
```

## Conclusion

`sort` is a versatile tool for sorting lines of text files based on various criteria. Understanding its options allows for efficient and powerful text sorting directly from the command line.
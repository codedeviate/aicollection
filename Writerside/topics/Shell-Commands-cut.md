# cut

`cut` is a command-line utility used to extract sections from each line of input, usually from a file. It is commonly used to extract specific columns or fields from text files.

## Basic Syntax

```sh
cut [options] [file...]
```

## Commonly Used Options

- `-b list`: Select only the bytes specified in `list`.
- `-c list`: Select only the characters specified in `list`.
- `-d delim`: Use `delim` as the field delimiter character instead of the default tab.
- `-f list`: Select only the fields specified in `list`.
- `-n`: Do not split multi-byte characters (used with `-b`).
- `--complement`: Complement the selection, i.e., select all bytes, characters, or fields except those specified.
- `--output-delimiter=string`: Use `string` as the output delimiter.

## Examples

### Basic Usage

Extract the first 10 characters of each line in a file:

```sh
cut -c 1-10 file.txt
```

### Extract Specific Fields

Extract the second and third fields from a file, using a comma as the field delimiter:

```sh
cut -d ',' -f 2,3 file.csv
```

### Extract Specific Bytes

Extract the first 5 bytes of each line in a file:

```sh
cut -b 1-5 file.txt
```

### Complement Selection

Extract all fields except the first and second, using a tab as the field delimiter:

```sh
cut -d $'\t' --complement -f 1,2 file.txt
```

### Using Output Delimiter

Extract the first and third fields and use a semicolon as the output delimiter:

```sh
cut -d ',' -f 1,3 --output-delimiter=';' file.csv
```

### Extract Fields with Multiple Delimiters

Extract the first field using a space as the delimiter:

```sh
cut -d ' ' -f 1 file.txt
```

### Extract Fields from Standard Input

Extract the second field from the input provided by `echo`:

```sh
echo "one two three" | cut -d ' ' -f 2
```

## Conclusion

`cut` is a versatile tool for extracting specific sections from lines of text files. Understanding its options allows for efficient and powerful text extraction directly from the command line.
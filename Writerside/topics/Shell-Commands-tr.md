# tr

`tr` is a command-line utility used to translate or delete characters from standard input and write the result to standard output. It is commonly used for transforming text, such as changing case, deleting characters, or replacing characters.

## Basic Syntax

```sh
tr [options] set1 [set2]
```

## Commonly Used Options

- `-c`: Complement the set of characters in `set1`.
- `-d`: Delete characters in `set1`.
- `-s`: Squeeze repeated characters in `set1`.
- `-t`: Truncate `set1` to the length of `set2`.

## Examples

### Basic Translation

Translate lowercase letters to uppercase:

```sh
echo "hello world" | tr 'a-z' 'A-Z'
```

### Delete Characters

Delete all digits from the input:

```sh
echo "hello123" | tr -d '0-9'
```

### Squeeze Repeated Characters

Squeeze multiple spaces into a single space:

```sh
echo "hello    world" | tr -s ' '
```

### Complement Set

Replace all characters except digits with asterisks:

```sh
echo "hello123" | tr -c '0-9' '*'
```

### Translate and Delete

Translate lowercase to uppercase and delete digits:

```sh
echo "hello123" | tr 'a-z0-9' 'A-Z'
```

### Using Character Classes

Translate all lowercase letters to uppercase using character classes:

```sh
echo "hello world" | tr '[:lower:]' '[:upper:]'
```

### Using Ranges

Translate digits to letters:

```sh
echo "12345" | tr '0-9' 'a-j'
```

### Truncate Set1

Translate the first three letters to uppercase, ignoring the rest:

```sh
echo "abcdef" | tr -t 'a-z' 'A-C'
```

## Conclusion

`tr` is a versatile tool for translating, deleting, and squeezing characters in text. Understanding its options allows for efficient and powerful text manipulation directly from the command line.
# sed

`sed` (short for **stream editor**) is a powerful, non-interactive text processing tool that allows you to perform basic text transformations on an input stream (a file or input from a pipeline). Unlike interactive text editors, `sed` applies editing commands to each line of input automatically, making it ideal for batch processing, scripting, and quick text manipulations. This comprehensive guide covers the basics of `sed`, its command-line options, a wide variety of commands and addresses, and plenty of practical examples to help you harness its power.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Basic Syntax and How `sed` Works](#basic-syntax-and-how-sed-works)
3. [Command-Line Options and Parameters](#command-line-options-and-parameters)
4. [Common `sed` Commands](#common-sed-commands)
    - [Substitution (`s`)](#substitution-s)
    - [Deletion (`d`)](#deletion-d)
    - [Insertion (`i`), Append (`a`), and Change (`c`)](#insertion-i-append-a-and-change-c)
    - [Print (`p`) and Suppress Default Output (`-n`)](#print-p-and-suppress-default-output-n)
5. [Addressing: Specifying Lines and Ranges](#addressing-specifying-lines-and-ranges)
6. [Advanced `sed` Features](#advanced-sed-features)
    - [Using Multiple Commands](#using-multiple-commands)
    - [The Hold Space and Pattern Space](#the-hold-space-and-pattern-space)
    - [Branching and Conditional Execution](#branching-and-conditional-execution)
    - [Extended Regular Expressions](#extended-regular-expressions)
7. [Practical Examples](#practical-examples)
8. [Conclusion and Further Reading](#conclusion-and-further-reading)

---

## Introduction

`sed` is an indispensable tool for anyone who needs to perform text transformations from the command line. Its non-interactive, scriptable nature makes it ideal for automating repetitive tasks such as:
- Substituting text (e.g., replacing all occurrences of a word).
- Deleting or inserting lines based on patterns.
- Extracting or rearranging parts of files.
- Performing in-place edits for configuration files or source code.

With a minimal syntax and a powerful set of commands, `sed` can handle a wide range of text processing tasks efficiently.

---

## Basic Syntax and How `sed` Works

The general syntax of `sed` is:

```bash
sed [OPTIONS] 'script' [input_file...]
```

- **OPTIONS:** Modify the behavior of `sed` (e.g., `-n` to suppress automatic printing).
- **`script`:** A set of `sed` commands enclosed in quotes. This can also be read from a file using the `-f` option.
- **`input_file`:** One or more files to process. If no file is specified, `sed` reads from standard input.

### Example: Simple Substitution

The most common use of `sed` is to perform a substitution:

```bash
sed 's/old/new/g' file.txt
```

This command replaces every occurrence of `old` with `new` in `file.txt` and prints the result to standard output.

---

## Command-Line Options and Parameters

`sed` offers a range of options to control its behavior:

- **`-n`**  
  Suppresses automatic printing of pattern space. When using `-n`, you typically use the `p` (print) command explicitly.

  ```bash
  sed -n 's/foo/bar/p' file.txt
  ```

- **`-e script`**  
  Allows you to specify multiple editing commands on the command line. This option is useful when you want to apply several commands sequentially.

  ```bash
  sed -e 's/foo/bar/g' -e 's/baz/qux/g' file.txt
  ```

- **`-f script_file`**  
  Reads `sed` commands from a file instead of specifying them on the command line.

  ```bash
  sed -f my_script.sed file.txt
  ```

- **`-i[SUFFIX]`**  
  Edits files in place. An optional backup suffix can be provided to save the original file.

  ```bash
  sed -i.bak 's/foo/bar/g' file.txt
  ```

- **`-r` or `-E`**  
  Enables extended regular expressions, allowing for a more concise syntax in pattern matching.

  ```bash
  sed -E 's/(foo|bar)/baz/g' file.txt
  ```

---

## Common `sed` Commands

### Substitution (`s`)

The substitution command is the most frequently used `sed` command:

```bash
s/pattern/replacement/flags
```

- **`pattern`**: A regular expression to match.
- **`replacement`**: The text to replace the matched pattern.
- **`flags`**: Modifiers such as:
    - **`g`**: Replace all occurrences in the line (global).
    - **`i`**: Ignore case (when supported).
    - **`number`**: Replace the *n*th occurrence only.

**Example:**

Replace all occurrences of "cat" with "dog":

```bash
sed 's/cat/dog/g' animals.txt
```

### Deletion (`d`)

The `d` command deletes lines that match a specified address or pattern.

**Example:**

Delete all lines containing "DEBUG" from a log file:

```bash
sed '/DEBUG/d' logfile.txt
```

### Insertion (`i`), Append (`a`), and Change (`c`)

- **Insertion (`i`):** Inserts text before a matching line.

  **Example:**

  ```bash
  sed '/^Chapter 2/i\
  Introduction:
  ' book.txt
  ```

  This inserts "Introduction:" before every line that starts with "Chapter 2".  
  *(Note: In many shells, you may need to handle newlines carefully.)*

- **Append (`a`):** Appends text after a matching line.

  **Example:**

  ```bash
  sed '/^Chapter 2/a\
  End of Introduction.
  ' book.txt
  ```

- **Change (`c`):** Replaces an entire line with new text.

  **Example:**

  ```bash
  sed '/^Old Title/c\
  New Title
  ' book.txt
  ```

### Print (`p`) and Suppress Default Output (`-n`)

By default, `sed` prints every line after processing. Using the `-n` option suppresses this behavior so that only explicitly printed lines (via the `p` command) appear.

**Example:**

Print only lines that have been modified by a substitution:

```bash
sed -n 's/error/ERROR/p' logfile.txt
```

---

## Addressing: Specifying Lines and Ranges

`sed` allows you to target specific lines or ranges of lines for editing.

- **Line Numbers:**  
  You can specify a particular line number.

  ```bash
  sed '3d' file.txt  # Deletes the 3rd line
  ```

- **Range of Lines:**  
  Specify a start and end line separated by a comma.

  ```bash
  sed '5,10d' file.txt  # Deletes lines 5 through 10
  ```

- **Pattern Addresses:**  
  Use regular expressions to match lines.

  ```bash
  sed '/^Chapter/,/^Appendix/d' book.txt
  ```

  This command deletes all lines starting from the one that begins with "Chapter" up to (and including) the line that begins with "Appendix".

- **Multiple Addresses:**  
  Combine line numbers and patterns.

  ```bash
  sed -n '1,5p; /Important/p' file.txt
  ```

  This prints lines 1 through 5 and any lines that contain the word "Important".

---

## Advanced `sed` Features

### Using Multiple Commands

You can execute multiple editing commands by using multiple `-e` options or by separating commands with semicolons inside a single script.

**Example:**

```bash
sed -e 's/foo/bar/g' -e 's/baz/qux/g' file.txt
```

Or:

```bash
sed 's/foo/bar/g; s/baz/qux/g' file.txt
```

### The Hold Space and Pattern Space

`sed` works with two primary areas:
- **Pattern Space:** The current line of text being processed.
- **Hold Space:** A secondary buffer used to store and retrieve text.

Commands like `h` (copy pattern space to hold space), `H` (append pattern space to hold space), `g` (copy hold space to pattern space), and `G` (append hold space to pattern space) allow for complex text manipulations.

**Example:**

Swap the first two lines of a file (a simplistic demonstration):

```bash
sed '1{h;d}; 2{G}' file.txt
```

### Branching and Conditional Execution

`sed` offers branching commands that allow you to create conditional execution flows:
- **`b label`**: Unconditionally branch to a label.
- **`t label`**: Branch to a label if a successful substitution has been made.

**Example:**

```bash
sed ':start
s/\(.*\)pattern/\1replacement/
t start
' file.txt
```

This loops until no more substitutions can be made on the line.

### Extended Regular Expressions

By default, `sed` uses basic regular expressions. To use extended regular expressions (which provide a more powerful syntax), you can invoke `sed` with the `-r` (or `-E` in some implementations) option.

**Example:**

```bash
sed -E 's/(cat|dog)/pet/g' animals.txt
```

---

## Practical Examples

### Example 1: Global Substitution

Replace all occurrences of "apple" with "orange" in a file:

```bash
sed 's/apple/orange/g' fruits.txt
```

### Example 2: In-Place Editing

Correct a typo in a file by editing it in place (with a backup):

```bash
sed -i.bak 's/teh/the/g' article.txt
```

### Example 3: Delete Blank Lines

Remove all blank lines from a file:

```bash
sed '/^$/d' file.txt
```

### Example 4: Print Specific Lines

Print only lines 10 to 20 from a file:

```bash
sed -n '10,20p' file.txt
```

### Example 5: Insert a Header

Insert a header line at the beginning of a file:

```bash
sed '1i\
Header: This is the file header
' document.txt
```

### Example 6: Combining Multiple Commands

Replace "foo" with "bar" and delete lines containing "baz":

```bash
sed -e 's/foo/bar/g' -e '/baz/d' file.txt
```

---

## Conclusion and Further Reading

`sed` is a versatile and efficient tool for stream editing that can handle everything from simple text substitutions to complex multi-line processing and conditional logic. By mastering its syntax, addressing mechanisms, and wide array of commands, you can significantly enhance your productivity in shell scripting, file processing, and text manipulation tasks.

### Further Reading and Resources

- **Manual Pages:**  
  Access the manual with:
  ```bash
  man sed
  ```
- **Online Documentation and Tutorials:**
    - [GNU sed Manual](https://www.gnu.org/software/sed/manual/sed.html)
    - [Sed - An Introduction and Tutorial](https://www.grymoire.com/Unix/Sed.html)
    - [Stack Overflow Sed Questions](https://stackoverflow.com/questions/tagged/sed)
- **Books:**
    - *Sed & Awk* by Dale Dougherty and Arnold Robbins

Experiment with different commands and options in `sed` to unlock its full potential and incorporate it into your daily workflows. Happy editing!
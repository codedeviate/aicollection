# uniq

The `uniq` command is a straightforward yet powerful tool in Unix-like systems that helps you filter out or report adjacent duplicate lines from input. Typically used on sorted data (since it only compares neighboring lines), `uniq` is ideal for summarizing and processing text streams, such as log files, configuration lists, or any structured text where redundancy is possible. In this comprehensive guide, we’ll explore the syntax, options, practical examples, and advanced usage of `uniq` to help you integrate it into your workflow.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Basic Syntax and How `uniq` Works](#basic-syntax-and-how-uniq-works)
3. [Common Command-Line Options and Parameters](#common-command-line-options-and-parameters)
    - [Counting Occurrences (`-c`)](#counting-occurrences-c)
    - [Displaying Only Duplicates (`-d`)](#displaying-only-duplicates-d)
    - [Displaying Only Unique Lines (`-u`)](#displaying-only-unique-lines-u)
    - [Other Options](#other-options)
4. [Practical Examples](#practical-examples)
5. [Advanced Usage and Tips](#advanced-usage-and-tips)
6. [Conclusion and Further Reading](#conclusion-and-further-reading)

---

## Introduction

The `uniq` command examines its input (usually a text file or stream) and removes or reports consecutive duplicate lines. Because `uniq` only compares adjacent lines, it is often paired with the `sort` command to ensure that duplicate items are positioned next to each other. With minimal syntax and a handful of useful options, `uniq` becomes an indispensable tool for data cleaning and summarization in shell scripts and on the command line.

---

## Basic Syntax and How `uniq` Works

The general syntax of `uniq` is:

```bash
uniq [OPTIONS] [INPUT [OUTPUT]]
```

- **INPUT:** The file to process. If no file is provided, `uniq` reads from standard input.
- **OUTPUT:** The file to which the output should be written. If omitted, output is sent to standard output.

**Key Points:**
- **Adjacent Comparison:** `uniq` only removes duplicate lines that appear one after another.
- **Sorted Input:** Since duplicates must be adjacent, input is typically sorted before using `uniq` (e.g., `sort file.txt | uniq`).

---

## Common Command-Line Options and Parameters

### Counting Occurrences (`-c`)

- **Usage:** Prepend each unique line with the number of occurrences.
- **Example:**

  ```bash
  sort file.txt | uniq -c
  ```

  This command sorts the file and then outputs each line along with a count of how many times it appeared.

### Displaying Only Duplicates (`-d`)

- **Usage:** Print only lines that are repeated (i.e., appear more than once).
- **Example:**

  ```bash
  sort file.txt | uniq -d
  ```

  Only lines that have duplicates will be printed, which is useful for quickly spotting repeated entries.

### Displaying Only Unique Lines (`-u`)

- **Usage:** Print only lines that appear exactly once.
- **Example:**

  ```bash
  sort file.txt | uniq -u
  ```

  This outputs only the lines that are not repeated in the file.

### Other Options

- **`-f N` or `--skip-fields=N`:**  
  Skip the first N fields (a field being a sequence of non-space characters) when comparing lines.

  ```bash
  sort file.txt | uniq -f 1
  ```

- **`-s N` or `--skip-chars=N`:**  
  Skip the first N characters when comparing lines.

  ```bash
  sort file.txt | uniq -s 3
  ```

- **`-i` or `--ignore-case`:**  
  Perform a case-insensitive comparison.

  ```bash
  sort file.txt | uniq -i
  ```

---

## Practical Examples

### Example 1: Basic Duplicate Removal

To remove adjacent duplicate lines from a file:

```bash
uniq file.txt
```

*Note:* If `file.txt` is not sorted, only consecutive duplicates will be removed.

### Example 2: Removing All Duplicates (After Sorting)

To remove duplicates regardless of their position in the file, sort the file first:

```bash
sort file.txt | uniq
```

### Example 3: Counting Occurrences

To count how many times each line appears in a file:

```bash
sort file.txt | uniq -c
```

This is particularly useful for creating frequency lists.

### Example 4: Display Only Duplicated Lines

To show only lines that are repeated:

```bash
sort file.txt | uniq -d
```

### Example 5: Display Only Unique Lines

To display lines that are unique (appear only once):

```bash
sort file.txt | uniq -u
```

### Example 6: Ignoring Case

To remove duplicates in a case-insensitive manner:

```bash
sort file.txt | uniq -i
```

---

## Advanced Usage and Tips

- **Using with Other Tools:**  
  `uniq` is often used in combination with `sort` to ensure that duplicate entries are adjacent. For example:
  ```bash
  sort -u file.txt
  ```
  The `sort -u` command performs both sorting and duplicate removal in one step.

- **Skipping Fields or Characters:**  
  When lines contain fields or prefixes that should be ignored for uniqueness, use `-f` or `-s`. For instance, if each line begins with a timestamp that should not affect the duplicate check:
  ```bash
  sort file.txt | uniq -s 20
  ```
  This skips the first 20 characters in each line during comparison.

- **Case Sensitivity:**  
  When you need to treat lines as identical regardless of case, always include `-i`.

- **Practical Scripting:**  
  Use `uniq` in scripts to filter log files, generate summary reports, or remove redundancy in configuration files. For example, combining with `grep`:
  ```bash
  grep "ERROR" log.txt | sort | uniq -c | sort -nr
  ```
  This pipeline filters error messages, counts occurrences, and sorts them in descending order.

---

## Conclusion and Further Reading

The `uniq` command is a simple yet effective utility for handling duplicate lines in text files. By understanding its options and combining it with other Unix tools like `sort`, you can quickly and efficiently process text data for reporting, analysis, or cleanup tasks. Its ease of use and flexibility make it an essential part of any Unix/Linux user’s toolkit.

### Further Reading and Resources

- **Manual Page:**  
  View the detailed manual by running:
  ```bash
  man uniq
  ```
- **Online Documentation:**
    - [GNU Coreutils: uniq](https://www.gnu.org/software/coreutils/uniq)
- **Community Examples:**  
  Websites like [Stack Overflow](https://stackoverflow.com/questions/tagged/uniq) and various Unix/Linux blogs offer practical examples and discussions about advanced usage of `uniq`.

Experiment with `uniq` on your own datasets to explore how it can simplify the process of filtering and summarizing text. Happy deduplicating!
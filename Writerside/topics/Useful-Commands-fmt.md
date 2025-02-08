# fmt

The `fmt` command is a simple text formatter that reflows and formats plain text paragraphs to a specified width. It’s especially useful for ensuring that text files, documentation, or email messages adhere to a consistent line length without breaking words inappropriately. In this comprehensive guide, we’ll explore the basic syntax, common options, practical examples, and advanced usage tips for the `fmt` command.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Basic Syntax and How `fmt` Works](#basic-syntax-and-how-fmt-works)
3. [Common Options and Parameters](#common-options-and-parameters)
    - [Setting the Desired Width (`-w` or `--width`)](#setting-the-desired-width)
    - [Controlling the Paragraph Mode (`-p` and `-u`)](#controlling-paragraph-mode)
    - [Preserving Existing Line Breaks (`-c`)](#preserving-existing-line-breaks)
    - [Other Useful Options](#other-useful-options)
4. [Practical Examples](#practical-examples)
    - [Reformatting a Simple Text File](#reformatting-a-simple-text-file)
    - [Changing the Maximum Line Width](#changing-the-maximum-line-width)
    - [Preserving Indentation and Blank Lines](#preserving-indentation-and-blank-lines)
    - [Processing Standard Input in a Pipeline](#processing-standard-input-in-a-pipeline)
5. [Advanced Usage and Tips](#advanced-usage-and-tips)
6. [Conclusion and Further Reading](#conclusion-and-further-reading)

---

## Introduction

The `fmt` command is a lightweight utility that is part of many Unix-like systems. Its primary purpose is to reformat paragraphs of text by adjusting line breaks so that each line is as close as possible to a specified maximum width without splitting words. This makes it ideal for cleaning up text files or reformatting output from other commands to improve readability.

Key benefits of `fmt` include:

- **Consistent Line Width:** Automatically reflows paragraphs to a uniform width.
- **Word Preservation:** Ensures words are not broken in the middle.
- **Ease of Use:** Works directly with files or standard input, making it suitable for pipelines and scripts.

---

## Basic Syntax and How `fmt` Works

The general syntax for `fmt` is:

```bash
fmt [OPTIONS] [FILE...]
```

- **FILE:** One or more text files to be formatted. If no file is provided, `fmt` reads from standard input.
- **OPTIONS:** Flags that allow you to control the formatting behavior, such as line width and paragraph handling.

By default, `fmt` processes the input text by grouping consecutive lines into paragraphs (separated by one or more blank lines) and then reflowing each paragraph to the default width (usually 75 characters).

---

## Common Options and Parameters

### Setting the Desired Width

- **`-w NUM` or `--width=NUM`:**  
  Specifies the maximum width (in columns) for the output lines. For example, to format text so that no line exceeds 50 characters:

  ```bash
  fmt -w 50 file.txt
  ```

  This option is the most frequently used, as it allows you to control the overall appearance of the text.

### Controlling Paragraph Mode

- **`-p`:**  
  Enables "paragraph mode" where blank lines are preserved as paragraph separators. This is the default behavior, but you can use this flag explicitly to ensure paragraphs remain distinct.

- **`-u`:**  
  Tells `fmt` to treat each input line as a separate paragraph, which means no reflowing is done across lines. Use this option if you want to prevent merging of lines that might be logically separate.

### Preserving Existing Line Breaks

- **`-c`:**  
  Prevents `fmt` from breaking long lines even if they exceed the specified width. This can be useful when you want to ensure that certain lines remain unchanged while still processing other paragraphs.

### Other Useful Options

- **`--help`:**  
  Displays help information for `fmt`.

- **`--version`:**  
  Outputs version information about the `fmt` utility.

---

## Practical Examples

### Reformatting a Simple Text File

Suppose you have a file named `example.txt` that contains text with irregular line breaks. Running:

```bash
fmt example.txt
```

will reflow the paragraphs so that each line is roughly 75 characters long (the default width), resulting in a more uniform appearance.

### Changing the Maximum Line Width

To format the text so that no line exceeds 60 characters, use:

```bash
fmt -w 60 example.txt
```

This ensures that the output lines are shorter, which might be preferable for narrow display windows or specific formatting requirements.

### Preserving Indentation and Blank Lines

If your text file contains indented lines or you want to ensure that blank lines (paragraph breaks) are preserved, you can combine options like:

```bash
fmt -w 80 -p example.txt
```

This command preserves paragraph breaks while reflowing the text to a width of 80 characters.

### Processing Standard Input in a Pipeline

`fmt` is often used in pipelines. For instance, if you want to reformat the output of another command, you can do:

```bash
cat example.txt | fmt -w 70
```

This reads the file through `cat`, pipes it into `fmt`, and formats the text to a maximum of 70 characters per line.

---

## Advanced Usage and Tips

- **Handling Preformatted Text:**  
  If you have sections of text that should not be reflowed (such as code blocks), consider isolating them before processing with `fmt` or using options like `-u` to control how lines are treated.

- **Scripting and Automation:**  
  `fmt` can be easily integrated into scripts for automated text formatting, ensuring that documents and log files maintain a consistent appearance.

- **Combining with Other Text Utilities:**  
  Pair `fmt` with tools like `sed`, `awk`, or `tr` to perform more complex text transformations before or after formatting.

- **Locale and Character Widths:**  
  Be aware that `fmt` operates on character counts. In environments with multibyte or variable-width characters, the output may not perfectly match the specified width. Adjust your expectations or preprocess your text accordingly.

---

## Conclusion and Further Reading

The `fmt` command is a straightforward yet powerful tool for reformatting plain text, making it easier to produce consistently formatted documents and readable output. Whether you’re cleaning up paragraphs for an email, preparing text for publication, or automating document processing, `fmt` can help ensure that your text adheres to the desired layout and width.

### Further Reading and Resources

- **Manual Page:**  
  Access the detailed manual by typing:
  ```bash
  man fmt
  ```
- **Online Documentation:**
    - [GNU Coreutils: fmt Documentation](https://www.gnu.org/software/coreutils/fmt)
- **Tutorials and Examples:**  
  Look for community examples on forums and Q&A sites like [Stack Overflow](https://stackoverflow.com) to see creative uses of `fmt` in various scripting scenarios.

Experiment with `fmt` on your own text files to discover how it can streamline your document formatting workflows. Happy formatting!
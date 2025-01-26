# Chapter 27 - Regular Expressions

Regular expressions, often abbreviated as regex or regexp, are a powerful tool for pattern matching and text manipulation. They provide a way to search, validate, and manipulate strings based on patterns defined by a concise syntax. Regular expressions are widely used in programming, data analysis, web development, and more. Understanding regex can help solve many problems involving text efficiently and elegantly.

This article explores what regular expressions are, explains the syntax of common regex patterns, and provides practical examples in Python, PHP, Go, C++, and Zig.

# What Are Regular Expressions?

A regular expression is a sequence of characters that defines a search pattern. The pattern is used to match strings or parts of strings. Regex is often used for tasks such as:

- **Searching for substrings**: Identifying whether a substring exists in a string.
- **Validation**: Checking if a string matches a specific format (e.g., email validation).
- **Extraction**: Retrieving specific parts of a string.
- **Substitution**: Replacing parts of a string with another value.
- **Splitting strings**: Breaking a string into parts based on a delimiter pattern.

Regular expressions rely on a rich set of rules and symbols. Let's explore these components in depth.

# Components of Regular Expressions

## Literal Characters

Literal characters are the simplest form of regex. They match exactly what you type. For example:
- The regex `cat` matches the word "cat" in a string.

### Example on Literal Characters:
```python
import re
result = re.search(r'cat', 'The cat is on the mat')
print(result.group())  # Output: cat
```

## Metacharacters: Special Characters for Matching Patterns

Metacharacters have special meanings in regex. Below is a list of common metacharacters:

- `.`: Matches any single character except a newline.
- `^`: Matches the start of a string.
- `$`: Matches the end of a string.
- `*`: Matches zero or more occurrences of the preceding element.
- `+`: Matches one or more occurrences of the preceding element.
- `?`: Matches zero or one occurrence of the preceding element.
- `{}`: Specifies the number of occurrences (e.g., `{2,4}`).
- `[]`: Defines a character set to match one character.
- `|`: Acts as a logical OR.
- `()`: Groups expressions or captures matched content.
- `\\`: Escapes a metacharacter.

### Example on Metacharacters:
```python
import re
result = re.search(r'^The', 'The cat is on the mat')
print(result.group())  # Output: The
```

## Character Classes

Character classes allow you to match specific groups of characters:
- `[abc]`: Matches any of `a`, `b`, or `c`.
- `[^abc]`: Matches any character except `a`, `b`, or `c`.
- `[a-z]`: Matches any lowercase letter.
- `[A-Z]`: Matches any uppercase letter.
- `\d`: Matches any digit (0-9).
- `\D`: Matches any non-digit.
- `\w`: Matches any word character (alphanumeric + underscore).
- `\W`: Matches any non-word character.
- `\s`: Matches any whitespace character.
- `\S`: Matches any non-whitespace character.

### Example on Character Classes:
```python
import re
result = re.findall(r'\d+', 'Order number: 12345')
print(result)  # Output: ['12345']
```

## Anchors for Position Matching

Anchors do not match characters but positions in a string:
- `^`: Matches the start of a string.
- `$`: Matches the end of a string.
- `\b`: Matches a word boundary.
- `\B`: Matches a non-word boundary.

### Example on Anchors:
```python
import re
result = re.search(r'\bcat\b', 'The cat is on the mat')
print(result.group())  # Output: cat
```

## Quantifiers for Repetition

Quantifiers specify how many times a character or group should be matched:
- `*`: Zero or more times.
- `+`: One or more times.
- `?`: Zero or one time.
- `{n}`: Exactly `n` times.
- `{n,}`: At least `n` times.
- `{n,m}`: Between `n` and `m` times.

### Example on Quantifiers:
```python
import re
result = re.findall(r'a{2,3}', 'aa aaa aaaa')
print(result)  # Output: ['aa', 'aaa', 'aaa']
```

# Practical Applications of Regular Expressions

## Searching and Matching

Regular expressions are often used to search for patterns in strings. For instance, you can check if an email is valid:

### Example in Python:
```python
import re
pattern = r'^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$'
email = 'example@example.com'
if re.match(pattern, email):
    print('Valid email')
else:
    print('Invalid email')
```

## Replacing Strings

Replace parts of a string using regex with substitution functions:

### Example in PHP:
```php
<?php
$pattern = '/[0-9]+/';
$replacement = 'number';
$string = 'Order 12345';
$result = preg_replace($pattern, $replacement, $string);
echo $result; // Output: Order number
?>
```

## Splitting Strings

Split a string into parts based on a regex pattern:

### Example in Go:
```go
package main
import (
	"fmt"
	"regexp"
)
func main() {
	pattern := regexp.MustCompile(`\s+`)
	result := pattern.Split("Split this string", -1)
	fmt.Println(result) // Output: [Split this string]
}
```

## Validating Input

Validation ensures that user input matches the expected format:

### Example in C++:
```cpp
#include <iostream>
#include <regex>

int main() {
    std::string phone = "123-456-7890";
    std::regex pattern("^\\d{3}-\\d{3}-\\d{4}$");

    if (std::regex_match(phone, pattern)) {
        std::cout << "Valid phone number" << std::endl;
    } else {
        std::cout << "Invalid phone number" << std::endl;
    }

    return 0;
}
```

## Parsing Text with Complex Patterns

Regular expressions are ideal for extracting structured information from text.

### Example in Zig:
```zig
const std = @import("std");
const regex = std.regex;

pub fn main() anyerror!void {
    const pattern = try regex.compile("(\\d{3})-(\\d{3})-(\\d{4})");
    const text = "Contact: 123-456-7890";

    if (pattern.search(text)) |match| {
        std.debug.print("Match found: {s}\n", .{match});
    } else {
        std.debug.print("No match found\n", .{});
    }
}
```

# Conclusion

Regular expressions are a versatile and powerful tool for text processing. By mastering regex, you can efficiently handle tasks involving searching, validation, and text manipulation across multiple programming languages. Understanding the syntax and practical use cases will empower you to solve complex problems in a concise and elegant way.


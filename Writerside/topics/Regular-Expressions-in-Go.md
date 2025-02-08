# Regular Expressions in Go

*An In-Depth Guide to Working with Regular Expressions in Go*

Regular expressions (regex) are a powerful tool for text processing, validation, and transformation. In Go, regex support is provided by the standard library's [`regexp`](https://pkg.go.dev/regexp) package, which implements the RE2 engine. Unlike some regex implementations, RE2 emphasizes predictable performance and avoids pathological cases of exponential backtracking. This article explores the fundamentals and advanced topics of using regular expressions in Go, complete with practical examples and best practices.

---

## Table of Contents

1. [Introduction](#introduction)
2. [The `regexp` Package in Go](#the-regexp-package-in-go)
    - [Compilation and Safety](#compilation-and-safety)
    - [Matching Functions](#matching-functions)
3. [Regex Pattern Syntax in Go](#regex-pattern-syntax-in-go)
    - [Delimiters and Literal Strings](#delimiters-and-literal-strings)
    - [Character Classes, Quantifiers, and Groups](#character-classes-quantifiers-and-groups)
    - [Differences from Other Regex Engines](#differences-from-other-regex-engines)
4. [Practical Examples](#practical-examples)
    - [Validation and Extraction](#validation-and-extraction)
    - [Text Replacement and Splitting](#text-replacement-and-splitting)
    - [Using Functions for Dynamic Replacement](#using-functions-for-dynamic-replacement)
5. [Performance Considerations and Best Practices](#performance-considerations-and-best-practices)
6. [Advanced Techniques](#advanced-techniques)
7. [Conclusion](#conclusion)

---

## Introduction

Go's approach to regular expressions is centered on simplicity, efficiency, and safety. The [`regexp`](https://pkg.go.dev/regexp) package implements the RE2 engine, which guarantees linear-time execution by eliminating features that can cause exponential backtracking. This design choice makes Go's regex engine ideal for processing untrusted input and large data sets, though it does come with some limitations compared to more feature-rich engines like PCRE.

In this guide, you'll learn how to compile regex patterns, perform matches and substitutions, and harness the power of Go’s regex capabilities in your applications.

---

## The `regexp` Package in Go

The [`regexp`](https://pkg.go.dev/regexp) package is the cornerstone of regex operations in Go. It provides a variety of functions and methods for compiling, matching, and manipulating text using regular expressions.

### Compilation and Safety

Before using a regex, you must compile it into a [`Regexp`](https://pkg.go.dev/regexp#Regexp) object. There are two primary methods:

- **Compile:**  
  Returns a compiled regular expression or an error if the pattern is invalid.
  ```go
  re, err := regexp.Compile(`^Hello,?\s+world!$`)
  if err != nil {
      log.Fatal(err)
  }
  ```

- **MustCompile:**  
  Panics if the pattern cannot be compiled. Use this when you’re confident that the regex is valid.
  ```go
  re := regexp.MustCompile(`^Hello,?\s+world!$`)
  ```

### Matching Functions

Once compiled, the `Regexp` object offers several methods:

- **Match / MatchString:**  
  Check if the pattern matches any part of the text.
  ```go
  if re.MatchString("Hello, world!") {
      fmt.Println("Match found!")
  }
  ```

- **Find / FindString:**  
  Retrieve the first match found in the input.
  ```go
  match := re.FindString("Greetings, Hello, world! Have a nice day.")
  fmt.Println(match) // Output: "Hello, world!"
  ```

- **FindAll / FindAllString:**  
  Retrieve all matches in the input, with an optional limit.
  ```go
  matches := re.FindAllString("Hello, world! Hello, Go!", -1)
  fmt.Println(matches) // Output: [ "Hello, world!", "Hello, Go!" ]
  ```

- **ReplaceAll / ReplaceAllString:**  
  Replace all occurrences of the pattern with a replacement string.
  ```go
  result := re.ReplaceAllString("Hello, world!", "Hi, universe!")
  fmt.Println(result) // Output: "Hi, universe!"
  ```

- **Split:**  
  Split the input string around all matches of the pattern.
  ```go
  parts := re.Split("Hello, world! Hello, Go!", -1)
  fmt.Println(parts)
  ```

---

## Regex Pattern Syntax in Go

Go’s regex syntax is based on the RE2 engine, which is similar to Perl’s but with some important differences.

### Delimiters and Literal Strings

Unlike some languages (e.g., PHP or JavaScript) where patterns are enclosed in delimiters, Go represents regex patterns as plain string literals. This means you write your regex directly as a Go string:
```go
pattern := `\d{3}-\d{2}-\d{4}`
```
Using backticks (`) helps avoid the need to escape backslashes, though you can also use regular string literals with proper escaping.

### Character Classes, Quantifiers, and Groups

- **Character Classes:**  
  Use square brackets to define a set of characters:
  ```go
  [A-Za-z0-9]
  ```
  Predefined classes such as `\d` (digit), `\w` (word character), and `\s` (whitespace) are supported.

- **Quantifiers:**  
  Define repetition using:
    - `*` (0 or more)
    - `+` (1 or more)
    - `?` (0 or 1)
    - `{n}` (exactly n)
    - `{n,}` (n or more)
    - `{n,m}` (between n and m)

- **Groups and Capturing:**  
  Parentheses create groups that capture parts of the match.
  ```go
  re := regexp.MustCompile(`(\w+)\s+(\w+)`)
  ```
  You can retrieve captured groups using the `FindStringSubmatch` method:
  ```go
  input := "Hello World"
  matches := re.FindStringSubmatch(input)
  // matches[1] will contain "Hello" and matches[2] will contain "World"
  ```

### Differences from Other Regex Engines

- **No Backreferences:**  
  RE2 does not support backreferences (e.g., `\1`), which makes it faster and less prone to catastrophic backtracking.

- **No Lookahead/Lookbehind:**  
  While some advanced features like lookahead or lookbehind assertions are missing, the available syntax is sufficient for many practical use cases.

- **Unicode Support:**  
  Go’s regex engine supports Unicode. For example, `\p{L}` matches any Unicode letter:
  ```go
  re := regexp.MustCompile(`\p{L}+`)
  ```

---

## Practical Examples

### Validation and Extraction

#### Example 1: Validating an Email Address
```go
package main

import (
	"fmt"
	"log"
	"regexp"
)

func main() {
	// A simple email validation pattern
	pattern := `^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$`
	re, err := regexp.Compile(pattern)
	if err != nil {
		log.Fatal(err)
	}

	email := "user@example.com"
	if re.MatchString(email) {
		fmt.Println("Valid email!")
	} else {
		fmt.Println("Invalid email.")
	}
}
```

#### Example 2: Extracting Date Components
```go
package main

import (
	"fmt"
	"log"
	"regexp"
)

func main() {
	pattern := `^(\d{4})-(\d{2})-(\d{2})$`
	re := regexp.MustCompile(pattern)
	date := "2025-02-08"
	matches := re.FindStringSubmatch(date)
	if matches == nil {
		fmt.Println("Invalid date format.")
		return
	}

	year := matches[1]
	month := matches[2]
	day := matches[3]
	fmt.Printf("Year: %s, Month: %s, Day: %s\n", year, month, day)
}
```

### Text Replacement and Splitting

#### Example 3: Replacing Patterns
```go
package main

import (
	"fmt"
	"regexp"
)

func main() {
	re := regexp.MustCompile(`\d+`)
	text := "There are 123 apples and 456 oranges."
	result := re.ReplaceAllString(text, "number")
	fmt.Println(result)
	// Output: "There are number apples and number oranges."
}
```

#### Example 4: Splitting a String
```go
package main

import (
	"fmt"
	"regexp"
)

func main() {
	re := regexp.MustCompile(`\s+`)
	text := "Split   this sentence into words."
	words := re.Split(text, -1)
	fmt.Println(words)
	// Output: [ "Split", "this", "sentence", "into", "words." ]
}
```

### Using Functions for Dynamic Replacement

Go’s `ReplaceAllStringFunc` allows you to perform dynamic replacements by passing a function that processes each match:
```go
package main

import (
	"fmt"
	"regexp"
	"strconv"
)

func main() {
	re := regexp.MustCompile(`\d+`)
	text := "The price is 100 USD, and the discount is 20 USD."
	// Increase each number by 10%
	result := re.ReplaceAllStringFunc(text, func(match string) string {
		number, err := strconv.Atoi(match)
		if err != nil {
			return match
		}
		return strconv.Itoa(int(float64(number) * 1.1))
	})
	fmt.Println(result)
	// Example Output: "The price is 110 USD, and the discount is 22 USD."
}
```

---

## Performance Considerations and Best Practices

- **Predictable Performance:**  
  Thanks to RE2, Go’s regex engine guarantees linear-time performance for matching. However, writing overly generic patterns may still affect performance.

- **Pre-compile Patterns:**  
  Compile regex patterns once (using `regexp.MustCompile` if safe) and reuse them to avoid the overhead of repeated compilation.

- **Use Raw String Literals:**  
  Using backticks for regex patterns reduces the need for escaping, making your patterns clearer and easier to maintain.
  ```go
  re := regexp.MustCompile(`\b\w+\b`)
  ```

- **Test Thoroughly:**  
  Always test your regex patterns with representative inputs to ensure they work as intended and perform well under expected loads.

---

## Advanced Techniques

### Parsing with Submatches and Named Capture (Simulated)

While Go’s regex engine does not support named capture groups directly, you can simulate them by tracking submatch indices:
```go
package main

import (
	"fmt"
	"regexp"
)

func main() {
	// Simulate named capture for a simple pattern (first name and last name)
	re := regexp.MustCompile(`^(\w+)\s+(\w+)$`)
	input := "John Doe"
	matches := re.FindStringSubmatch(input)
	if matches == nil {
		fmt.Println("No match found.")
		return
	}

	// Define names for each capture group
	captureNames := []string{"Full Match", "FirstName", "LastName"}
	for i, match := range matches {
		fmt.Printf("%s: %s\n", captureNames[i], match)
	}
	// Output:
	// Full Match: John Doe
	// FirstName: John
	// LastName: Doe
}
```

### Handling Unicode

Go’s regex engine handles Unicode characters gracefully. Use Unicode properties such as `\p{L}` to match any kind of letter:
```go
package main

import (
	"fmt"
	"regexp"
)

func main() {
	re := regexp.MustCompile(`\p{L}+`)
	text := "Café 北京 Привет"
	words := re.FindAllString(text, -1)
	fmt.Println(words)
	// Output: [ "Café", "北京", "Привет" ]
}
```

---

## Conclusion

Working with regular expressions in Go is both powerful and efficient thanks to the RE2 engine, which ensures predictable performance without sacrificing expressiveness. By understanding how to compile, match, replace, and split text using the [`regexp`](https://pkg.go.dev/regexp) package, you can effectively harness regex for data validation, parsing, and transformation in your Go applications.

Whether you're validating user input, processing logs, or dynamically modifying text, the examples and best practices outlined in this guide provide a solid foundation for integrating regex into your Go projects. As always, test your patterns thoroughly and choose the right balance between expressiveness and performance for your specific use case. Happy coding!
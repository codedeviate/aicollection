# Regular Expressions in Zig

*An In-Depth Guide to Working with Regular Expressions in Zig*

Regular expressions (regex) are indispensable tools for text processing, pattern matching, and data validation. While languages such as Go and PHP come with mature, built-in regex support, Zig—a relatively new systems programming language—does not yet include a regex engine in its standard library. However, Zig’s flexibility and powerful compile-time features make it straightforward to integrate regex functionality through third-party libraries or via the C Foreign Function Interface (FFI). In this guide, we’ll explore the current options for working with regex in Zig, provide practical examples, and discuss best practices for integrating regex into your Zig projects.

---

## Table of Contents

1. [Introduction](#introduction)
2. [The State of Regex in Zig](#the-state-of-regex-in-zig)
    - [Third-Party Libraries](#third-party-libraries)
    - [Interfacing with C Libraries](#interfacing-with-c-libraries)
3. [Using a Third-Party Regex Library in Zig](#using-a-third-party-regex-library-in-zig)
    - [Example: Using `zig-regex`](#example-using-zig-regex)
4. [Using C Libraries for Regex (PCRE2) via FFI](#using-c-libraries-for-regex-pcre2-via-ffi)
5. [Practical Examples](#practical-examples)
    - [Validation and Extraction](#validation-and-extraction)
    - [Text Replacement and Splitting](#text-replacement-and-splitting)
6. [Error Handling, Performance, and Best Practices](#error-handling-performance-and-best-practices)
7. [Conclusion](#conclusion)

---

## Introduction

Zig is a modern, low-level programming language designed for performance, safety, and ease of cross-compilation. Although it lacks a built-in regular expression engine in its standard library (as of this writing), Zig’s rich ecosystem and its straightforward interoperability with C provide effective ways to work with regex. Whether you prefer a pure-Zig solution with a third-party library or want to leverage the mature PCRE2 engine via FFI, this guide will help you integrate regular expressions into your Zig projects.

---

## The State of Regex in Zig

### Third-Party Libraries

The Zig community has produced several third-party libraries that bring regex functionality to Zig. One notable example is [zig-regex](https://github.com/ratfactor/zig-regex), which offers a regex engine written in Zig. Although these libraries may not be as feature-rich as mature engines like PCRE2, they can be perfectly adequate for many tasks, and they benefit from Zig’s compile-time checking and simplicity.

### Interfacing with C Libraries

For applications that require robust and feature-rich regex capabilities, you can use Zig’s C FFI to interface with existing C libraries such as PCRE or PCRE2. This approach lets you leverage the power and maturity of these libraries while writing your application logic in Zig. The trade-off is the additional complexity of dealing with C’s API and managing memory manually, but Zig’s safety features help mitigate many of these challenges.

---

## Using a Third-Party Regex Library in Zig

In this section, we’ll illustrate how to use a third-party regex library in Zig. We’ll assume the existence of a library (for example, [zig-regex](https://github.com/ratfactor/zig-regex)) that exposes a straightforward API for compiling regex patterns, matching text, and extracting captured groups.

### Example: Using `zig-regex`

Below is an example of how you might use a Zig regex library to match and extract text from a string. (Note that the API shown is illustrative; consult your chosen library’s documentation for exact usage details.)

```zig
const std = @import("std");
const regex = @import("zig-regex"); // Assumes you have added zig-regex as a dependency

pub fn main() !void {
    var allocator = std.heap.page_allocator;

    // Compile a regex pattern to match a simple pattern: two words separated by whitespace.
    // The pattern captures two groups: the first and second words.
    var re = try regex.compile(allocator, `^(\w+)\s+(\w+)$`, .{});
    defer re.deinit();

    const input = "Hello World";
    const match = re.match(input) orelse {
        std.debug.print("No match found.\n", .{});
        return;
    };

    // Access captured groups. For example, group 1 is "Hello" and group 2 is "World".
    const firstWord = match.group(0); // Full match ("Hello World")
    const secondWord = match.group(1); // First captured group ("Hello")
    const thirdWord = match.group(2);  // Second captured group ("World")

    std.debug.print("Full Match: {}\n", .{firstWord});
    std.debug.print("First Word: {}\n", .{secondWord});
    std.debug.print("Second Word: {}\n", .{thirdWord});
}
```

**Key Points:**
- The regex is compiled at runtime using an allocator.
- The pattern is written as a raw string literal (using backticks) to avoid excessive escaping.
- The API provides methods for matching and retrieving captured groups.

---

## Using C Libraries for Regex (PCRE2) via FFI

If your application demands advanced regex features (such as backreferences, lookaround assertions, or extensive Unicode support), you might opt to use a C library like PCRE2 via Zig’s FFI. Below is a simplified outline of the steps involved:

1. **Set Up the FFI:**  
   Use `@cImport` to include the necessary C headers for PCRE2.

   ```zig
   const std = @import("std");
   const c = @cImport({
       @cInclude("pcre2.h");
   });
   ```

2. **Compile and Execute Regex:**  
   Write Zig wrappers around PCRE2’s API functions. This typically involves:
    - Compiling a regex pattern using `pcre2_compile`.
    - Matching against a string using `pcre2_match`.
    - Handling memory management and error codes.

3. **Example Skeleton:**

   ```zig
   const std = @import("std");
   const c = @cImport({
       @cInclude("pcre2.h");
   });

   pub fn main() !void {
       var allocator = std.heap.page_allocator;
       
       // Define the pattern and subject string
       const pattern = "^(\\w+)\\s+(\\w+)$";
       const subject = "Hello World";
       
       // Set up PCRE2 compilation (error handling omitted for brevity)
       var errorcode: c.int = 0;
       var erroroffset: c.size_t = 0;
       const re = c.pcre2_compile(
           pattern, // pattern
           std.mem.len(pattern), // length of pattern
           0,       // options
           &errorcode,
           &erroroffset,
           null     // use default character tables
       );
       if (re == null) {
           std.debug.print("PCRE2 compilation error at offset {}: {}\n", .{ erroroffset, errorcode });
           return;
       }
       defer c.pcre2_code_free(re);
       
       // Allocate a match data block
       const match_data = c.pcre2_match_data_create_from_pattern(re, null);
       if (match_data == null) {
           std.debug.print("Failed to allocate match data.\n", .{});
           return;
       }
       defer c.pcre2_match_data_free(match_data);
       
       // Perform the match
       const rc = c.pcre2_match(re, subject, std.mem.len(subject), 0, 0, match_data, null);
       if (rc < 0) {
           std.debug.print("No match found or error occurred: {}\n", .{ rc });
           return;
       }
       
       // Extract captured substrings (this example extracts the first captured group)
       var ovector: [30]c.uint = undefined;
       _ = c.pcre2_jit_stack_assign(re, ovector.ptr, ovector.len);
       // Further extraction code would go here, using pcre2_substring_get_bynumber, etc.
       
       std.debug.print("Match found using PCRE2 via FFI.\n", .{});
   }
   ```

**Note:**  
Interfacing with C libraries requires careful management of resources and understanding of the C API. Consult the PCRE2 documentation and consider wrapping the FFI calls in safer, idiomatic Zig code if you choose this route.

---

## Practical Examples

### Validation and Extraction

#### Example 1: Validating an Email Address (Using zig-regex)
```zig
const std = @import("std");
const regex = @import("zig-regex");

pub fn main() !void {
    var allocator = std.heap.page_allocator;

    // A simple email validation pattern.
    var re = try regex.compile(allocator, `^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$`, .{});
    defer re.deinit();

    const email = "user@example.com";
    if (re.match(email)) {
        std.debug.print("Valid email!\n", .{});
    } else {
        std.debug.print("Invalid email.\n", .{});
    }
}
```

#### Example 2: Extracting Date Components (Using zig-regex)
```zig
const std = @import("std");
const regex = @import("zig-regex");

pub fn main() !void {
    var allocator = std.heap.page_allocator;

    // Pattern to capture a date in the format YYYY-MM-DD.
    var re = try regex.compile(allocator, `^(\d{4})-(\d{2})-(\d{2})$`, .{});
    defer re.deinit();

    const date = "2025-02-08";
    const match = re.match(date) orelse {
        std.debug.print("Invalid date format.\n", .{});
        return;
    };

    std.debug.print("Year: {}\n", .{match.group(1)});
    std.debug.print("Month: {}\n", .{match.group(2)});
    std.debug.print("Day: {}\n", .{match.group(3)});
}
```

### Text Replacement and Splitting

While many third-party Zig regex libraries may provide basic matching and extraction capabilities, text replacement and splitting functions can be implemented by iterating over matches and rebuilding the string. As libraries mature, expect more built-in utility functions for these tasks.

---

## Error Handling, Performance, and Best Practices

- **Error Handling:**  
  Always check for errors when compiling regex patterns. Third-party libraries typically return errors or error unions, and when using C libraries via FFI, inspect error codes and manage resources carefully.

- **Performance:**  
  Pre-compile regex patterns when reusing them in performance-critical sections of your code. Zig’s compile-time capabilities also enable you to potentially perform regex compilation during build time, though this depends on the library.

- **Testing:**  
  Validate your regex patterns with a variety of input data to ensure correctness and robustness, especially when processing untrusted input.

- **Memory Management:**  
  Zig’s explicit memory management means you must manage allocators and deinitialize regex objects properly to avoid leaks.

---

## Conclusion

Although Zig does not include built-in regex support in its standard library, you have multiple options for integrating regular expressions into your projects. Whether you choose a pure-Zig solution via a third-party library like `zig-regex` or leverage mature C libraries such as PCRE2 via Zig’s FFI, you can harness the power of regex in your applications. By following best practices for error handling, performance, and resource management, you can effectively use regular expressions for validation, extraction, and text processing in Zig.

As Zig continues to evolve, we can expect further enhancements and possibly even native regex support in the future. Until then, the approaches outlined in this guide will help you build robust, efficient, and maintainable regex-based solutions in your Zig projects. Happy coding!
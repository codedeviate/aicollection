# Regular Expressions in Javascript (Node, Bun and Deno)

*An In-Depth Guide to Working with Regular Expressions in JavaScript (Node, Bun, and Deno)*

Regular expressions (regex) are one of the most powerful tools available in JavaScript for pattern matching, text manipulation, and data validation. Whether you’re building backend services with Node.js, experimenting with Bun, or developing secure applications with Deno, JavaScript’s regex capabilities are built into the language and follow the ECMAScript standard. In this guide, we will explore the core concepts, syntax, advanced techniques, and practical examples of using regular expressions in JavaScript across these modern runtimes.

---

## Table of Contents

1. [Introduction](#introduction)
2. [The JavaScript RegExp Object](#the-javascript-regexp-object)
    - [Creating Regular Expressions](#creating-regular-expressions)
    - [Regex Flags and Modifiers](#regex-flags-and-modifiers)
3. [Regex Syntax and Features](#regex-syntax-and-features)
    - [Character Classes and Quantifiers](#character-classes-and-quantifiers)
    - [Capturing Groups and Named Groups](#capturing-groups-and-named-groups)
    - [Lookahead and Lookbehind Assertions](#lookahead-and-lookbehind-assertions)
    - [Unicode Mode and the `/u` Flag](#unicode-mode-and-the-u-flag)
4. [Working with Regex in JavaScript](#working-with-regex-in-javascript)
    - [Matching Methods](#matching-methods)
    - [Replacing Text](#replacing-text)
    - [Splitting Strings](#splitting-strings)
    - [Using `matchAll` for Iterating Matches](#using-matchall-for-iterating-matches)
5. [Practical Examples](#practical-examples)
    - [Validating an Email Address](#validating-an-email-address)
    - [Extracting Date Components](#extracting-date-components)
    - [Dynamic Replacement with Callbacks](#dynamic-replacement-with-callbacks)
6. [Environment-Specific Considerations](#environment-specific-considerations)
    - [Node.js](#node-js)
    - [Bun](#bun)
    - [Deno](#deno)
7. [Performance and Best Practices](#performance-and-best-practices)
8. [Debugging and Error Handling](#debugging-and-error-handling)
9. [Conclusion](#conclusion)

---

## Introduction

JavaScript’s built-in support for regular expressions means you can immediately use regex to parse, validate, and transform strings without relying on external libraries. This capability is consistent across popular JavaScript runtimes such as Node.js, Bun, and Deno. With modern improvements like named capture groups and lookbehind assertions now available in many environments, JavaScript regex has grown even more expressive and useful.

---

## The JavaScript RegExp Object

### Creating Regular Expressions

There are two main ways to create a regular expression in JavaScript:

1. **Literal Notation:**  
   Use forward slashes (`/pattern/flags`) to define a regex literal.
   ```javascript
   const regexLiteral = /hello\s+world/i;
   ```

2. **Constructor Function:**  
   Use the `RegExp` constructor for dynamic patterns.
   ```javascript
   const pattern = "hello\\s+world";
   const regexFromConstructor = new RegExp(pattern, "i");
   ```

### Regex Flags and Modifiers

Common flags include:

- **`i`**: Case-insensitive matching
- **`g`**: Global search (find all matches)
- **`m`**: Multiline mode (affects `^` and `$`)
- **`s`**: Dotall mode, so that `.` matches newline characters
- **`u`**: Unicode mode, enabling proper handling of Unicode characters
- **`y`**: Sticky matching (match starting at `lastIndex`)

Example:
```javascript
const regex = /(\d{3})-(\d{2})-(\d{4})/g; // For matching a social security number pattern
```

---

## Regex Syntax and Features

### Character Classes and Quantifiers

- **Character Classes:**  
  `[A-Za-z0-9]` matches any alphanumeric character; predefined classes like `\d` (digit), `\w` (word character), and `\s` (whitespace) are also available.

- **Quantifiers:**
    - `*` – zero or more
    - `+` – one or more
    - `?` – zero or one
    - `{n}` – exactly _n_ times
    - `{n,}` – _n_ or more times
    - `{n,m}` – between _n_ and _m_ times

Example:
```javascript
const phoneRegex = /\d{3}-\d{3}-\d{4}/; // Matches phone numbers like 123-456-7890
```

### Capturing Groups and Named Groups

Parentheses `()` capture submatches. Modern JavaScript (ES2018+) supports named capture groups:
```javascript
const nameRegex = /(?<first>\w+)\s+(?<last>\w+)/;
const str = "John Doe";
const match = str.match(nameRegex);
if (match) {
  console.log(match.groups.first); // "John"
  console.log(match.groups.last);  // "Doe"
}
```

### Lookahead and Lookbehind Assertions

JavaScript supports zero-width assertions:
- **Positive Lookahead:** `(?=...)`
- **Negative Lookahead:** `(?!...)`
- **Positive Lookbehind:** `(?<=...)` (supported in modern engines)
- **Negative Lookbehind:** `(?<!...)`

Example:
```javascript
const lookaheadRegex = /foo(?=bar)/;
console.log("foobar".match(lookaheadRegex)); // Matches "foo" only if followed by "bar"

const lookbehindRegex = /(?<=\$)\d+/u;
console.log("$100".match(lookbehindRegex)); // Matches "100" if preceded by a dollar sign
```

### Unicode Mode and the `/u` Flag

Using the `/u` flag ensures that regex patterns handle Unicode characters properly:
```javascript
const unicodeRegex = /\p{L}+/gu;  // Matches one or more Unicode letters
console.log("Café 北京".match(unicodeRegex)); // ["Café", "北京"]
```

---

## Working with Regex in JavaScript

### Matching Methods

- **`String.prototype.match()`**:  
  Returns an array of matches (or `null` if no match is found).
  ```javascript
  const result = "hello world".match(/world/);
  console.log(result); // ["world"]
  ```

- **`RegExp.prototype.test()`**:  
  Returns a boolean indicating whether the pattern matches the string.
  ```javascript
  const regex = /world/;
  console.log(regex.test("hello world")); // true
  ```

### Replacing Text

- **`String.prototype.replace()`**:  
  Replace matched patterns with a replacement string or a function.
  ```javascript
  const newText = "I have 100 apples".replace(/\d+/, (match) => Number(match) * 2);
  console.log(newText); // "I have 200 apples"
  ```

### Splitting Strings

- **`String.prototype.split()`**:  
  Split a string based on a regex delimiter.
  ```javascript
  const words = "Split  this   sentence".split(/\s+/);
  console.log(words); // ["Split", "this", "sentence"]
  ```

### Using `matchAll` for Iterating Matches

For iterating over all matches including capturing groups:
```javascript
const text = "Numbers: 42, 100, 7";
const regex = /\d+/g;
for (const match of text.matchAll(regex)) {
  console.log(match[0]);  // Logs each number found
}
```

---

## Practical Examples

### Validating an Email Address

A simple email validation pattern:
```javascript
const email = "user@example.com";
const emailRegex = /^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$/;
if (emailRegex.test(email)) {
  console.log("Valid email address.");
} else {
  console.log("Invalid email address.");
}
```

### Extracting Date Components

Extracting year, month, and day from a date string:
```javascript
const dateStr = "2025-02-08";
const dateRegex = /^(\d{4})-(\d{2})-(\d{2})$/;
const dateMatch = dateStr.match(dateRegex);
if (dateMatch) {
  const [, year, month, day] = dateMatch;
  console.log(`Year: ${year}, Month: ${month}, Day: ${day}`);
} else {
  console.log("Invalid date format.");
}
```

### Dynamic Replacement with Callbacks

Using a callback to modify matched text:
```javascript
const text = "Discount: 20%, 30%, and 50%";
const updatedText = text.replace(/\d+%/g, (match) => {
  // Increase each discount by 5%
  const value = parseInt(match, 10);
  return `${value + 5}%`;
});
console.log(updatedText); // "Discount: 25%, 35%, and 55%"
```

---

## Environment-Specific Considerations

### Node.js

- **Runtime:**  
  Node.js uses the V8 engine, ensuring that JavaScript regex features are up-to-date.
- **Usage:**  
  Regex operations are used throughout Node.js applications, from server-side validations to log processing.
- **Tip:**  
  Leverage modules and npm packages that further extend regex capabilities if needed.

### Bun

- **Runtime:**  
  Bun is a fast JavaScript runtime that also uses modern JavaScript standards.
- **Usage:**  
  Due to Bun’s focus on speed, regex operations are highly optimized, making it ideal for performance-critical applications.
- **Tip:**  
  Ensure you’re running a recent version of Bun to take full advantage of modern regex features like lookbehind assertions and Unicode support.

### Deno

- **Runtime:**  
  Deno is built on the V8 engine with a secure-by-default design.
- **Usage:**  
  Deno’s standard library and built-in TypeScript support make regex operations straightforward and type-safe.
- **Tip:**  
  Deno’s permission model requires explicit file or network access; this does not affect regex directly but is worth keeping in mind when processing external data.

---

## Performance and Best Practices

- **Pre-Compile Patterns:**  
  If a regex pattern is used repeatedly, store it in a constant rather than recreating it.
- **Use Appropriate Flags:**  
  Apply flags like `g`, `i`, and `u` only when necessary.
- **Keep Patterns Readable:**  
  Use comments (with verbose mode or external documentation) for complex regexes.
- **Test Thoroughly:**  
  Validate your patterns against a diverse set of input data.
- **Be Aware of Engine Differences:**  
  While Node, Bun, and Deno largely follow the ECMAScript standard, always test in your target environment to ensure compatibility.

---

## Debugging and Error Handling

- **Error Handling:**  
  Invalid regex patterns in JavaScript throw a `SyntaxError`. Use try-catch blocks during development to catch these issues.
  ```javascript
  try {
    const faultyRegex = new RegExp("([A-Z"); // Missing closing bracket
  } catch (e) {
    console.error("Regex error:", e.message);
  }
  ```
- **Debugging Tools:**  
  Use browser developer tools or Node.js debugging utilities to step through regex operations and inspect match results.
- **Online Testers:**  
  Platforms like [regex101](https://regex101.com/) and [RegExr](https://regexr.com/) support ECMAScript regex and are excellent for building and testing patterns.

---

## Conclusion

JavaScript’s native regex support is robust, versatile, and consistent across modern runtimes like Node.js, Bun, and Deno. With built-in features for pattern matching, text transformation, and data validation—and with modern enhancements such as named capture groups, lookbehind assertions, and Unicode support—JavaScript regex empowers developers to solve complex text processing challenges efficiently.

By understanding the core syntax, leveraging advanced techniques, and following best practices for performance and readability, you can harness the full potential of regular expressions in your JavaScript applications. Whether you’re building server-side logic, command-line tools, or secure web applications, the powerful regex capabilities in JavaScript are an essential part of your toolkit.

Happy pattern matching!
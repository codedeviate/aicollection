# Chapter 14a - Basic Data Types

Data types are foundational to programming, defining how data is stored, manipulated, and understood by a program. Each data type specifies what kind of data a variable can hold, as well as the operations that can be performed on that data. This concept is vital for creating efficient, error-free, and maintainable code.

Programming languages provide a variety of data types to represent numbers, text, and more specialized types like bytes, signed/unsigned integers, and floating-point values. These types allow developers to control memory usage and optimize performance in different applications.

In this article, we will explore the most common data types across programming languages, including Python, PHP, C++, Go, and Zig. We’ll examine their variations, uses, and examples in detail.

---

## Basic Data Types: Numbers, Text, and Boolean Values

Basic data types are the simplest forms of data a program can handle. They include numbers (integers and floating-point), text (characters and strings), and boolean values (true/false). Some languages also provide specialized types like bytes, words, signed/unsigned integers, and high-precision floats for specific use cases.

---

### Numeric Data Types: Backbone of Calculations

#### **Integers (Whole Numbers)**
Integers represent whole numbers, both positive and negative, including zero. They are used for counting, indexing, and performing arithmetic operations.

Most programming languages provide multiple integer types, such as:
- **Signed Integers:** Represent both positive and negative numbers.
- **Unsigned Integers:** Represent only non-negative numbers, effectively doubling the positive range.
- **Bit-Specific Integers:** Integers of fixed sizes (e.g., 8, 16, 32, or 64 bits).

**Code Examples:**
```python
# Python
signed_int = -42
unsigned_int = 42  # Python doesn't enforce unsigned integers explicitly.

# PHP
$signed_int = -42;
$unsigned_int = 42;

# C++
int16_t signed_int = -42;
uint16_t unsigned_int = 42;

# Go
var signed_int int16 = -42
var unsigned_int uint16 = 42

# Zig
const signed_int: i16 = -42;
const unsigned_int: u16 = 42;
```

---

#### **Floating-Point Numbers (Decimals)**
Floating-point numbers represent real numbers with a fractional part. These are available in single precision (`float`) and double precision (`double`) formats, and in some languages, extended precision (`float80` or `float128`).

**Examples of Use:**
- Measurements like temperature, speed, or weight.
- Complex calculations in scientific computing.

**Code Examples:**
```python
# Python
float_value = 3.14159  # Double precision by default.

# PHP
$float_value = 3.14159;

# C++
float float_value = 3.14159f;  // Single precision.
double double_value = 3.141592653589793;  // Double precision.

# Go
var float_value float32 = 3.14159
var double_value float64 = 3.141592653589793

# Zig
const float_value: f32 = 3.14159;
const double_value: f64 = 3.141592653589793;
```

---

#### **Bytes and Words**

**Bytes** are 8-bit unsigned integers commonly used for binary data and file handling. **Words** refer to the natural data size of the system's architecture (e.g., 16-bit, 32-bit, or 64-bit).

**Code Examples:**
```python
# Python
byte_value = bytes([65])  # ASCII value for 'A'.

# PHP
$byte_value = chr(65);  // 'A'

# C++
unsigned char byte_value = 65;

# Go
var byte_value byte = 65  // Equivalent to uint8

# Zig
const byte_value: u8 = 65;
```

---

### Textual Data Types: Characters and Strings

Textual data types represent sequences of characters or individual symbols. These are critical for user input, text processing, and file operations.

#### **Characters (Single Symbols)**
A `char` stores a single character, such as a letter, digit, or punctuation mark. Some languages provide Unicode-compatible wide characters for internationalization.

**Code Examples:**
```python
# Python
char_value = 'A'

# PHP
$char_value = 'A';

# C++
char char_value = 'A';

# Go
var char_value rune = 'A'  // Runes represent Unicode code points.

# Zig
const char_value: u8 = 'A';
```

---

#### **Strings (Sequences of Characters)**
Strings are used for handling text and are often immutable in modern languages. They support operations like concatenation, slicing, and searching.

**Code Examples:**
```python
# Python
string_value = "Hello, World!"

# PHP
$string_value = "Hello, World!";

# C++
std::string string_value = "Hello, World!";

# Go
var string_value string = "Hello, World!"

# Zig
const string_value = "Hello, World!";
```

---

### Boolean Data Types: True and False

Booleans represent logical states: `true` or `false`. These are fundamental in conditional statements, loops, and logical expressions.

**Code Examples:**
```python
# Python
is_valid = True

# PHP
$is_valid = true;

# C++
bool is_valid = true;

# Go
var is_valid bool = true

# Zig
const is_valid: bool = true;
```

---

## Advanced Numeric and Specialized Data Types

### Decimals and High-Precision Numbers

Some languages, like Python, provide specialized types for high-precision calculations, often used in financial applications.

**Code Example in Python:**
```python
from decimal import Decimal
precise_value = Decimal("3.141592653589793238462643383279")
```

---

### Complex Numbers

Complex numbers consist of real and imaginary parts. They are available in Python, Go, and other languages for scientific applications.

**Code Examples in Go:**
```go
var complexNumber complex64 = 3 + 4i
fmt.Printf("Complex number: %v\n", complexNumber)
```

---

## Conclusion

Data types are the foundation of all programming, dictating how data is stored, manipulated, and retrieved. By understanding the intricacies of numeric types (like signed/unsigned integers and floats), textual types (characters and strings), and boolean logic, developers can write efficient and robust programs. Advanced types like bytes, complex numbers, and high-precision decimals provide even greater control and functionality for specialized applications. Whether you're using Python, PHP, C++, Go, or Zig, mastering these data types is essential for building reliable and efficient software.

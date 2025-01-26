# Chapter 39 - Command Line Flags

Command-line flags (or options) are parameters passed to a program during its execution in the command line interface (CLI). They allow users to control the program's behavior without altering its source code. Command-line flags are commonly used to provide additional information or enable/disable features in a program.

For example, when running a program like `ls` on Linux, you can use flags such as `-l` for detailed output or `-a` to show hidden files.

This article explores command-line flags, including the different types, their purposes, and how to implement them in various programming languages.

---

## What Are Command-Line Flags?

Command-line flags are specific identifiers that modify how a program runs. They can be single-character options (e.g., `-v`) or longer, more descriptive options (e.g., `--verbose`). Flags are used for a variety of purposes, such as:

- **Setting configurations**: Example: `--config=/path/to/config`.
- **Enabling verbose/debug modes**: Example: `-v` or `--verbose`.
- **Specifying input/output files**: Example: `-i input.txt -o output.txt`.
- **Toggling features**: Example: `--enable-feature` or `--disable-feature`.
- **Providing help or usage information**: Example: `-h` or `--help`.

Command-line flags can be required, optional, or have default values. Programs often combine flags with positional arguments to enable flexible and powerful configurations.

---

## Types of Command-Line Flags

### Boolean Flags
Boolean flags act as switches to enable or disable a specific feature. For example:
- `-v` enables verbose mode.
- `--debug` turns on debugging.

### Value-Based Flags
These flags accept a value as input, such as a file path, number, or string. For example:
- `--input=input.txt` specifies an input file.
- `--port=8080` sets the server port.

### Multi-Value Flags
Some flags can accept multiple values, often separated by commas or by repeating the flag. For example:
- `--files=file1.txt,file2.txt`.
- `--file file1.txt --file file2.txt`.

### Help and Usage Flags
Help flags (`-h`, `--help`) display information about how to use the program. These are essential for making programs user-friendly.

### Combined Flags
Flags can be combined for brevity if they don't require values. For example:
- `-abc` is equivalent to `-a -b -c`.

---

## How to Use Command-Line Flags in Python, PHP, Go, C++, and Zig

### Implementing Command-Line Flags in Python

Python's `argparse` module makes it easy to work with command-line flags:

```python
import argparse

parser = argparse.ArgumentParser(description="Example program with command-line flags")
parser.add_argument("-v", "--verbose", action="store_true", help="Enable verbose output")
parser.add_argument("-i", "--input", type=str, help="Input file")
parser.add_argument("-n", "--number", type=int, default=10, help="Specify a number (default: 10)")

args = parser.parse_args()

if args.verbose:
    print("Verbose mode enabled")

if args.input:
    print(f"Input file: {args.input}")

print(f"Number: {args.number}")
```

Run this script with:
```
python script.py -v -i example.txt -n 42
```

---

### Command-Line Flags in PHP

PHP provides access to command-line arguments via the `$argv` array or libraries like `getopt`.

```php
$options = getopt("vhi:n:", ["verbose", "help", "input:", "number:"]);

if (isset($options['h']) || isset($options['help'])) {
    echo "Usage: php script.php [options]\n";
    echo "  -v, --verbose   Enable verbose output\n";
    echo "  -i, --input     Input file\n";
    echo "  -n, --number    Specify a number\n";
    exit(0);
}

if (isset($options['v']) || isset($options['verbose'])) {
    echo "Verbose mode enabled\n";
}

if (isset($options['i'])) {
    echo "Input file: " . $options['i'] . "\n";
}

if (isset($options['n'])) {
    echo "Number: " . $options['n'] . "\n";
}
```

Run this script with:
```
php script.php -v -i=example.txt -n=42
```

---

### Handling Flags in Go

Go has a built-in `flag` package for handling flags:

```go
package main

import (
	"flag"
	"fmt"
)

func main() {
	verbose := flag.Bool("verbose", false, "Enable verbose output")
	input := flag.String("input", "", "Input file")
	number := flag.Int("number", 10, "Specify a number (default: 10)")

	flag.Parse()

	if *verbose {
		fmt.Println("Verbose mode enabled")
	}

	if *input != "" {
		fmt.Println("Input file:", *input)
	}

	fmt.Println("Number:", *number)
}
```

Run this script with:
```
go run script.go -verbose -input=example.txt -number=42
```

---

### Working with Flags in C++

In C++, you can parse flags manually or use libraries like Boost.Program_options.

```cpp
#include <iostream>
#include <getopt.h>

int main(int argc, char* argv[]) {
    int opt;
    std::string input;
    int number = 10;
    bool verbose = false;

    while ((opt = getopt(argc, argv, "vi:n:")) != -1) {
        switch (opt) {
            case 'v':
                verbose = true;
                break;
            case 'i':
                input = optarg;
                break;
            case 'n':
                number = std::stoi(optarg);
                break;
            default:
                std::cerr << "Usage: ./program [-v] [-i input] [-n number]\n";
                return 1;
        }
    }

    if (verbose) {
        std::cout << "Verbose mode enabled\n";
    }

    if (!input.empty()) {
        std::cout << "Input file: " << input << "\n";
    }

    std::cout << "Number: " << number << "\n";
    return 0;
}
```

Run this script with:
```
./program -v -i example.txt -n 42
```

---

### Using Command-Line Flags in Zig

Zig provides libraries like `std.os` to work with command-line arguments:

```zig
const std = @import("std");

pub fn main() !void {
    const args = try std.process.argsAlloc(std.heap.page_allocator);
    defer std.process.argsFree(std.heap.page_allocator, args);

    var verbose = false;
    var input: ?[]const u8 = null;
    var number = 10;

    for (args[1..]) |arg| {
        if (arg == "--verbose" or arg == "-v") {
            verbose = true;
        } else if (arg.startsWith("--input=")) {
            input = arg[8..];
        } else if (arg.startsWith("--number=")) {
            number = try std.fmt.parseInt(i32, arg[9..], 10);
        }
    }

    if (verbose) {
        std.debug.print("Verbose mode enabled\n", .{});
    }

    if (input) |file| {
        std.debug.print("Input file: {s}\n", .{file});
    }

    std.debug.print("Number: {}\n", .{number});
}
```

Run this script with:
```
zig build-exe program.zig && ./program -v --input=example.txt --number=42
```

---

## Best Practices for Using Command-Line Flags

1. **Provide Help Information**: Always include a `--help` flag to guide users.
2. **Use Meaningful Names**: Use descriptive long flags (e.g., `--output-file`) and concise short flags (e.g., `-o`).
3. **Set Default Values**: Make your program user-friendly by setting sensible defaults.
4. **Validate Input**: Ensure the input provided through flags is valid.
5. **Allow Combinations**: Let users combine short flags (e.g., `-abc`).

---

## Conclusion

Command-line flags are a powerful way to customize the behavior of your programs. By understanding their types, purposes, and implementation across languages, you can build flexible and user-friendly CLI applications. Whether you're using Python, PHP, Go, C++, or Zig, the concepts remain the same: define, parse, and use flags to improve your program's versatility.
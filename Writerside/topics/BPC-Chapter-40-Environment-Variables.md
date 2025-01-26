# Chapter 40 - Environment Variables

Environment variables are a critical part of many operating systems and programming environments. They allow software to behave differently based on specific configurations set outside the code itself. By understanding what environment variables are and how to use them effectively, you can unlock powerful ways to customize, secure, and control your applications.

## What Are Environment Variables?

Environment variables are key-value pairs stored in a system’s environment. They are accessible to programs running in that environment and provide information that can be used to influence the behavior of these programs. For example, an environment variable might store a file path, a server URL, or even sensitive information such as API keys.

### Different Types of Environment Variables

1. **System-Wide Variables**: These variables are available to all users and applications on a system. Examples include `PATH`, which lists directories where executable programs are located, and `HOME`, which indicates the current user’s home directory.

2. **User-Specific Variables**: These variables are specific to a particular user. For instance, `USER` on Linux or macOS and `USERNAME` on Windows are user-specific variables that store the name of the logged-in user.

3. **Session-Specific Variables**: These variables exist only for the duration of a session, such as a terminal session. They are often used to store temporary configurations or data.

4. **Custom Variables**: Developers or administrators can define their own variables to meet specific application requirements. For example, you could create `MY_APP_CONFIG` to store a custom configuration path.

---

## Why Use Environment Variables?

Environment variables play a crucial role in software development and system configuration. Some key benefits include:

- **Separation of Concerns**: Environment variables allow you to decouple configuration details from your code, making your applications more portable and easier to maintain.
- **Enhanced Security**: Sensitive information, such as database credentials or API tokens, can be stored as environment variables instead of hardcoding them into source files.
- **Flexible Configuration**: Environment variables make it easy to change the behavior of an application without modifying the code. For example, you can switch between development and production environments by setting a single variable.

---

## Common Environment Variables and Their Functions

### 1. `PATH`
The `PATH` variable specifies directories where executable programs are located. When you type a command in the terminal, the system searches these directories for the executable.

- **Example**: `/usr/local/bin:/usr/bin:/bin`
- **Use Case**: Running programs without specifying their full paths.

### 2. `HOME` or `USERPROFILE`
These variables indicate the current user’s home directory.

- **Linux/macOS**: `HOME=/home/username`
- **Windows**: `USERPROFILE=C:\Users\username`
- **Use Case**: Locating user-specific files or configurations.

### 3. `SHELL` or `COMSPEC`
The `SHELL` variable (on Unix-based systems) or `COMSPEC` (on Windows) specifies the default command-line shell.

- **Example**:
    - Linux/macOS: `/bin/bash`
    - Windows: `C:\Windows\System32\cmd.exe`
- **Use Case**: Determining the shell used for executing commands.

### 4. `TEMP` or `TMPDIR`
These variables indicate the directory where temporary files can be stored.

- **Linux/macOS**: `/tmp`
- **Windows**: `C:\Temp`
- **Use Case**: Temporary file handling in applications.

### 5. `LANG`
The `LANG` variable defines the language and locale settings.

- **Example**: `en_US.UTF-8`
- **Use Case**: Internationalization and localization of applications.

### 6. `EDITOR`
The `EDITOR` variable specifies the default text editor for command-line applications.

- **Example**: `vim`, `nano`, or `notepad`
- **Use Case**: Automatically launching the preferred editor for editing tasks.

---

## How to Set and Access Environment Variables

### Setting Environment Variables

#### Linux and macOS
You can set environment variables in the terminal or in configuration files like `.bashrc`, `.zshrc`, or `/etc/environment`.

```bash
# Temporary
export MY_VARIABLE="Hello, World!"

# Permanent (add to .bashrc or .zshrc)
echo 'export MY_VARIABLE="Hello, World!"' >> ~/.bashrc
source ~/.bashrc
```

#### Windows
You can set environment variables temporarily in Command Prompt or permanently through the System Properties.

```shell
:: Temporary
set MY_VARIABLE=Hello, World!

:: Permanent (through System Properties or PowerShell)
[System.Environment]::SetEnvironmentVariable("MY_VARIABLE", "Hello, World!", "User")
```

### Accessing Environment Variables

#### Python
```python
import os

# Access an environment variable
my_variable = os.getenv('MY_VARIABLE')
print(my_variable)
```

#### PHP
```php
<?php
// Access an environment variable
$my_variable = getenv('MY_VARIABLE');
echo $my_variable;
?>
```

#### Go
```go
package main

import (
	"fmt"
	"os"
)

func main() {
	myVariable := os.Getenv("MY_VARIABLE")
	fmt.Println(myVariable)
}
```

#### C++
```cpp
#include <iostream>
#include <cstdlib>

int main() {
    const char* myVariable = std::getenv("MY_VARIABLE");
    if (myVariable) {
        std::cout << myVariable << std::endl;
    } else {
        std::cout << "Variable not found" << std::endl;
    }
    return 0;
}
```

#### Zig
```zig
const std = @import("std");

pub fn main() void {
    const env = std.os.getenv("MY_VARIABLE");
    if (env) |value| {
        std.debug.print("{s}\n", .{value});
    } else {
        std.debug.print("Variable not found\n", .{});
    }
}
```

---

## Best Practices for Using Environment Variables

1. **Avoid Hardcoding**: Never hardcode sensitive information, such as passwords or keys, into your application code.
2. **Use `.env` Files**: Store environment variables in a `.env` file and load them programmatically.
3. **Limit Scope**: Use session- or user-specific variables when appropriate, instead of system-wide variables.
4. **Secure Access**: Restrict access to environment variables containing sensitive information.
5. **Document Variables**: Keep a list of required environment variables and their purposes for each project.

---

## Conclusion

Environment variables are a powerful tool for configuring and managing software. By understanding their purpose, types, and how to use them, you can enhance the flexibility, security, and maintainability of your applications. Whether you're a system administrator or a developer, mastering environment variables is an essential skill for modern computing.
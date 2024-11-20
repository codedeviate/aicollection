# Hello, World

Here is a simple "Hello World" program in C:

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

### Steps to Compile and Build

1. **Save the code**: Save the above code in a file named `hello.c`.

2. **Open a terminal**: Navigate to the directory where `hello.c` is saved.

3. **Compile the code**: Use the `gcc` compiler to compile the code. Run the following command:
   ```sh
   gcc -o hello hello.c
   ```

4. **Run the executable**: After compilation, an executable file named `hello` (or `hello.exe` on Windows) will be created. Run it using:
   ```sh
   ./hello
   ```

This will output:
```
Hello, World!
```
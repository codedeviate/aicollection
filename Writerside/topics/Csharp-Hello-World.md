# Hello, World

Here is a simple "Hello World" program in C#:

```c#
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

## Steps to Compile and Build

1. **Save the code**: Save the above code in a file named `Program.cs`.

2. **Open a terminal**: Navigate to the directory where `Program.cs` is saved.

3. **Compile the code**: Use the `csc` (C# compiler) to compile the code. Run the following command:
   ```sh
   csc Program.cs
   ```

4. **Run the executable**: After compilation, an executable file named `Program.exe` will be created. Run it using:
   ```sh
   Program.exe
   ```

This will output:
```
Hello, World!
```
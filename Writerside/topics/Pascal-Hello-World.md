# Hello, World

Here is a simple "Hello World" program in Pascal:

```pascal
program HelloWorld;
begin
  WriteLn('Hello, World!');
end.
```

## Steps to Run

1. **Save the code**: Save the above code in a file named `hello.pas`.

2. **Open a terminal**: Navigate to the directory where `hello.pas` is saved.

3. **Compile the program**: Use the Pascal compiler (e.g., Free Pascal or Turbo Pascal) to compile the program. Run the following command:
   ```sh
   fpc hello.pas
   ```

4. **Run the program**: After compilation, execute the generated binary file (e.g., `hello` or `hello.exe` depending on your platform). Run the following command:
   ```sh
   ./hello
   ```

This will output:
```
Hello, World!
```
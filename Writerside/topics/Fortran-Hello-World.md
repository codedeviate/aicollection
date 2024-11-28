# Hello, World

## Hello World Example in Fortran

Here is a simple "Hello, World!" program written in Fortran:

```fortran
program hello
    print *, 'Hello, World!'
end program hello
```

## Instructions to Run the Fortran Program

1. **Save the Code**: Save the above code in a file named `hello.f90`.

2. **Compile the Program**: Use a Fortran compiler to compile the program. If you have `gfortran` installed, you can compile the program using the following command in the terminal:

   ```sh
   gfortran -o hello hello.f90
   ```

   This command compiles `hello.f90` and creates an executable named `hello`.

3. **Run the Program**: Execute the compiled program by running the following command in the terminal:

   ```sh
   ./hello
   ```

   You should see the output:

   ```
   Hello, World!
   ```

## Summary

1. Save the code in `hello.f90`.
2. Compile with `gfortran -o hello hello.f90`.
3. Run with `./hello`.
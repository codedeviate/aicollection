# Hello, World!

To compile and build a C++ program, follow these steps:

1. **Install a C++ Compiler**: Ensure you have a C++ compiler installed, such as `g++` (part of GCC) or `clang++`.

2. **Write Your C++ Code**: Create a file named `main.cpp` with your C++ code. For example:
    ```cpp
    #include <iostream>

    int main() {
        std::cout << "Hello, World!" << std::endl;
        return 0;
    }
    ```

3. **Open Terminal**: Navigate to the directory containing your `main.cpp` file.

4. **Compile the C++ Code**: Use the `g++` or `clang++` command to compile your C++ code into an executable.
    ```sh
    g++ main.cpp -o main
    ```

5. **Run the Executable**: After compilation, run the generated executable.
    ```sh
    ./main
    ```

These steps will compile and build your C++ program, allowing you to run the resulting executable.
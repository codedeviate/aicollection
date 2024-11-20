# Hello, World!

To compile and build a Zig program, follow these steps:

1. **Install Zig**: Download and install Zig from the [official website](https://ziglang.org/download/).

2. **Write Your Zig Code**: Create a file named `main.zig` with your Zig code. For example:
    ```zig
    const std = @import("std");

    pub fn main() void {
        std.debug.print("Hello, World!\n", .{});
    }
    ```

3. **Open Terminal**: Navigate to the directory containing your `main.zig` file.

4. **Compile the Zig Code**: Use the `zig build-exe` command to compile your Zig code into an executable.
    ```sh
    zig build-exe main.zig
    ```

5. **Run the Executable**: After compilation, run the generated executable.
    ```sh
    ./main
    ```

These steps will compile and build your Zig program, allowing you to run the resulting executable.
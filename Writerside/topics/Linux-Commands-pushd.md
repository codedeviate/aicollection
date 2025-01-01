# pushd

In Linux, `pushd` is a command used to manage the directory stack, which is a stack of directories that allows users to quickly navigate back and forth between directories. It works in conjunction with the `popd` command, which pops the top directory off the stack, and `dirs`, which shows the contents of the stack. The `pushd` command adds the current directory to the stack and then changes to a new directory, making it useful for temporary changes in the directory that you can easily return from.

## Key Points:
1. **Directory Stack**: The directory stack is a list of directories stored in memory, enabling users to go back to a previous directory using the `popd` command.
2. **pushd Syntax**:
   ```bash
   pushd <directory>
   ```
    - If no argument is given, `pushd` swaps the current directory with the top of the stack (it essentially returns you to the previous directory).
    - If a directory is specified, it is pushed onto the stack, and the working directory changes to the specified directory.

## Example 1: Basic usage of `pushd`
Let’s say you are in a directory `/home/user` and you want to navigate to `/tmp` and then easily come back to `/home/user`.

1. **Current directory**:
   ```bash
   $ pwd
   /home/user
   ```

2. **Use `pushd` to change to `/tmp`**:
   ```bash
   $ pushd /tmp
   /tmp ~ /home/user
   ```

   After running `pushd`, the output shows that `/home/user` is added to the stack, and the current directory is changed to `/tmp`.

3. **Check the directory stack**:
   ```bash
   $ dirs
   /tmp ~ /home/user
   ```

   The `dirs` command shows that `/tmp` is the top of the stack, and `/home/user` is the second entry.

4. **Return to the previous directory**:
   ```bash
   $ popd
   /home/user
   ```

   The `popd` command pops the top directory off the stack (which was `/tmp`), returning you to the previous directory, which is `/home/user`.

## Example 2: Using `pushd` with no argument
When you run `pushd` with no arguments, it swaps the current directory with the top directory on the stack.

1. **Current directory**:
   ```bash
   $ pwd
   /home/user
   ```

2. **Use `pushd` to change to `/tmp`**:
   ```bash
   $ pushd /tmp
   /tmp ~ /home/user
   ```

3. **Now, use `pushd` with no argument**:
   ```bash
   $ pushd
   /home/user ~ /tmp
   ```

   The `pushd` command swapped the current directory `/tmp` with `/home/user`, putting `/home/user` back at the top of the stack.

## Example 3: Using `pushd` with a relative directory
You can also use `pushd` with relative paths. Let's assume you're in `/home/user` and want to go to `/home/user/projects`, a subdirectory.

1. **Current directory**:
   ```bash
   $ pwd
   /home/user
   ```

2. **Use `pushd` with a relative directory**:
   ```bash
   $ pushd projects
   /home/user/projects ~ /home/user
   ```

   Here, `projects` is a subdirectory of `/home/user`, and `pushd` took you to `/home/user/projects` while adding `/home/user` to the stack.

## Summary
- `pushd` changes your working directory and adds the previous one to a stack.
- The stack allows easy navigation back to previous directories with `popd`.
- You can check the contents of the stack with the `dirs` command.
- Running `pushd` without an argument swaps your current directory with the top directory in the stack.

This is very useful for complex navigation scenarios, especially when you need to work in multiple directories but want to easily return to where you started.
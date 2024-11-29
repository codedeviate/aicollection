# mv

`git mv` is a command used to move or rename files and directories in a Git repository. It is a convenient way to perform these operations because it stages the changes for you, so you don't need to run `git add` after moving or renaming the files.

## Basic Usage

1. **Move a File**

   To move a file from one location to another, use the following command:

   ```sh
   git mv old_file_path new_file_path
   ```

   This will move the file from `old_file_path` to `new_file_path` and stage the change.

2. **Rename a File**

   To rename a file, use the same command with the new file name:

   ```sh
   git mv old_file_name new_file_name
   ```

   This will rename the file from `old_file_name` to `new_file_name` and stage the change.

3. **Move a Directory**

   To move a directory and all its contents, use the following command:

   ```sh
   git mv old_directory_path new_directory_path
   ```

   This will move the directory from `old_directory_path` to `new_directory_path` and stage the change.

## Examples

1. **Move a File**

   ```sh
   git mv src/old_file.txt src/new_file.txt
   ```

   This command moves `old_file.txt` from the `src` directory to `new_file.txt` in the same directory.

2. **Rename a File**

   ```sh
   git mv README.md README.txt
   ```

   This command renames `README.md` to `README.txt`.

3. **Move a Directory**

   ```sh
   git mv docs/old_directory docs/new_directory
   ```

   This command moves the `old_directory` from the `docs` directory to `new_directory` in the same directory.

Using `git mv` ensures that the changes are tracked correctly by Git and staged for the next commit.
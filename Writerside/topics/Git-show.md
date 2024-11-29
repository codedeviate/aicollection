# show

`git show` is a command used to display various types of objects in a Git repository. It is commonly used to show the details of a specific commit, including the commit message, author, date, and the changes made.

## Basic Usage

1. **Show a Specific Commit**

   To display the details of a specific commit, use the commit hash:

   ```sh
   git show <commit_hash>
   ```

   This will show the commit message, author, date, and the changes made in the specified commit.

2. **Show the Last Commit**

   To display the details of the most recent commit, use:

   ```sh
   git show
   ```

   This will show the details of the last commit.

3. **Show a Specific File in a Commit**

   To display the changes made to a specific file in a commit, use:

   ```sh
   git show <commit_hash>:<file_path>
   ```

   This will show the changes made to the specified file in the given commit.

## Examples

1. **Show a Specific Commit**

   ```sh
   git show abc123
   ```

   This command displays the details of the commit with hash `abc123`.

2. **Show the Last Commit**

   ```sh
   git show
   ```

   This command displays the details of the most recent commit.

3. **Show Changes to a Specific File in a Commit**

   ```sh
   git show abc123:src/main.c
   ```

   This command displays the changes made to `src/main.c` in the commit with hash `abc123`.

Using `git show` helps you inspect the details of commits and the changes made to files in your Git repository.
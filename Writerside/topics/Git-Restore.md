# restore

`git restore` is a command used to restore working tree files. It can be used to discard changes in the working directory or to restore files from another commit. It is a more focused alternative to `git checkout` for restoring files.

## Basic Usage

1. **Restore a File to the Last Committed State**

   To discard changes in a file and restore it to the last committed state, use:

   ```sh
   git restore file.txt
   ```

   This will discard any changes in `file.txt` and restore it to the state of the last commit.

2. **Restore Multiple Files**

   To restore multiple files, list them all:

   ```sh
   git restore file1.txt file2.txt
   ```

   This will discard changes in both `file1.txt` and `file2.txt`.

3. **Restore All Files in the Working Directory**

   To discard changes in all files in the working directory, use:

   ```sh
   git restore .
   ```

   This will discard changes in all files and restore them to the state of the last commit.

4. **Restore a File from a Specific Commit**

   To restore a file from a specific commit, use the `--source` option followed by the commit hash:

   ```sh
   git restore --source=<commit_hash> file.txt
   ```

   This will restore `file.txt` to the state it was in at the specified commit.

5. **Unstage a File**

   To unstage a file that has been added to the staging area, use the `--staged` option:

   ```sh
   git restore --staged file.txt
   ```

   This will unstage `file.txt` but keep the changes in the working directory.

## Examples

1. **Discard Changes in a File**

   ```sh
   git restore src/main.c
   ```

   This command discards changes in `src/main.c` and restores it to the last committed state.

2. **Discard Changes in All Files**

   ```sh
   git restore .
   ```

   This command discards changes in all files in the working directory.

3. **Restore a File from a Specific Commit**

   ```sh
   git restore --source=abc123 src/main.c
   ```

   This command restores `src/main.c` to the state it was in at commit `abc123`.

4. **Unstage a File**

   ```sh
   git restore --staged src/main.c
   ```

   This command unstages `src/main.c` but keeps the changes in the working directory.

Using `git restore` helps manage changes in the working directory and staging area efficiently.
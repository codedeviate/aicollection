# reset

`git reset` is a command used to undo changes in a Git repository. It can modify the index (staging area), the working directory, and the commit history. There are three main modes of `git reset`: `--soft`, `--mixed`, and `--hard`.

## Basic Usage

1. **Reset the Last Commit (`--soft`)**

   This mode moves the HEAD to the specified commit and leaves the index and working directory unchanged. The changes from the reset commit are staged for commit.

   ```sh
   git reset --soft HEAD~1
   ```

   This command resets the last commit but keeps the changes in the staging area.

2. **Reset the Last Commit (`--mixed`)**

   This is the default mode. It moves the HEAD to the specified commit and updates the index to match, but leaves the working directory unchanged. The changes from the reset commit are unstaged.

   ```sh
   git reset --mixed HEAD~1
   ```

   This command resets the last commit and unstages the changes, but keeps them in the working directory.

3. **Reset the Last Commit (`--hard`)**

   This mode moves the HEAD to the specified commit and updates both the index and working directory to match. All changes are discarded.

   ```sh
   git reset --hard HEAD~1
   ```

   This command resets the last commit and discards all changes in the working directory and index.

## Examples

1. **Undo the Last Commit but Keep Changes Staged**

   ```sh
   git reset --soft HEAD~1
   ```

   This command undoes the last commit but keeps the changes in the staging area.

2. **Unstage Changes from the Last Commit**

   ```sh
   git reset --mixed HEAD~1
   ```

   This command undoes the last commit and unstages the changes, but keeps them in the working directory.

3. **Discard All Changes from the Last Commit**

   ```sh
   git reset --hard HEAD~1
   ```

   This command undoes the last commit and discards all changes in the working directory and index.

4. **Reset to a Specific Commit**

   ```sh
   git reset --hard <commit_hash>
   ```

   This command resets the repository to the specified commit and discards all changes in the working directory and index.

Using `git reset` allows you to undo changes at different levels, providing flexibility in managing your commit history and working directory.
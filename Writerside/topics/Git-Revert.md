# revert

`git revert` is a command used to create a new commit that undoes the changes made by a previous commit. Unlike `git reset`, which can alter the commit history, `git revert` is a safe way to undo changes because it preserves the history.

## Basic Usage

1. **Revert a Single Commit**

   To revert a single commit, use the following command:

   ```sh
   git revert <commit_hash>
   ```

   This will create a new commit that undoes the changes made by the specified commit.

2. **Revert Multiple Commits**

   To revert a range of commits, use the following command:

   ```sh
   git revert <oldest_commit_hash>..<newest_commit_hash>
   ```

   This will create new commits that undo the changes made by the specified range of commits.

3. **Revert a Commit with a Message**

   To revert a commit and provide a custom commit message, use the `-m` option:

   ```sh
   git revert -m "Reverting commit <commit_hash>" <commit_hash>
   ```

## Examples

1. **Revert a Single Commit**

   ```sh
   git revert abc123
   ```

   This command creates a new commit that undoes the changes made by commit `abc123`.

2. **Revert Multiple Commits**

   ```sh
   git revert abc123..def456
   ```

   This command creates new commits that undo the changes made by the commits in the range from `abc123` to `def456`.

3. **Revert a Commit with a Custom Message**

   ```sh
   git revert -m "Reverting commit abc123" abc123
   ```

   This command creates a new commit that undoes the changes made by commit `abc123` and includes the custom message "Reverting commit abc123".

Using `git revert` allows you to safely undo changes while preserving the commit history.
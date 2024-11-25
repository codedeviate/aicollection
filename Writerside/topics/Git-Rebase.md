# Rebase

The `git rebase` command is used to reapply commits on top of another base tip. It is a powerful tool for streamlining a series of commits, making the commit history more linear and easier to understand.

### Detailed Explanation

1. **Basic Usage**: `git rebase` moves or combines a sequence of commits to a new base commit. This is often used to keep a feature branch up to date with the latest changes from the main branch.

2. **Interactive Rebase**: Using the `-i` option, you can interactively rebase, allowing you to edit, reorder, squash, or drop commits.

3. **Rebasing vs. Merging**: Unlike `git merge`, which creates a merge commit, `git rebase` rewrites the commit history, making it appear as if the changes were made sequentially.

4. **Conflict Resolution**: During a rebase, conflicts may arise. You need to resolve these conflicts manually and then continue the rebase process.

5. **Preserving Merge Commits**: The `--preserve-merges` option can be used to keep merge commits during a rebase.

### Examples

1. **Rebasing a Feature Branch onto Master**:
   ```sh
   git checkout feature-branch
   git rebase master
   ```
   This command moves the commits from `feature-branch` to be based on the latest commit in `master`.

2. **Interactive Rebase to Squash Commits**:
   ```sh
   git checkout feature-branch
   git rebase -i HEAD~3
   ```
   This command starts an interactive rebase for the last three commits on `feature-branch`, allowing you to squash, edit, or reorder commits.
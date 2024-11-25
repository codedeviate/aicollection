# Reflog

The `git reflog` command is used to manage the reference logs in Git. Reflogs record when the tips of branches and other references were updated in the local repository. This is useful for recovering lost commits and understanding the history of changes.

### Detailed Explanation

1. **Viewing Reflog**: The `git reflog` command shows a log of all the changes made to the tips of branches and other references. Each entry includes the commit hash, the action taken, and a timestamp.

2. **Recovering Lost Commits**: If you accidentally delete a branch or reset to a previous commit, you can use the reflog to find the commit hash and recover your changes.

3. **Cleaning Up Reflog**: Over time, the reflog can grow large. You can clean up old entries using the `git reflog expire` command.

4. **Pruning Reflog**: You can prune unreachable reflog entries using the `git reflog delete` command.

### Examples

1. **Viewing the Reflog**:
   ```sh
   git reflog
   ```
   This command displays the reflog for the current branch, showing all changes made to the branch tip.

2. **Recovering a Lost Commit**:
   ```sh
   git reflog
   git checkout <commit-hash>
   ```
   First, view the reflog to find the commit hash of the lost commit. Then, use `git checkout` to recover the commit.

3. **Cleaning Up Old Reflog Entries**:
   ```sh
   git reflog expire --expire=90.days.ago --all
   ```
   This command cleans up reflog entries older than 90 days for all references.

4. **Pruning Unreachable Reflog Entries**:
   ```sh
   git reflog delete --rewrite <commit-hash>
   ```
   This command deletes the specified reflog entry and rewrites the reflog to remove unreachable entries.
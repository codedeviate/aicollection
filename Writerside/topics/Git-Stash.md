# stash

The `git stash` command is used to temporarily save changes in your working directory that you are not ready to commit. This allows you to switch branches or perform other tasks without losing your current work. The stashed changes can be reapplied later.

## Detailed Explanation

1. **Stashing Changes**: When you run `git stash`, Git saves the changes in your working directory and index (staging area) to a new stash entry and reverts your working directory to match the HEAD commit.

2. **Stash List**: You can view the list of stashed changes using `git stash list`. Each stash entry is identified by a name like `stash@{0}`, `stash@{1}`, etc.

3. **Applying Stashed Changes**: You can reapply stashed changes using `git stash apply` or `git stash pop`. The `apply` command reapplies the changes without removing the stash entry, while `pop` reapplies the changes and removes the stash entry.

4. **Dropping Stashes**: You can remove a specific stash entry using `git stash drop` or clear all stashes using `git stash clear`.

## Examples

1. **Stashing Changes**:
   ```sh
   git stash
   ```
   This command stashes the current changes in your working directory and index.

2. **Applying the Most Recent Stash**:
   ```sh
   git stash apply
   ```
   This command reapplies the most recent stash entry without removing it from the stash list.
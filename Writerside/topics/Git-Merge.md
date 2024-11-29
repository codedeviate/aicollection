# merge

The `git merge` command is used to combine the changes from one branch into another. It is a key part of the Git workflow, allowing you to integrate changes from different branches.

## Detailed Explanation

1. **Fast-Forward Merge**: If the branch you are merging has not diverged from the branch you are merging into, Git will perform a fast-forward merge. This simply moves the pointer of the current branch forward to the latest commit of the branch being merged.

2. **Three-Way Merge**: If the branches have diverged, Git will perform a three-way merge. This involves creating a new commit that combines the changes from both branches. Git uses the common ancestor of the two branches to perform the merge.

3. **Merge Conflicts**: Sometimes, changes in the branches being merged conflict with each other. In such cases, Git will mark the conflicts in the affected files and pause the merge process. You will need to resolve the conflicts manually and then complete the merge.

4. **Merge Commit**: A merge commit is a special commit that has two parent commits. It represents the result of merging two branches.

## Examples

1. **Merging a Branch into the Current Branch**:
   ```sh
   git checkout master
   git merge feature-branch
   ```
   This command switches to the `master` branch and merges the `feature-branch` into it.

2. **Merging with a Commit Message**:
   ```sh
   git checkout master
   git merge feature-branch -m "Merge feature-branch into master"
   ```
   This command switches to the `master` branch, merges the `feature-branch` into it, and adds a custom merge commit message.
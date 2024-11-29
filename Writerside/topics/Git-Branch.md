# branch

The `git branch` command is used to manage branches in a Git repository. Branches are an essential part of Git, allowing you to work on different features or bug fixes independently of the main codebase.

## Detailed Explanation

1. **Creating Branches**: A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is `master` (or `main` in newer repositories). When you create a new branch, you are creating a new pointer to the current commit.

2. **Switching Branches**: You can switch to an existing branch using the `git checkout` or `git switch` command. This updates the working directory to match the state of the branch you are switching to.

3. **Listing Branches**: You can list all branches in your repository using `git branch`. This will show you all local branches and indicate the current branch with an asterisk.

4. **Deleting Branches**: Once a branch is no longer needed, you can delete it using `git branch -d` for a safe delete (only if the branch has been merged) or `git branch -D` for a force delete.

## Examples

1. **Creating a New Branch**:
   ```sh
   git branch new-feature
   ```
   This command creates a new branch named `new-feature`.

2. **Switching to a Branch**:
   ```sh
   git checkout new-feature
   ```
   This command switches to the `new-feature` branch.

3. **Listing All Branches**:
   ```sh
   git branch
   ```
   This command lists all branches in the repository, with the current branch indicated by an asterisk.

4. **Deleting a Branch**:
   ```sh
   git branch -d new-feature
   ```
   This command deletes the `new-feature` branch if it has been merged. Use `-D` to force delete if it hasn't been merged.
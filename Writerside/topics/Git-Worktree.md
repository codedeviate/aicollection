# Worktree

The `git worktree` command allows you to manage multiple working directories attached to a single Git repository. This is useful for working on different branches simultaneously without having to switch between them in a single directory.

### Detailed Explanation

1. **Creating a Worktree**: You can create a new worktree linked to a specific branch or commit. This creates a new directory where you can work on that branch or commit independently of the main working directory.

2. **Listing Worktrees**: You can list all existing worktrees associated with the repository.

3. **Removing a Worktree**: You can remove a worktree when it is no longer needed.

4. **Pruning Worktrees**: You can prune worktrees to remove references to directories that no longer exist.

### Examples

1. **Creating a New Worktree for a Branch**:
   ```sh
   git worktree add ../new-worktree-branch feature-branch
   ```
   This command creates a new worktree in the `../new-worktree-branch` directory and checks out the `feature-branch` in that directory.

2. **Creating a New Worktree for a Specific Commit**:
   ```sh
   git worktree add ../new-worktree-commit <commit-hash>
   ```
   This command creates a new worktree in the `../new-worktree-commit` directory and checks out the specified commit.

3. **Listing All Worktrees**:
   ```sh
   git worktree list
   ```
   This command lists all worktrees associated with the repository, showing their paths and the branches or commits they are checked out to.

4. **Removing a Worktree**:
   ```sh
   git worktree remove ../new-worktree-branch
   ```
   This command removes the worktree located at `../new-worktree-branch`. Note that you need to manually delete the directory if it still exists.

These commands help you manage multiple working directories efficiently, allowing you to work on different branches or commits simultaneously.
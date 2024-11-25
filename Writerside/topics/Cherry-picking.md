# Cherry picking

Cherry-picking in Git refers to the process of selecting specific commits from one branch and applying them to another. This is useful when you want to incorporate particular changes without merging entire branches.

### Example

1. **Identify the Commit to Cherry-Pick:**
   First, find the commit hash you want to cherry-pick. You can use `git log` to list commits.

   ```sh
   git log
   ```

2. **Cherry-Pick the Commit:**
   Use the `git cherry-pick` command followed by the commit hash.

   ```sh
   git cherry-pick <commit-hash>
   ```

   For example, if the commit hash is `a1b2c3d4`, you would run:

   ```sh
   git cherry-pick a1b2c3d4
   ```

3. **Resolve Conflicts (if any):**
   If there are conflicts, Git will pause the cherry-pick process and allow you to resolve them. After resolving conflicts, you can continue the process with:

   ```sh
   git add <resolved-files>
   git cherry-pick --continue
   ```

4. **Abort Cherry-Pick:**
   If you decide to abort the cherry-pick process, you can use:

   ```sh
   git cherry-pick --abort
   ```

### Example Scenario

Suppose you have two branches: `feature` and `master`. You want to apply a specific commit from `feature` to `master`.

1. **Switch to the `master` branch:**

   ```sh
   git checkout master
   ```

2. **Cherry-pick the commit from `feature`:**

   ```sh
   git cherry-pick a1b2c3d4
   ```

This will apply the changes from the specified commit in the `feature` branch to the `master` branch.
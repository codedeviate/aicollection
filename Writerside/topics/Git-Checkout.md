# checkout

The `git checkout` command is used to switch between branches or restore working tree files in a Git repository. It is a versatile command that can be used for various purposes, such as switching branches, checking out specific commits, or discarding changes in the working directory.

## Detailed Explanation

1. **Switching Branches**: The most common use of `git checkout` is to switch between branches. When you switch branches, Git updates the files in your working directory to match the state of the branch you are switching to.

2. **Creating and Switching to a New Branch**: You can create a new branch and switch to it in a single command using the `-b` option.

3. **Checking Out Specific Commits**: You can use `git checkout` to check out a specific commit by its hash. This puts your repository in a "detached HEAD" state, meaning you are not on any branch.

4. **Restoring Files**: You can use `git checkout` to restore specific files to their state in a particular commit or branch.

## Examples

1. **Switching to an Existing Branch**:
   ```sh
   git checkout master
   ```
   This command switches to the `master` branch.

2. **Creating and Switching to a New Branch**:
   ```sh
   git checkout -b new-feature
   ```
   This command creates a new branch named `new-feature` and switches to it.
# Commit

The `git commit` command is used to save changes to the local repository. It captures a snapshot of the project's currently staged changes. This command is a crucial part of the Git workflow, as it allows you to record the history of your project.

### Detailed Explanation

1. **Creating a Commit**: When you run `git commit`, Git takes the changes that have been added to the staging area and stores them in a new commit. Each commit has a unique identifier (SHA-1 hash) and contains metadata such as the author, date, and commit message.

2. **Commit Message**: A commit message is a brief description of the changes made. It helps to understand the purpose of the commit. You can provide a commit message using the `-m` option.

3. **Amending a Commit**: If you need to modify the most recent commit, you can use the `--amend` option. This is useful for correcting mistakes or adding forgotten changes.

4. **Commit All Changes**: You can use the `-a` option to automatically stage all modified and deleted files before committing, but it does not include new untracked files.

### Examples

1. **Committing Staged Changes with a Message**:
   ```sh
   git commit -m "Add new feature"
   ```
   This command commits the staged changes with the message "Add new feature".

2. **Amending the Most Recent Commit**:
   ```sh
   git commit --amend -m "Update feature implementation"
   ```
   This command amends the most recent commit with a new message "Update feature implementation".

3. **Committing All Changes**:
   ```sh
   git commit -a -m "Fix bugs and update documentation"
   ```
   This command stages all modified and deleted files and commits them with the message "Fix bugs and update documentation".
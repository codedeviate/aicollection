# Daily Git Commands

These commands cover most use cases in Git.

---

## 1. Getting Started
- `git init` – Initialize a new Git repository.
- `git clone <url>` – Clone a repository into a new directory.

---

## 2. Configuration
- `git config` – Configure user details, preferences, etc.
    - `git config --global user.name "<name>"` – Set user name.
    - `git config --global user.email "<email>"` – Set user email.
    - `git config --list` – List all Git configurations.

---

## 3. Basic Snapshotting
### Staging and Commit
- `git add <file>` – Add file to the staging area.
- `git add .` – Add all changes to the staging area.
- `git commit -m "<message>"` – Commit changes with a message.
- `git commit --amend` – Edit the last commit.

### Viewing Changes
- `git status` – Check the status of files in the working directory.
- `git diff` – Show changes in unstaged files.
- `git diff --staged` – Show changes in staged files.

---

## 4. Branching and Merging
### Branch Management
- `git branch` – List branches.
- `git branch <name>` – Create a new branch.
- `git branch -d <name>` – Delete a branch.
- `git branch -D <name>` – Force-delete a branch.

### Switching Branches
- `git switch <branch>` – Switch to another branch.
- `git checkout <branch>` – Legacy command to switch branches.

### Merging
- `git merge <branch>` – Merge a branch into the current branch.

### Rebasing
- `git rebase <branch>` – Reapply commits on top of another base branch.

---

## 5. Remote Repositories
- `git remote add <name> <url>` – Add a remote repository.
- `git remote -v` – List remote repositories.
- `git fetch <remote>` – Download objects and refs from a remote.
- `git pull` – Fetch and integrate changes from a remote repository.
- `git push` – Push changes to a remote repository.
- `git push -u <remote> <branch>` – Push and set upstream tracking.

---

## 6. Inspection and Comparison
- `git log` – Show commit history.
- `git log --oneline` – Display a concise log view.
- `git show <commit>` – Show details about a specific commit.
- `git blame <file>` – Show who made changes to each line of a file.
- `git diff <commit1> <commit2>` – Compare two commits.

---

## 7. Undoing Changes
- `git restore <file>` – Discard changes in the working directory.
- `git restore --staged <file>` – Unstage a file.
- `git reset <commit>` – Reset current HEAD to a specified commit.
- `git reset --hard <commit>` – Reset and delete all changes.

---

## 8. Stashing
- `git stash` – Save changes for later.
- `git stash list` – List all stashes.
- `git stash pop` – Apply and remove the most recent stash.
- `git stash drop` – Remove a specific stash.

---

## 9. Tagging
- `git tag` – List tags.
- `git tag <name>` – Create a new tag.
- `git tag -d <name>` – Delete a tag.
- `git push <remote> <tag>` – Push a tag to a remote repository.

---

## 10. Collaboration
- `git cherry-pick <commit>` – Apply a specific commit to the current branch.
- `git rebase --onto` – Apply commits elsewhere.
- `git pull --rebase` – Fetch and reapply local changes after fetching.

---

## 11. Debugging
- `git bisect` – Perform binary search to find a buggy commit.
- `git fsck` – Check the repository for errors.

---

## 12. Advanced
- `git reflog` – Show a log of all references.
- `git filter-branch` – Rewrite history (deprecated, use filters or `git replace`).
- `git cherry` – Show commits that are not yet merged.

---

## 13. Archive and Export
- `git archive` – Create a tarball of the repository.

---

## 14. Help
- `git help <command>` – Display help for a specific Git command.
- `git --version` – Display the current Git version.

---

This list covers most commands you’ll need in day-to-day Git usage.
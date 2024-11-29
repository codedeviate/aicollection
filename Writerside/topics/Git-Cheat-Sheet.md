# Git Cheat Sheet

Here is an extensive cheat sheet for using Git:

## Basic Commands

### Initializing a Repository
```sh
git init
```
Initialize a new Git repository.

### Cloning a Repository
```sh
git clone <repository_url>
```
Clone an existing repository.

### Checking the Status
```sh
git status
```
Show the working directory status.

### Adding Changes
```sh
git add <file>
git add .
```
Add a file or all changes to the staging area.

### Committing Changes
```sh
git commit -m "Commit message"
```
Commit staged changes with a message.

### Viewing the Commit History
```sh
git log
```
Show the commit history.

## Branching and Merging

### Creating a New Branch
```sh
git branch <branch_name>
```
Create a new branch.

### Switching Branches
```sh
git checkout <branch_name>
```
Switch to a different branch.

### Merging Branches
```sh
git merge <branch_name>
```
Merge a branch into the current branch.

### Deleting a Branch
```sh
git branch -d <branch_name>
```
Delete a branch.

## Remote Repositories

### Adding a Remote
```sh
git remote add <name> <url>
```
Add a new remote repository.

### Fetching Changes
```sh
git fetch <remote>
```
Fetch changes from a remote repository.

### Pulling Changes
```sh
git pull <remote> <branch>
```
Fetch and merge changes from a remote branch.

### Pushing Changes
```sh
git push <remote> <branch>
```
Push changes to a remote branch.

## Undoing Changes

### Resetting Changes
```sh
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```
Reset changes at different levels.

### Restoring Files
```sh
git restore <file>
git restore --staged <file>
```
Restore files to the last committed state or unstage them.

### Reverting Commits
```sh
git revert <commit_hash>
```
Create a new commit that undoes a previous commit.

## Stashing

### Stashing Changes
```sh
git stash
```
Stash changes in the working directory.

### Applying Stashed Changes
```sh
git stash apply
```
Apply stashed changes.

### Listing Stashes
```sh
git stash list
```
List all stashes.

## Submodules

### Adding a Submodule
```sh
git submodule add <repository_url> <path>
```
Add a new submodule.

### Updating Submodules
```sh
git submodule update --init --recursive
```
Initialize and update submodules.

### Running Commands in Submodules
```sh
git submodule foreach <command>
```
Run a command in each submodule.

## Tags

### Creating a Tag
```sh
git tag -a <tag_name> -m "Tag message"
```
Create an annotated tag.

### Listing Tags
```sh
git tag
```
List all tags.

### Pushing Tags
```sh
git push <remote> <tag_name>
```
Push a tag to a remote repository.

## Worktrees

### Creating a Worktree
```sh
git worktree add <path> <branch>
```
Create a new worktree for a branch.

### Listing Worktrees
```sh
git worktree list
```
List all worktrees.

### Removing a Worktree
```sh
git worktree remove <path>
```
Remove a worktree.

## Advanced Index Manipulation

### Adding to the Index
```sh
git update-index --add <file>
```
Add a file to the index.

### Marking as Assumed Unchanged
```sh
git update-index --assume-unchanged <file>
```
Mark a file as "assume unchanged".

This cheat sheet covers a wide range of Git commands and their usage.
It can serve as a quick reference guide for beginners and experienced users alike.

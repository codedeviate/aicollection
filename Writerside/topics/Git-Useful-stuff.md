# Useful stuff

In this section, we will cover some useful commands and operations in Git, a popular version control system used for tracking changes in code repositories. Git provides a powerful set of tools for managing code, collaborating with others, and tracking the history of your projects.

## Viewing Commit History
To view the commit history of a repository, use:
```sh
git log
```
This command shows a list of commits with details like commit hash, author, date, and commit message.

## Checking the Status
To check the status of your working directory and staging area, use:
```sh
git status
```
This command shows which files are staged, unstaged, and untracked.

## Staging Changes
To stage changes for the next commit, use:
```sh
git add <file>
```
Replace `<file>` with the name of the file you want to stage. To stage all changes, use:
```sh
git add .
```

## Committing Changes
To commit staged changes, use:
```sh
git commit -m "Your commit message"
```
This command records the changes in the repository with a message describing the changes.

## Pushing Changes
To push your commits to a remote repository, use:
```sh
git push origin <branch>
```
Replace `<branch>` with the name of the branch you want to push to.

## Pulling Changes
To fetch and merge changes from a remote repository, use:
```sh
git pull origin <branch>
```
Replace `<branch>` with the name of the branch you want to pull from.

## Creating a New Branch
To create a new branch, use:
```sh
git branch <new-branch>
```
Replace `<new-branch>` with the name of the new branch.

## Switching Branches
To switch to a different branch, use:
```sh
git checkout <branch>
```
Replace `<branch>` with the name of the branch you want to switch to.

## Merging Branches
To merge another branch into your current branch, use:
```sh
git merge <branch>
```
Replace `<branch>` with the name of the branch you want to merge.

## Resolving Merge Conflicts
If there are merge conflicts, Git will mark the conflicted areas in the files. After resolving the conflicts, stage the resolved files and commit the changes:
```sh
git add <resolved-file>
git commit -m "Resolved merge conflict in <resolved-file>"
```
Replace `<resolved-file>` with the name of the file you resolved.

## Viewing Differences
To view the differences between your working directory and the staging area, use:
```sh
git diff
```
To view the differences between the staging area and the last commit, use:
```sh
git diff --cached
```

These commands cover some of the most useful operations in Git for managing your code and collaborating with others.
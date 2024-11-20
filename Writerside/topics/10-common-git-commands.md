# 10 common git commands

Here are the 10 of the most commonly used Git commands with descriptions and examples:

## `git init`

### Initialize a new Git repository

`git init` initializes a new Git database and sets up the basic structure for a version control system.

```bash
mkdir myproject
cd myproject
git init
```

## `git add <file>`

### Stage a file for commit

`git add <file>` adds one or more files to the index, preparing them for a future commit.

```bash
touch newfile.txt
git add newfile.txt
```

## `git add .`

### Stage all changes in the current directory and subdirectories

`git add .` adds all changes in the current directory and its subdirectories to the index, preparing them for a future commit.

```bash
git add .
```

## `git commit -m "<message>"`

### Commit changes with a meaningful message

`git commit -m "<message>"` creates a new commit with the specified message.

```bash
touch newfile.txt
echo "Hello World!" > newfile.txt
git add .
git commit -m "Initial commit"
```

## `git log`

### Display a list of commits made in the repository

`git log` shows a brief history of changes made to the project, including timestamps and commit messages.

```bash
git log
```

## `git branch <branch-name>`

### Create a new branch with the specified name

`git branch <branch-name>` creates a new branch from the current head (usually `master`) and moves the current branch to that new branch.

```bash
git branch feature/new-feature
```

## `git checkout <branch-name>`

### Switch to a different branch

`git checkout <branch-name>` switches to the specified branch, allowing you to work on that branch without affecting the other branches.

```bash
git checkout feature/new-feature
```

## `git merge <branch-name>`

### Merge changes from another branch into the current branch

`git merge <branch-name>` combines the changes made in one branch with those made in another branch, creating a new merge commit that contains both sets of changes.

```bash
git checkout master
git merge feature/new-feature
```

## `git remote add <name> <url>`

### Add a new remote repository to the local Git repository

`git remote add <name> <url>` links the local repository to another Git repository, allowing you to push and pull changes between them.

```bash
git remote add origin https://github.com/user/repo.git
```

## `git push <remote-name> <branch-name>`

### Push the current branch (or a specific set of commits) to the remote repository

`git push <remote-name> <branch-name>` sends changes from one repository to another, updating the central location for all collaborators working on that project.

```bash
git push origin master
```
# 25 essential git commands

### 1. Git init
Initializes a new Git repository in the current directory.

**Example:**
```sh
git init
```

### 2. Git commit
Records changes to the repository with a message describing the changes.

**Example:**
```sh
git commit -m "Initial commit"
```

### 3. Git branch
Lists, creates, or deletes branches.

**Example:**
```sh
git branch new-feature
```

### 4. Git checkout
Switches branches or restores working tree files.

**Example:**
```sh
git checkout new-feature
```

### 5. Git merge
Merges changes from one branch into the current branch.

**Example:**
```sh
git merge new-feature
```

### 6. Git pull
Fetches from and integrates with another repository or a local branch.

**Example:**
```sh
git pull origin main
```

### 7. Git remote
Manages set of tracked repositories.

**Example:**
```sh
git remote add origin git@github.com:user/repo.git
```

### 8. Git clone
Clones a repository into a new directory.

**Example:**
```sh
git clone git@github.com:user/repo.git
```

### 9. Git log
Shows the commit logs.

**Example:**
```sh
git log
```

### 10. Git fetch
Downloads objects and refs from another repository.

**Example:**
```sh
git fetch origin
```

### 11. Git blame
Shows what revision and author last modified each line of a file.

**Example:**
```sh
git blame file.txt
```

### 12. Git stash
Stashes changes in a dirty working directory away.

**Example:**
```sh
git stash
```

### 13. Git tag
Creates, lists, deletes or verifies tags.

**Example:**
```sh
git tag v1.0.0
```

### 14. Git cherry-pick
Applies the changes introduced by some existing commits.

*For more information on cherry-picking, see [this page](Git-Cherry-picking.md).*

**Example:**
```sh
git cherry-pick abc123
```

### 15. Git rebase
Reapplies commits on top of another base tip.

**Example:**
```sh
git rebase main
```

### 16. Git bisect
Uses binary search to find the commit that introduced a bug.

**Example:**
```sh
git bisect start
```

### 17. Git worktree
Manages multiple working trees.

**Example:**
```sh
git worktree add ../new-worktree new-branch
```

### 18. Git reflog
Records when the tips of branches and other references were updated in the local repository.

**Example:**
```sh
git reflog
```

### 19. Git rerere
Records and reuses conflict resolutions.

**Example:**
```sh
git rerere
```

### 20. Git submodule
Initializes, updates, or inspects submodules.

**Example:**
```sh
git submodule update --init
```

### 21. Git filter-branch
Rewrites branches.

**Example:**
```sh
git filter-branch --env-filter 'GIT_AUTHOR_NAME="New Name"' HEAD
```

### 22. Git update-index
Updates the index using the working directory content.

**Example:**
```sh
git update-index --assume-unchanged file.txt
```

### 23. Git gc
Runs a garbage collection to optimize the repository.

**Example:**
```sh
git gc
```

### 24. Git instaweb
Instantiates a web server with an interface into the local repository.

**Example:**
```sh
git instaweb
```

### 25. Git submodule foreach
Evaluates a shell command in each checked out submodule.

**Example:**
```sh
git submodule foreach 'git pull'
```
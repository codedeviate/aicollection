# 25 essential git commands

## 1. Git init
Initializes a new Git repository in the current directory.

*For more information on initializing a repository, see [this page](Git-Init.md).*

**Example:**
```sh
git init
```

## 2. Git commit
Records changes to the repository with a message describing the changes.

*For more information on committing changes, see [this page](Git-Commit.md).*

**Example:**
```sh
git commit -m "Initial commit"
```

## 3. Git branch
Lists, creates, or deletes branches.

*For more information on branching, see [this page](Git-Branch.md).*

**Example:**
```sh
git branch new-feature
```

## 4. Git checkout
Switches branches or restores working tree files.

*For more information on checking out branches, see [this page](Git-Checkout.md).*

**Example:**
```sh
git checkout new-feature
```

## 5. Git merge
Merges changes from one branch into the current branch.

*For more information on checkout, see [this page](Git-Checkout.md).*

**Example:**
```sh
git merge new-feature
```

## 6. Git pull
Fetches from and integrates with another repository or a local branch.

*For more information on pulling changes, see [this page](Git-Pull.md).*

**Example:**
```sh
git pull origin main
```

## 7. Git remote
Manages set of tracked repositories.

*For more information on adding a remote repository, see [this page](Git-Remote.md).*

**Example:**
```sh
git remote add origin git@github.com:user/repo.git
```

## 8. Git clone
Clones a repository into a new directory.

*For more information on cloning a repository, see [this page](Git-Clone.md).*

**Example:**
```sh
git clone git@github.com:user/repo.git
```

## 9. Git log
Shows the commit logs.

*For more information on viewing commit history, see [this page](Git-Log.md).*

**Example:**
```sh
git log
```

## 10. Git fetch
Downloads objects and refs from another repository.

*For more information on fetching changes, see [this page](Git-Fetch.md).*

**Example:**
```sh
git fetch origin
```

## 11. Git blame
Shows what revision and author last modified each line of a file.

*For more information on using `git blame`, see [this page](Git-Blame.md).*

**Example:**
```sh
git blame file.txt
```

## 12. Git stash
Stashes changes in a dirty working directory away.

*For more information on stashing changes, see [this page](Git-Stash.md).*

**Example:**
```sh
git stash
```

## 13. Git tag
Creates, lists, deletes or verifies tags.

*For more information on tagging commits, see [this page](Git-Tag.md).*

**Example:**
```sh
git tag v1.0.0
```

## 14. Git cherry-pick
Applies the changes introduced by some existing commits.

*For more information on cherry-picking, see [this page](Git-Cherry-picking.md).*

**Example:**
```sh
git cherry-pick abc123
```

## 15. Git rebase
Reapplies commits on top of another base tip.

*For more information on rebasing, see [this page](Git-Rebase.md).*

**Example:**
```sh
git rebase main
```

## 16. Git bisect
Uses binary search to find the commit that introduced a bug.

*For more information on using `git bisect`, see [this page](Git-Bisect.md).*

**Example:**
```sh
git bisect start
```

## 17. Git worktree
Manages multiple working trees.

*For more information on using `git worktree`, see [this page](Git-Worktree.md).*

**Example:**
```sh
git worktree add ../new-worktree new-branch
```

## 18. Git reflog
Records when the tips of branches and other references were updated in the local repository.

*For more information on using `git reflog`, see [this page](Git-Reflog.md).*

**Example:**
```sh
git reflog
```

## 19. Git rerere
Records and reuses conflict resolutions.

*For more information on using `git rerere`, see [this page](Git-Rerere.md).*

**Example:**
```sh
git rerere
```

## 20. Git submodule
Initializes, updates, or inspects submodules.

*For more information on using submodules, see [this page](Git-Submodule.md).*

**Example:**
```sh
git submodule update --init
```

## 21. Git filter-branch
Rewrites branches.

*For more information on using `git filter-branch`, see [this page](Git-Filter-branch.md).*

**Example:**
```sh
git filter-branch --env-filter 'GIT_AUTHOR_NAME="New Name"' HEAD
```

## 22. Git update-index
Updates the index using the working directory content.

*For more information on using `git update-index`, see [this page](Git-Update-index.md).*

**Example:**
```sh
git update-index --assume-unchanged file.txt
```

## 23. Git gc
Runs a garbage collection to optimize the repository.

*For more information on running `git gc`, see [this page](Git-Gc.md).*

**Example:**
```sh
git gc
```

## 24. Git instaweb
Instantiates a web server with an interface into the local repository.

*For more information on using `git instaweb`, see [this page](Git-Instaweb.md).*

**Example:**
```sh
git instaweb
```

## 25. Git submodule foreach
Evaluates a shell command in each checked out submodule.

*For more information on using `git submodule foreach`, see [this page](Git-Submodule.md).*

**Example:**
```sh
git submodule foreach 'git pull'
```
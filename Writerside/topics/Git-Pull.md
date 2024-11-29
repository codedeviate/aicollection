# pull

The `git pull` command is used to fetch and integrate changes from a remote repository into the current branch. It is a combination of two commands: `git fetch` and `git merge`. First, it fetches the changes from the remote repository, and then it merges those changes into the current branch.

## Detailed Explanation

1. **Fetching Changes**: The `git fetch` part of `git pull` retrieves the latest changes from the remote repository but does not integrate them into your working directory. It updates the remote-tracking branches.

2. **Merging Changes**: After fetching, the `git merge` part of `git pull` integrates the fetched changes into the current branch. If there are no conflicts, the merge happens automatically. If there are conflicts, you will need to resolve them manually.

3. **Fast-Forward Merge**: If the current branch has not diverged from the remote branch, Git will perform a fast-forward merge, simply moving the branch pointer forward.

4. **Three-Way Merge**: If the branches have diverged, Git will perform a three-way merge, creating a new commit that combines the changes from both branches.

5. **Rebasing**: You can use the `--rebase` option with `git pull` to rebase your local commits on top of the fetched commits instead of merging them. This can result in a cleaner project history.

## Examples

1. **Pulling Changes from the Remote Repository**:
   ```sh
   git pull origin master
   ```
   This command fetches the changes from the `master` branch of the remote repository `origin` and merges them into the current branch.

2. **Pulling with Rebase**:
   ```sh
   git pull --rebase origin master
   ```
   This command fetches the changes from the `master` branch of the remote repository `origin` and rebases the local commits on top of the fetched commits.
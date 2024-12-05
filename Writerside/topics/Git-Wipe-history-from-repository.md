# Wipe history from repository

> Dangerous and irreversible operation. Use with caution.
{style="warning"}

To wipe all history in a Git repository, you can follow these steps:

1. Create a new orphan branch.
2. Add all files to the new branch.
3. Commit the changes.
4. Delete the old branch.
5. Rename the new branch to the old branch name.
6. Force push the changes to the remote repository.

Here is the sequence of commands to achieve this:

```bash
# Create a new orphan branch
git checkout --orphan new-branch

# Add all files to the new branch
git add -A

# Commit the changes
git commit -m "Initial commit"

# Delete the old branch
git branch -D master

# Rename the new branch to the old branch name
git branch -m master

# Force push the changes to the remote repository
git push -f origin master
```

This will effectively wipe all history from the repository and start with a single commit. Be cautious, as this operation is destructive and cannot be undone.
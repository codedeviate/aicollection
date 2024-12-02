# shelve

`git shelve` is not a native Git command, but it is a concept similar to `git stash` that can be implemented using Git's features. Shelving changes allows you to temporarily set aside changes in your working directory without committing them, similar to stashing.

## Basic Usage

1. **Shelve Changes**

   To shelve changes, you can use `git stash` to save your current changes:

   ```sh
   git stash push -m "Shelve: <description>"
   ```

   This command stashes your changes with a message describing the shelve.

2. **List Shelved Changes**

   To list all stashed (shelved) changes, use:

   ```sh
   git stash list
   ```

   This will show a list of all stashed changes.

3. **Apply Shelved Changes**

   To apply shelved changes back to your working directory, use:

   ```sh
   git stash apply <stash@{n}>
   ```

   Replace `<stash@{n}>` with the identifier of the stash you want to apply.

4. **Drop Shelved Changes**

   To remove a specific shelved change, use:

   ```sh
   git stash drop <stash@{n}>
   ```

   Replace `<stash@{n}>` with the identifier of the stash you want to drop.

## Examples

1. **Shelve Changes with a Description**

   ```sh
   git stash push -m "Shelve: WIP on feature-x"
   ```

   This command stashes your current changes with the message "Shelve: WIP on feature-x".

2. **List All Shelved Changes**

   ```sh
   git stash list
   ```

   This command lists all stashed changes.

3. **Apply a Specific Shelved Change**

   ```sh
   git stash apply stash@{1}
   ```

   This command applies the changes from the stash with identifier `stash@{1}`.

4. **Drop a Specific Shelved Change**

   ```sh
   git stash drop stash@{1}
   ```

   This command drops the stash with identifier `stash@{1}`.

Using these commands, you can effectively manage shelved changes in your Git repository.
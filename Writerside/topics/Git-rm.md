# rm

`git rm` is a command used to remove files from the working directory and the staging area in a Git repository. It stages the removal of the specified files for the next commit.

## Basic Usage

1. **Remove a File**

   To remove a file from the working directory and stage the removal, use:

   ```sh
   git rm file.txt
   ```

   This will delete `file.txt` from the working directory and stage the removal.

2. **Remove a File from the Staging Area Only**

   To remove a file from the staging area but keep it in the working directory, use the `--cached` option:

   ```sh
   git rm --cached file.txt
   ```

   This will unstage `file.txt` but keep it in the working directory.

3. **Remove a Directory Recursively**

   To remove a directory and all its contents, use the `-r` option:

   ```sh
   git rm -r directory/
   ```

   This will delete the directory and all its contents from the working directory and stage the removal.

## Examples

1. **Remove a Single File**

   ```sh
   git rm src/old_file.txt
   ```

   This command removes `old_file.txt` from the `src` directory and stages the removal.

2. **Unstage a File but Keep It Locally**

   ```sh
   git rm --cached README.md
   ```

   This command unstages `README.md` but keeps it in the working directory.

3. **Remove a Directory and Its Contents**

   ```sh
   git rm -r docs/old_directory
   ```

   This command removes `old_directory` and all its contents from the `docs` directory and stages the removal.

Using `git rm` helps manage file removals in your Git repository efficiently.
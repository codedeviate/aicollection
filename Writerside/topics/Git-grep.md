# grep

`git grep` is a command used to search for specific patterns in the files tracked by Git. It is similar to the Unix `grep` command but is optimized for searching within a Git repository.

## Basic Usage

1. **Search for a Pattern in the Working Directory**

   To search for a pattern in the working directory, use the following command:

   ```sh
   git grep "pattern"
   ```

   This will search for the specified pattern in all files tracked by Git in the current working directory.

2. **Search for a Pattern in a Specific Branch**

   To search for a pattern in a specific branch, use the `-b` option followed by the branch name:

   ```sh
   git grep "pattern" branch_name
   ```

3. **Search for a Pattern in a Specific Commit**

   To search for a pattern in a specific commit, use the commit hash:

   ```sh
   git grep "pattern" commit_hash
   ```

4. **Search for a Pattern in a Specific Directory**

   To limit the search to a specific directory, specify the directory path:

   ```sh
   git grep "pattern" -- path/to/directory
   ```

5. **Search for a Pattern with Line Numbers**

   To include line numbers in the search results, use the `-n` option:

   ```sh
   git grep -n "pattern"
   ```

## Examples

1. **Search for the Word "TODO" in the Entire Repository**

   ```sh
   git grep "TODO"
   ```

2. **Search for the Word "FIXME" in the `main` Branch**

   ```sh
   git grep "FIXME" main
   ```

3. **Search for the Word "bug" in a Specific Commit**

   ```sh
   git grep "bug" 1a2b3c4d
   ```

4. **Search for the Word "function" in the `src` Directory**

   ```sh
   git grep "function" -- src
   ```

5. **Search for the Word "error" and Show Line Numbers**

   ```sh
   git grep -n "error"
   ```

These commands help you efficiently search for patterns within your Git repository, making it easier to locate specific code or comments.
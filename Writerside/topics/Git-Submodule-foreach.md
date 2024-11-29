# submodule foreach

The `git submodule foreach` command is used to execute a specified command in each submodule of a Git repository. This can be useful for performing batch operations on all submodules, such as updating, checking status, or running custom scripts.

## Detailed Explanation

1. **Executing Commands**: The `git submodule foreach` command runs the specified shell command in each submodule's directory. The command is executed in the context of each submodule, allowing you to perform operations as if you were in the submodule's directory.

2. **Submodule Context**: Within the command, you can use `$name` to refer to the submodule's name and `$path` to refer to the submodule's path.

3. **Recursive Option**: You can use the `--recursive` option to apply the command to nested submodules as well.

## Examples

1. **Updating All Submodules**:
   ```sh
   git submodule foreach git pull origin master
   ```
   This command updates each submodule to the latest commit on the `master` branch from its remote repository.

2. **Checking the Status of All Submodules**:
   ```sh
   git submodule foreach git status
   ```
   This command runs `git status` in each submodule, showing the current status of each one.

3. **Initializing and Updating All Submodules**:
   ```sh
   git submodule foreach git submodule init
   git submodule foreach git submodule update
   ```
   These commands initialize and update all submodules, ensuring they are properly set up and up-to-date.

4. **Running a Custom Script in All Submodules**:
   ```sh
   git submodule foreach './custom-script.sh'
   ```
   This command runs a custom script (`custom-script.sh`) in each submodule's directory.

5. **Listing the Paths of All Submodules**:
   ```sh
   git submodule foreach 'echo $path'
   ```
   This command prints the path of each submodule, which can be useful for scripting and automation.

These examples demonstrate how `git submodule foreach` can be used to perform various operations on all submodules in a repository.
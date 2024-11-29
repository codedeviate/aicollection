# init

The `git init` command is used to create a new Git repository. It can be used to convert an existing project into a Git repository or initialize a new, empty repository. When you run `git init`, it creates a new subdirectory named `.git` that contains all of the necessary repository files, including the metadata and object database for the repository. This command is the first step in creating a new repository.

## Detailed Explanation

- **Creates a `.git` directory**: This directory contains all the configuration files and directories that make up the repository.
- **Initializes a new repository**: This can be done in an existing directory or a new directory.
- **Sets up default branch**: By default, the initial branch is named `master` (or `main` in newer versions of Git).

## Example 1: Initialize a New Repository in an Existing Directory

```sh
# Navigate to your project directory
cd /path/to/your/project

# Initialize a new Git repository
git init
```

## Example 2: Initialize a New Repository and Create a New Directory

```sh
# Create a new directory for your project
mkdir new-project

# Navigate to the new directory
cd new-project

# Initialize a new Git repository
git init
```
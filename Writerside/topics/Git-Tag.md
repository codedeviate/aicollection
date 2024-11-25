# Tag

The `git tag` command is used to create, list, delete, and verify tags in Git repositories. Tags are used to mark specific points in the repository's history, typically used to mark release points (e.g., v1.0, v2.0).

### Detailed Explanation

1. **Creating Tags**: Tags can be lightweight or annotated. Lightweight tags are just pointers to a specific commit, while annotated tags store additional metadata such as the tagger's name, email, date, and a message.

2. **Listing Tags**: You can list all tags in the repository using the `git tag` command.

3. **Deleting Tags**: Tags can be deleted locally and remotely.

4. **Pushing Tags**: Tags are not automatically pushed to remote repositories. You need to explicitly push tags.

### Examples

1. **Creating an Annotated Tag**:
   ```sh
   git tag -a v1.0 -m "Release version 1.0"
   ```
   This command creates an annotated tag named `v1.0` with the message "Release version 1.0".

2. **Listing All Tags**:
   ```sh
   git tag
   ```
   This command lists all tags in the repository.
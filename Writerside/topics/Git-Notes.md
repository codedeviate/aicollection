# notes

Git notes are a way to add additional information to Git objects (commits, blobs, trees, and tags) without changing the objects themselves. Notes are stored in a separate namespace and can be used to annotate commits with extra information, such as code reviews, build statuses, or any other metadata.

## Key Features of Git Notes

1. **Non-intrusive**: Notes do not alter the original Git objects.
2. **Flexible**: Notes can be added, edited, and removed without affecting the commit history.
3. **Namespace**: Notes are stored in a separate namespace, allowing for multiple notes on the same object.

## Basic Commands

### Adding a Note
To add a note to a commit:
```sh
git notes add -m "This is a note for the commit"
```
This command adds a note to the current commit. You can specify a different commit by adding the commit hash at the end:
```sh
git notes add -m "This is a note for a specific commit" <commit-hash>
```

### Showing Notes
To display notes for a commit:
```sh
git notes show
```
To show notes for a specific commit:
```sh
git notes show <commit-hash>
```

### Editing a Note
To edit an existing note:
```sh
git notes edit
```
To edit a note for a specific commit:
```sh
git notes edit <commit-hash>
```

### Removing a Note
To remove a note:
```sh
git notes remove
```
To remove a note from a specific commit:
```sh
git notes remove <commit-hash>
```

## Advanced Usage

### Listing All Notes
To list all notes in the repository:
```sh
git notes list
```

### Merging Notes
If you have notes from different branches and want to merge them:
```sh
git notes merge <branch>
```

### Pruning Notes
To remove notes that are no longer referenced:
```sh
git notes prune
```

## Examples

### Adding a Note to a Commit
```sh
git notes add -m "Reviewed by John Doe"
```

### Showing a Note for a Specific Commit
```sh
git notes show 1a2b3c4d
```

### Editing a Note for a Specific Commit
```sh
git notes edit 1a2b3c4d
```

### Removing a Note from a Specific Commit
```sh
git notes remove 1a2b3c4d
```

### Listing All Notes Example
```sh
git notes list
```

### Merging Notes from Another Branch
```sh
git notes merge feature-branch
```

### Pruning Unreferenced Notes
```sh
git notes prune
```

Git notes provide a powerful way to annotate your Git objects with additional information, making it easier to manage and track metadata without altering the commit history.
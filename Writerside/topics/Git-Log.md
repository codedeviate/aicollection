# log

The `git log` command is used to display the commit history of a Git repository. It provides detailed information about each commit, including the commit hash, author, date, and commit message. This command is highly customizable, allowing you to filter and format the output in various ways.

## Detailed Explanation

1. **Basic Usage**: By default, `git log` shows the commit history in reverse chronological order (most recent commits first).

2. **Formatting Options**: You can customize the output format using various options, such as `--pretty`, `--oneline`, and `--graph`.

3. **Filtering Options**: You can filter the commit history based on criteria like author, date, and commit message using options like `--author`, `--since`, `--until`, and `--grep`.

4. **Limiting Output**: You can limit the number of commits displayed using the `-n` option, where `n` is the number of commits to show.

## Examples

1. **Basic Log**:
   ```sh
   git log
   ```
   This command displays the commit history with detailed information for each commit.

2. **One-line Log**:
   ```sh
   git log --oneline
   ```
   This command displays the commit history with each commit on a single line, showing the commit hash and message.

3. **Graphical Log**:
   ```sh
   git log --graph --oneline --all
   ```
   This command displays the commit history as a graph, with each commit on a single line, including all branches.
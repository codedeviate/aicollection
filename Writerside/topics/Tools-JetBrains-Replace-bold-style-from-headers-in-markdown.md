# Replace bold style from headers in markdown

When writing markdown documents, you might want to remove the `**` characters from bold text in headers. This can be useful when you want to convert markdown files to other formats or when you prefer a different styling for headers.

JetBrains editors (like IntelliJ IDEA, PyCharm, WebStorm, etc.) support regular expressions in their "Find and Replace" functionality, allowing you to apply this transformation. Here's how you can achieve it:

## Steps to Remove `**` from Headers in JetBrains Editors

1. **Open the Find and Replace Tool**:
    - Press `Ctrl + R` (Windows/Linux) or `Cmd + R` (macOS) for "Replace."
    - Check the **Regex** option (toggle it in the search bar).

2. **Enter the Regular Expression**:
    - Find:
      ```regex
      (?<=#.*)\*\*(.*?)\*\*
      ```
    - Replace:
      ```text
      $1
      ```

3. **Apply Changes**:
    - Review the matches JetBrains highlights in the editor.
    - Use "Replace All" or manually confirm each replacement with "Replace."

---

## Example:
### Input:
```markdown
# This is a **bold** header
## Another **example**
### A header with **bold** text
```

### Regular Expression in Find:
```regex
(?<=#.*)\*\*(.*?)\*\*
```

### Replacement Text:
```text
$1
```

### Output:
```markdown
# This is a bold header
## Another example
### A header with bold text
```

---

## Important Notes:
- The `(?<=#.*)` ensures that only lines starting with `#` are matched, targeting markdown headers specifically.
- Make sure the **Regex** option is enabled in the Find/Replace dialog; otherwise, the pattern won't work as intended.

## Compatibility with Other Editors

While this guide focuses on JetBrains editors, you can adapt the regular expression to work in other text editors that support regex-based find and replace functionality. The key is to adjust the pattern to match the specific markdown headers you want to modify.

The most common difference between editors is the syntax for capturing groups and backreferences, so you may need to adjust the replacement syntax accordingly. Backreferences are represented as `$1`, `$2`, etc. in JetBrains products, but some editors use `\1`, `\2`, etc.
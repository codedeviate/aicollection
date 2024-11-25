# Rerere

The `git rerere` (Reuse Recorded Resolution) command is a Git feature that helps manage and reuse conflict resolutions. When you encounter a merge conflict and resolve it, `git rerere` records the resolution. If the same conflict occurs again in the future, Git can automatically apply the recorded resolution, saving you time and effort.

### Detailed Explanation

1. **Enabling Rerere**: You need to enable `rerere` in your Git configuration. This can be done globally or per repository.

2. **Recording Resolutions**: When you resolve a conflict, `rerere` records the resolution in the `.git/rr-cache` directory.

3. **Reusing Resolutions**: If the same conflict occurs again, `rerere` automatically applies the recorded resolution.

4. **Cleaning Up**: You can clean up old or unused recorded resolutions to keep the `.git/rr-cache` directory manageable.

5. **Manual Intervention**: In some cases, `rerere` might not be able to apply the resolution automatically, and you may need to intervene manually.

### Examples

1. **Enabling Rerere Globally**:
   ```sh
   git config --global rerere.enabled true
   ```
   This command enables `rerere` for all repositories on your system.

2. **Enabling Rerere for a Specific Repository**:
   ```sh
   git config rerere.enabled true
   ```
   This command enables `rerere` for the current repository.

3. **Viewing Recorded Resolutions**:
   ```sh
   git rerere status
   ```
   This command shows the status of recorded resolutions, including any conflicts that have been resolved and recorded.

4. **Cleaning Up Old Resolutions**:
   ```sh
   git rerere gc
   ```
   This command cleans up old or unused recorded resolutions from the `.git/rr-cache` directory.

5. **Manually Recording a Resolution**:
   ```sh
   git rerere
   ```
   After resolving a conflict, running this command manually records the resolution if `rerere` is not enabled by default.

These commands help you manage and reuse conflict resolutions efficiently, making it easier to handle recurring conflicts in your Git workflow.
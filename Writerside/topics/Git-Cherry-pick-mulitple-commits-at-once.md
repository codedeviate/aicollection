# Cherry-pick mulitple commits at once

Git's **cherry-pick** command allows you to select specific commits from one branch and apply them to another. If you need to cherry-pick multiple commits from the same pull request (or a specific range of commits), you can do this efficiently. Here’s a step-by-step guide:

---

## **1. Identify the Commits**
To begin, identify the commits you want to cherry-pick. You can find these commits in the pull request, using a Git hosting service like GitHub or GitLab, or via the command line.

### Example 1:
Suppose the commits in the pull request are:

```
commit abc1234: "Added feature X"
commit def5678: "Fixed bug in feature X"
commit ghi9012: "Improved documentation"
```

---

## **2. Cherry-Pick a Single Commit**
To cherry-pick one commit:

```bash
git cherry-pick <commit-hash>
```

### Example 2:
```bash
git cherry-pick abc1234
```

This applies the changes from commit `abc1234` to your current branch.

---

## **3. Cherry-Pick Multiple Commits**
If you want to cherry-pick multiple commits:

### **a. List each commit explicitly**
You can list all the commit hashes you want to cherry-pick in a single command:

```bash
git cherry-pick <commit1> <commit2> <commit3>
```

### Example 3:
```bash
git cherry-pick abc1234 def5678 ghi9012
```

This will sequentially apply the three commits to your current branch.

### **b. Use a range of commits**
If the commits are consecutive (in a linear history), you can use a commit range:

```bash
git cherry-pick <start-commit>^..<end-commit>
```

- `<start-commit>`: The first commit in the range.
- `<end-commit>`: The last commit in the range.

**Important:** Use `^` to include the starting commit in the range.

### Example 4:
```bash
git cherry-pick abc1234^..ghi9012
```

This applies all the commits from `abc1234` to `ghi9012` inclusively.

---

## **4. Resolve Conflicts (if any)**
If there are conflicts during the cherry-pick process, Git will pause and allow you to resolve them. You can resolve conflicts as follows:

1. Open the conflicting files and manually fix the conflicts.
2. Stage the resolved files:
   ```bash
   git add <file>
   ```
3. Continue the cherry-pick process:
   ```bash
   git cherry-pick --continue
   ```

If you decide to abort the cherry-pick process:
```bash
git cherry-pick --abort
```

---

## **5. Verify the Changes**
After cherry-picking, verify that the commits have been successfully applied by checking the commit history:

```bash
git log
```

---

## **6. Push the Changes**
Once you're satisfied with the cherry-picks, push the changes to the remote repository:

```bash
git push origin <branch-name>
```

---

## **Example Workflow**
You’re working on a branch `main` and want to cherry-pick commits from a feature branch `feature/awesome-feature` that were part of a pull request.

1. Switch to `main`:
   ```bash
   git checkout main
   ```

2. Cherry-pick the commits:
   ```bash
   git cherry-pick abc1234 def5678 ghi9012
   ```

3. Resolve conflicts if necessary and continue.

4. Push the changes:
   ```bash
   git push origin main
   ```

---

## **Best Practices**
- **Keep commits clean:** Ensure that each cherry-picked commit has a clear and complete change set.
- **Use squash when necessary:** If the commits are small and tightly related, squash them into a single commit before cherry-picking to simplify history:
  ```bash
  git cherry-pick --no-commit <commit1> <commit2> <commit3>
  git commit -m "Merged features and fixes"
  ```
- **Test after cherry-picking:** Test your branch after applying the changes to confirm everything works as expected.

This approach ensures a clean and predictable cherry-picking process for multiple commits.
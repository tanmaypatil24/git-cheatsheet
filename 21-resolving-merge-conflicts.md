# 21. Resolving Merge Conflicts & Using Merge Tools

A merge conflict occurs when Git cannot automatically reconcile differences between two commits. This typically happens when two developers modify the exact same line in a file on different branches, or when one developer deletes a file that another developer is actively editing. Git pauses the merge or rebase, highlights the conflict, and asks you to choose which code to keep.

---

## Anatomy of a Conflict Marker

When Git encounters a conflict, it writes special markers directly inside the conflicting file:

```text
<<<<<<< HEAD
const apiUrl = "https://api.production-domain.com";
=======
const apiUrl = "https://api.staging-domain.com";
>>>>>>> feature/staging-config
```

### Explaining the Markers:
- **`<<<<<<< HEAD`**: Marks the beginning of the conflicting changes on your active local branch (where HEAD is pointed).
- **`=======`**: The divider between the two conflicting blocks.
- **`>>>>>>> feature/staging-config`**: Marks the end of the conflict and shows the name of the incoming branch/commit introducing the changes.

---

## Step-by-Step Conflict Resolution Workflow

### Step 1: Identify the Conflicts
When a conflict happens during `git merge` or `git pull`, Git outputs:
`Conflict: Merge conflict in [filename]. Automatic merge failed; fix conflicts and then commit the result.`

Run status to view exactly which files are blocking the merge:
```bash
git status
```
*Conflicting files are marked as `both modified`.*

---

### Step 2: Open and Edit the Conflicting Files
Open the conflicting files in your text editor (e.g. VS Code). You have four choices to resolve the conflict:
1. **Accept Current Change (HEAD)**: Keep your local branch code and discard the incoming branch changes.
2. **Accept Incoming Change**: Discard your local branch code and use the incoming branch changes.
3. **Accept Both Changes**: Keep both blocks of code.
4. **Manual Edit**: Rewrite the code entirely.

> [!IMPORTANT]
> Whichever option you choose, **you must delete all conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)** from the file before staging it!

---

### Step 3: Stage and Commit the Resolution
Once the file is cleaned up and saved, inform Git that the conflict is resolved by staging the file and finishing the merge:
```bash
# Step 1: Stage the resolved file
git add src/config.js

# Step 2: Complete the merge commit
git commit -m "merge: resolve API endpoint config conflict"
```

---

## Interactive Conflict Resolution with Merge Tools

Instead of manually editing files in text editors, you can configure interactive graphical merge tools (like **Meld**, **KDiff3**, **P4Merge**, or **VS Code**) to compare changes side-by-side in a 3-way split pane.

### 1. Configure VS Code as the Default Merge Tool
##### Purpose:
Sets up Visual Studio Code as your default graphical conflict resolution interface.

##### Syntax:
```bash
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd "code --wait --merge \$LOCAL \$REMOTE \$BASE \$MERGED"
```

---

### 2. Launch the Merge Tool
##### Purpose:
Opens the configured graphical merge tool for all files currently having conflicts.

##### Syntax:
```bash
git mergetool
```

---

## How to Abort a Merge in Panic

If you get flooded with dozens of complex conflicts and want to reset your repository to its exact pre-merge state to coordinate with your team:

##### Syntax:
```bash
# Abort during merge or pull
git merge --abort

# Abort during rebase
git rebase --abort
```

---

## Common Mistakes & Solutions

### Mistake 1: Committing Conflict Markers
**Problem**: You finished a merge conflict, ran `git commit`, and pushed to production. Your application crashed because conflict markers (`<<<<<<< HEAD`) were committed directly into your active JS or HTML code.
**Solution**: Never stage files without checking for markers. Search your codebase for `<<<<<<<` before staging. If it happened, edit the code to remove them, make a hotfix, and commit immediately.

### Mistake 2: Resolving Conflicts in a Rebase vs. Merge
**Problem**: You get confused because resolving conflicts during `git rebase` requires different final commands than `git merge`.
**Solution**: Keep this cheat sheet handy:
- **During `git merge`**: Fix code, run `git add <file>`, and complete with `git commit`.
- **During `git rebase`**: Fix code, run `git add <file>`, and complete with **`git rebase --continue`** (do not commit!).

---

## Best Practices
- **Communicate with authors**: If you are resolving conflicts on code you didn't write, talk to the teammate who wrote it before deciding which change to discard.
- **Keep branches short-lived**: The longer your feature branch sits without being integrated into `main`, the more files will diverge, leading to massive, unresolvable merge conflicts. Merge feature branches frequently!

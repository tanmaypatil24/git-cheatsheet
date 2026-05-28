# 15. Stashing: Stashing Code Temporarily

Sometimes you are working on a new feature in a branch, but you aren't ready to commit it. Suddenly, an urgent bug arises on `main` that you need to fix immediately. Switching branches with dirty, uncommitted changes can trigger conflicts or transfer changes to the destination branch in unexpected ways. Git Stashing solves this by saving your work-in-progress code on a local stack and reverting your working directory to a clean state.

---

## Core Stashing Commands

### 1. Stash Tracked Changes (Basic Stash)
##### Purpose:
Saves all tracked changes in your working directory and staging area to the stash stack, resetting your directory to a clean state.

##### Syntax:
```bash
git stash
# OR (Modern syntax with a custom description - HIGHLY RECOMMENDED)
git stash push -m "[Stash description]"
```

##### Real-world Example:
```bash
git stash push -m "wip: integration of stripe buttons"
```

---

### 2. Stash Including Untracked Files
##### Purpose:
By default, `git stash` only stashes modifications to already-tracked files. To stash newly created (untracked) files as well, you must use the untracked flag.

##### Syntax:
```bash
git stash -u
# OR
git stash --include-untracked
```

---

### 3. List Stashed Changes
##### Purpose:
Displays all stashes currently stored in your repository's local stash stack.

##### Syntax:
```bash
git stash list
```

##### Real-world Output:
```text
stash@{0}: On feature/auth: wip: integration of stripe buttons
stash@{1}: On main: WIP on payment page
```

---

### 4. Apply Stash (Keep in Stack)
##### Purpose:
Applies the stashed changes back into your current branch while **keeping** the stash inside the stash stack (safe for applying the same stash to multiple branches).

##### Syntax:
```bash
# Applies the most recent stash (stash@{0})
git stash apply

# Applies a specific stash from the stack
git stash apply stash@{[index]}
```

##### Real-world Example:
```bash
git stash apply stash@{1}
```

---

### 5. Pop Stash (Apply and Remove)
##### Purpose:
Applies the stashed changes back into your current branch and **immediately deletes** it from the stash stack.

##### Syntax:
```bash
# Pops the most recent stash
git stash pop

# Pops a specific stash
git stash pop stash@{[index]}
```

##### Real-world Example:
```bash
git stash pop stash@{0}
```

---

### 6. Delete a Stash
##### Purpose:
Deletes a specific stash or clears the entire stash stack.

##### Syntax:
```bash
# Delete a specific stash
git stash drop stash@{[index]}

# Delete ALL stashes in your local repository
git stash clear
```

##### Real-world Example:
```bash
git stash drop stash@{1}
```

---

### 7. View Stash Contents
##### Purpose:
Inspects what changes are inside a stash before applying it.

##### Syntax:
```bash
# Show file names and summary of changes
git stash show

# Show exact code diff of a stash
git stash show -p
```

---

## Stash Branching

### 8. Create a New Branch directly from a Stash
##### Purpose:
If your stashed changes conflict heavily with the latest edits on your active branch, you can create a brand new branch starting from the commit where you originally created the stash, and immediately apply the stash there.

##### Syntax:
```bash
git stash branch <new-branch-name> stash@{[index]}
```

##### Real-world Example:
```bash
git stash branch recovery-branch stash@{0}
```

---

## Common Mistakes & Solutions

### Mistake 1: Switching Branches and Losing Untracked Files
**Problem**: You ran `git stash` and switched branches, but your newly created files stayed in your directory or disappeared.
**Solution**: You forgot to use `git stash -u` (include untracked files). Make sure to always use `-u` when you have new files that haven't been staged or committed yet.

### Mistake 2: Stashing in a detached HEAD state
**Problem**: Stashing while in a detached HEAD state, which makes it harder to find or apply stashes safely on a branch later.
**Solution**: Pop the stash, switch to your target branch first, and apply the stash there.

---

## Best Practices
- **Always write stash messages**: Running `git stash` blindly makes it hard to identify what's inside when you run `git stash list` weeks later. Use `git stash push -m "WIP..."`.
- **Review before popping**: Use `git stash show -p` to inspect the stash contents before applying them to your active branch.
- **Keep stash stack clean**: Don't let stashes pile up indefinitely. If you no longer need stashed work, run `git stash drop` or `git stash clear` to free up space and maintain order.

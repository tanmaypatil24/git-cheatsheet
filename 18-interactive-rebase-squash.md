# 18. Interactive Rebase & Squashing Commits

An Interactive Rebase is one of Git's most powerful history-rewriting tools. It allows you to pause, edit, reorder, squash, or delete commits in your branch history. This is incredibly useful for cleaning up your local, unpushed commits so that your branch looks professional and clean before opening a Pull Request.

---

## What is Interactive Rebasing?

Running `git rebase -i` opens an interactive checklist in your configured text editor containing your recent commits in chronological order (oldest to newest). By editing the instruction command next to each commit, you instruct Git how to rewrite history.

### 1. Launch Interactive Rebase
##### Purpose:
Launches the interactive rebase interface for the last `n` commits.

##### Syntax:
```bash
git rebase -i HEAD~<number-of-commits>
# OR (Rebase starting from a specific parent commit)
git rebase -i <commit-hash>
```

##### Real-world Example (Clean up the last 4 commits):
```bash
git rebase -i HEAD~4
```

---

## Interactive Rebase Instructions Reference

When the editor opens, you will see a list of commits formatted like this:
```text
pick a1b2c3d feat: build login form UI
pick e5f6g7h fix: correct form validation typo
pick i9j0k1l wip: working on payment button
pick m2n3o4p feat: integrate stripe payment
```

You can replace the word `pick` with any of these instruction actions:

| Action | Alias | Description |
| :--- | :--- | :--- |
| **`pick`** | `p` | Keeps the commit as-is. |
| **`reword`** | `r` | Keeps the commit, but allows you to edit the commit message. |
| **`edit`** | `e` | Pauses the rebase at this commit, allowing you to modify files or add/remove code. |
| **`squash`** | `s` | Merges this commit's changes into the **previous** commit, combining their commit messages. |
| **`fixup`** | `f` | Merges this commit's changes into the **previous** commit, but **discards** this commit's message. |
| **`drop`** | `d` | Completely deletes the commit and all its code modifications. |

---

## Step-by-Step Guide: Squashing Commits

Squashing combines multiple small, intermediate commits (like `typo fix`, `WIP`) into a single, cohesive commit.

### Scenario:
You want to combine 3 recent commits into a single commit with a clean description `feat: build complete authentication system`.

#### Step 1: Launch Rebase
```bash
git rebase -i HEAD~3
```

#### Step 2: Configure Instructions in the Editor
Your editor will open. Modify the text to `squash` (or `s`) the subsequent commits into the first one:
```text
pick a1b2c3d feat: build login form UI
squash e5f6g7h fix: correct form validation typo
squash i9j0k1l feat: integrate backend session
```
*Save and close the editor tab.*

#### Step 3: Write a Clean Consolidated Message
Git will execute the squashes and then open a **second editor tab** containing the combined commit messages of all three commits. Clean it up and replace them with a single professional message:
```text
feat: build complete authentication system

- Implemented login form UI with responsive styles
- Added validation for form inputs
- Integrated backend session endpoints
```
*Save and close the editor.*

#### Step 4: Verification
Verify your clean, consolidated branch logs:
```bash
git log --oneline
```
Your 3 messy commits are now represented by a single professional commit!

---

## Aborting or Continuing Rebase

If you make a mistake or run into merge conflicts during a rebase:

```bash
# Abort and restore original branch state exactly
git rebase --abort

# Continue rebase after resolving conflicts and staging files
git add .
git rebase --continue
```

---

## Common Mistakes & Solutions

### Mistake 1: Squashing the Very First Commit
**Problem**: When editing the instruction list, you marked the top-most (oldest) commit as `squash`.
**Solution**: Git will throw an error because there is no prior commit to squash it into. The first commit in the interactive list must always remain `pick` (or `reword`/`edit`).

### Mistake 2: History Conflict on Push
**Problem**: After rebasing, running `git push` is rejected.
**Solution**: Since interactive rebase rewrites history, Git prevents a standard push. If you are on a private feature branch that no one else is using, you must force push:
```bash
git push origin feature/auth --force-with-lease
```

---

## Best Practices
- **Rebase before push**: Do an interactive rebase locally to clean up your development commits before opening a pull request.
- **Fixup vs. Squash**: Use `fixup` when combining tiny corrections (like "fix typo" or "fix indent") where the commit message is redundant. Use `squash` when you want to preserve the explanations of what was done.

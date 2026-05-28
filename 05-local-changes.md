# 05. Working with & Committing Local Changes

Once files are edited in your working directory, Git detects the modifications. Before committing, you must review your changes to ensure accuracy, stage the appropriate files, and then commit them with a meaningful, clear message.

---

## Reviewing Changes

### 1. View File Modifications
##### Purpose:
Shows details of modifications in the working directory that have not yet been staged.

##### Syntax:
```bash
git diff
```

---

### 2. View Modifications for a Specific File
##### Purpose:
Compares the working directory copy of a specific file with the last committed version.

##### Syntax:
```bash
git diff <filename>
```

##### Real-world Example:
```bash
git diff src/index.js
```

---

### 3. View Staged Differences
##### Purpose:
Compares files in the staging area with the last committed state (what will be committed if you run `git commit`).

##### Syntax:
```bash
git diff --staged
# OR
git diff --cached
```

---

## Committing Changes

### 4. Commit Staged Changes (Launches Text Editor)
##### Purpose:
Commits staged changes and opens the default text editor to write a detailed, multi-line commit message.

##### Syntax:
```bash
git commit
```

---

### 5. Commit with an Inline Message
##### Purpose:
Records staged changes in repository history with a short, single-line message.

##### Syntax:
```bash
git commit -m "[Your commit message]"
```

##### Real-world Example:
```bash
git commit -m "feat: integrate stripe checkout page"
```

---

### 6. Commit Skipping Staging (Tracked Files Only)
##### Purpose:
Stages and commits all modifications and deletions of tracked files in a single step.

##### Syntax:
```bash
git commit -am "[Your commit message]"
# OR
git commit -a -m "[Your commit message]"
```

> [!WARNING]
> `git commit -a` only works on files that are *already tracked* by Git. It will completely ignore newly created (untracked) files. Always double-check your `git status`!

---

## Modifying Existing Commits

### 7. Amend the Last Commit
##### Purpose:
Modifies the most recent commit. Perfect for adding forgotten files, correcting typos in the last commit message, or amending code without creating a new commit.

##### Syntax:
```bash
git commit --amend
# OR (Keep the previous commit message)
git commit --amend --no-edit
```

> [!CAUTION]
> **Rule of Thumb**: Never amend a commit that has already been pushed to a public/shared remote repository (`origin`). Amending rewrites commit hashes and can disrupt the histories of your collaborators.

---

### 8. Change Authorship/Date of the Last Commit
##### Purpose:
Overrides the author or committer dates of the last commit. Handy for synchronization or backdating if needed.

##### Syntax:
```bash
# Amend last commit with a custom author date
git commit --amend --date="[date]"

# Amend last commit with a custom committer date
GIT_COMMITTER_DATE="[date]" git commit --amend --no-edit
```

##### Real-world Example:
```bash
git commit --amend --date="2 days ago"
```

---

## Difference between Working Directory, Staging, and Commit Scopes

| Command | Compares | Used For |
| :--- | :--- | :--- |
| `git diff` | Working Directory vs. Staging Area | Reviewing what you edited before staging. |
| `git diff --staged` | Staging Area vs. Last Commit | Double-checking exactly what is about to be saved. |
| `git diff HEAD` | Working Directory vs. Last Commit | Viewing all modifications made since the last commit. |

---

## Best Practices
- **Commit atomicity**: A commit should represent a single logical unit of work (e.g. fix one bug, add one feature). Do not bundle unrelated changes.
- **Write descriptive messages**: Follow a consistent commit structure (e.g., [Conventional Commits](29-conventional-commits.md)). Prefix commit messages with `feat:`, `fix:`, `docs:`, `refactor:`, `style:`, or `test:`.
- **Review before committing**: Get into the habit of running `git diff --staged` right before you commit. This catches stray debugging logs and temporary code.
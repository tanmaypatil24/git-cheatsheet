# 08. Branching & Tagging Basics

Branching is Git's most powerful feature. It allows developers to diverge from the main line of development to work on new features, experiment, or fix bugs in isolation. Tags are static pointers that mark specific points in repository history (like releases).

---

## Branching Commands

### 1. List Branches
##### Purpose:
Lists active branches in the repository.

##### Syntax:
```bash
# List local branches
git branch

# List remote-tracking branches
git branch -r

# List all local and remote-tracking branches
git branch -a
```

---

### 2. Create a Branch (Without Switching)
##### Purpose:
Creates a new branch pointer at your current commit but does not switch your working directory to it.

##### Syntax:
```bash
git branch <branch-name>
```

##### Real-world Example:
```bash
git branch feature/payment-gateway
```

---

### 3. Switch Branches (Modern Syntax)
##### Purpose:
Switches your working directory to the target branch and updates your HEAD pointer.

##### Syntax:
```bash
git switch <branch-name>
```

##### Real-world Example:
```bash
git switch main
```

---

### 4. Create and Switch to a Branch (Modern Syntax)
##### Purpose:
Creates a new branch and immediately switches your active working directory to it.

##### Syntax:
```bash
git switch -c <branch-name>
```

##### Real-world Example:
```bash
git switch -c feature/dark-mode
```

---

### 5. Switch Branches (Legacy Syntax)
##### Purpose:
Historically used to switch branches or restore working tree files.

##### Syntax:
```bash
# Switch to an existing branch
git checkout <branch-name>

# Create and switch to a new branch
git checkout -b <branch-name>

# Switch back to the previously active branch (quick toggle)
git checkout -
```

> [!NOTE]
> **Switch vs. Checkout**: `git switch` was introduced in Git 2.23 to separate the responsibility of branch switching from file discarding (`git checkout` did both, which was confusing). It is highly recommended to use `git switch` for branch navigation.

---

### 6. Delete a Branch
##### Purpose:
Deletes a branch that is no longer needed.

##### Syntax:
```bash
# Safe delete (only if branch has been fully merged)
git branch -d <branch-name>

# Force delete (ignores merge status - CAUTION: will lose unmerged code!)
git branch -D <branch-name>
```

##### Real-world Example:
```bash
git branch -d feature/login-bugfix
```

---

### 7. Rename a Branch
##### Purpose:
Renames a branch.

##### Syntax:
```bash
# Rename the current branch you are on
git branch -m <new-branch-name>

# Rename a different branch
git branch -m <old-branch-name> <new-branch-name>
```

---

### 8. Delete a Remote Branch
##### Purpose:
Deletes the branch reference on your remote repository server (like GitHub).

##### Syntax:
```bash
git push <remote> --delete <branch-name>
```

##### Real-world Example:
```bash
git push origin --delete feature/contact-page
```

---

## Tagging Commands (Basics)

Tags represent fixed points in history. Unlike branches, tags do not change when new commits are made.

### 9. Create a Lightweight Tag
##### Purpose:
Creates a simple tag that is essentially just a pointer to a specific commit.

##### Syntax:
```bash
git tag <tag-name>
```

##### Real-world Example:
```bash
git tag v1.0.0-beta
```

---

### 10. Create an Annotated Tag
##### Purpose:
Creates a full, annotated Git object containing the tagger's name, email, date, and a specific tag message. Highly recommended for production releases.

##### Syntax:
```bash
git tag -a <tag-name> -m "[Tag release message]"
```

##### Real-world Example:
```bash
git tag -a v1.0.0 -m "Production release 1.0.0"
```

---

### 11. List and Filter Tags
##### Purpose:
Lists tags matching specific wildcards.

##### Syntax:
```bash
# List all tags
git tag

# Filter tags using wildcard patterns
git tag -l "[pattern]"
```

##### Real-world Example:
```bash
# Find all release versions starting with v1
git tag -l "v1.*"
```

---

### 12. Delete a Tag
##### Purpose:
Removes a tag locally.

##### Syntax:
```bash
git tag -d <tag-name>
```

---

### 13. Push Tags to Remote Server
##### Purpose:
Pushes local tags to the remote server (by default, `git push` does not push tags).

##### Syntax:
```bash
# Push a specific tag
git push origin <tag-name>

# Push all local tags in one go
git push origin --tags
```

---

## Branching & Tagging Comparison

| Concept | Can move? | Stores Metadata? | Typical Use Case |
| :--- | :--- | :--- | :--- |
| **Branch** | Yes (Moves automatically with commits) | No | Active feature development, bug fixes. |
| **Lightweight Tag** | No (Static reference) | No | Quick local testing, CI/CD targets. |
| **Annotated Tag** | No (Static reference) | Yes (Author, date, message) | Production version releases (e.g. `v2.4.0`). |

---

## Common Mistakes & Solutions

### Mistake 1: Deleting the Active Branch
**Problem**: You try to delete a branch you are currently working on (`git branch -d feature`), resulting in an error: `cannot delete branch 'feature' checked out at...`.
**Solution**: You must switch to a different branch (e.g. `git switch main`) before deleting the target branch.

### Mistake 2: Committing on a Tag
**Problem**: You checked out a tag (`git checkout v1.0.0`) and began making edits. This puts you in a **Detached HEAD** state. If you commit here, your commits aren't on any branch and will be lost.
**Solution**: Never commit directly on a tag. If you need to make modifications, create a branch from that tag first:
```bash
git switch -c bugfix-v1.0.0 v1.0.0
```

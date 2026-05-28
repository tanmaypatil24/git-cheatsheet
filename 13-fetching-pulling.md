# 13. Fetching vs. Pulling in Git

When working in a team, code modifications are constantly pushed to the remote repository on GitHub. To keep your local repository up to date, you must download those changes. Git offers two commands to download remote changes: **Fetch** and **Pull**. Understanding the difference is crucial to avoiding accidental merge conflicts.

---

## Fetching: The Safe Download

`git fetch` downloads all new commits, branches, and tags from the remote repository to your local machine, but **does not integrate them** into your active working directory. It simply updates your local tracking branches (like `origin/main`). It is a 100% safe operation that will never overwrite your active code.

### 1. Fetch from Default Remote
##### Purpose:
Downloads changes from your default remote repository (`origin`).

##### Syntax:
```bash
git fetch
```

---

### 2. Fetch a Specific Remote Branch
##### Purpose:
Downloads changes for a specific branch from the remote.

##### Syntax:
```bash
git fetch <remote-name> <branch-name>
```

##### Real-world Example:
```bash
git fetch origin feature/login
```

---

### 3. Review Fetched Commits
##### Purpose:
Reviews what commits were downloaded before merging them into your active branch.

##### Syntax:
```bash
# View the list of new remote commits
git log main..origin/main --oneline

# View differences between your local branch and remote tracking branch
git diff main origin/main
```

---

## Pulling: Fetching + Merging

`git pull` is a convenience command that performs **`git fetch` followed immediately by `git merge`**. It downloads remote changes and instantly tries to merge them into your current active local branch.

### 4. Pull Changes
##### Purpose:
Downloads and merges changes from the tracking branch of the remote server.

##### Syntax:
```bash
git pull <remote-name> <branch-name>
```

##### Real-world Example:
```bash
git pull origin main
```

---

### 5. Pull with Rebase (Highly Recommended)
##### Purpose:
Downloads remote changes and reapplies your local unpushed commits on top of them. This avoids messy merge commits and keeps your git tree clean and linear.

##### Syntax:
```bash
git pull --rebase <remote-name> <branch-name>
```

##### Real-world Example:
```bash
git pull --rebase origin main
```

---

### 6. Pull with Interactive Rebase
##### Purpose:
Invokes an interactive rebase during pull. This allows you to choose, edit, or squash your local commits as they are applied on top of the downloaded remote history.

##### Syntax:
```bash
git pull --rebase=interactive <remote-name> <branch-name>
# OR
git pull --rebase=i <remote-name> <branch-name>
```

---

## Force Operations

### 7. Force Push
##### Purpose:
Forces your local history onto the remote server, overwriting any changes on the server.

##### Syntax:
```bash
git push <remote> <branch> -f
# OR
git push <remote> <branch> --force
```

> [!CAUTION]
> **Use `--force-with-lease` instead of `--force`**: Direct force pushing is highly dangerous because it overwrites all remote commits blindly. If a teammate pushed code while you weren't looking, direct force push will erase their work. `--force-with-lease` is a safer alternative that blocks the force push if new commits have been made on the remote by someone else.
> ```bash
> git push origin main --force-with-lease
> ```

---

## Fetch vs. Pull Comparison

| Feature | `git fetch` | `git pull` |
| :--- | :--- | :--- |
| **Operation** | Fetch only. | Fetch + Merge (or Rebase). |
| **Safety** | **Extremely Safe** (Will never modify or delete your local code). | **Moderate Risk** (Can trigger merge conflicts or modify active files). |
| **Action** | Updates remote tracking branches (`origin/main`). | Merges changes directly into active local branch (`main`). |
| **Workflow** | Safe auditing of history before integrating. | Quick synchronization of local and remote. |

---

## Common Mistakes & Solutions

### Mistake: Pulling and Getting Flooded with Merge Conflicts
**Problem**: You ran `git pull` and got flooded with merge conflicts in files you were editing.
**Solution**: If you are not ready to solve them, abort the merge safely:
```bash
git merge --abort
```
To avoid this in the future, run `git fetch` first to inspect what was changed, or stash your changes before pulling:
```bash
git stash
git pull --rebase origin main
git stash pop
```
This cleanly reapplies your modifications on top of the updated remote history!

---

## Best Practices
- **Inspect before merging**: If you are working on critical branches, fetch first, inspect with `git log` or `git diff`, and then merge manually.
- **Prefer `pull --rebase`**: It avoids cluttering the history with auto-generated "Merge branch 'main' of github.com..." commits.
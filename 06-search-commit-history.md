# 06. Searching Code & Reviewing Commit History

As repositories grow, finding specific changes, understanding when a line of code was introduced, and tracking commit history becomes essential. Git provides robust tools for searching file contents (`git grep`) and auditing commit history (`git log` and `git blame`).

---

## Searching Code with Git Grep

### 1. Search Files for a Keyword
##### Purpose:
Searches all tracked files in your working directory for a specified keyword or phrase (much faster than traditional file search).

##### Syntax:
```bash
git grep "[search-query]"
```

##### Real-world Example:
```bash
# Search for standard API endpoints
git grep "fetchUserData"
```

---

### 2. Search a Specific Git Revision for a Keyword
##### Purpose:
Searches file contents within a historical commit, tag, or branch instead of your active working directory.

##### Syntax:
```bash
git grep "[search-query]" <commit-hash-or-tag-or-branch>
```

##### Real-world Example:
```bash
git grep "StripeCheckout" v2.5.0
```

---

## Searching Commit Logs (Pickaxe)

### 3. Find Commits that Added/Removed a Keyword
##### Purpose:
Audits commit history to find exactly when a keyword or variable name was added or deleted from any file (referred to as Git Pickaxe).

##### Syntax:
```bash
git log -S "[keyword]"
```

##### Real-world Example:
```bash
git log -S "secret_api_key"
```

---

### 4. Search Commit Logs with Regular Expressions
##### Purpose:
Uses Git Pickaxe with regular expressions to identify commits introducing specific code patterns.

##### Syntax:
```bash
git log -S "[regex]" --pickaxe-regex
```

---

## Reviewing Commit History

### 5. Standard Commit Log
##### Purpose:
Displays the complete commit history, starting with the newest, showing full hashes, author details, dates, and messages.

##### Syntax:
```bash
git log
```

---

### 6. Condensed Single-Line Commit Log
##### Purpose:
Shows a compressed view of commit history (abbreviated hash and commit message) for quick scannability.

##### Syntax:
```bash
git log --oneline
```

---

### 7. Filter Commits by Author
##### Purpose:
Filters the commit history to display only commits authored by a specific developer.

##### Syntax:
```bash
git log --author="[author-name]"
```

##### Real-world Example:
```bash
git log --author="Tanmay"
```

---

### 8. View Detailed History of a File
##### Purpose:
Displays every commit that modified a specific file, along with full patch details (exact line diffs).

##### Syntax:
```bash
git log -p <filename>
```

##### Real-world Example:
```bash
git log -p src/utils/auth.js
```

---

### 9. Compare Diverged History between Remote and Local
##### Purpose:
Shows commits that are present in one branch/remote but missing in another (using dot ranges).

##### Syntax:
```bash
git log --oneline <branch1>..<branch2>
```

##### Real-world Example (What's on remote main that I don't have local?):
```bash
git log --oneline main..origin/main
```

---

### 10. Audit Line-by-Line Changes (Git Blame)
##### Purpose:
Annotates each line of a file with the commit ID, author name, and date of the change. Excellent for finding out who wrote a line of code and why.

##### Syntax:
```bash
git blame <filename>
```

##### Real-world Example:
```bash
git blame package.json
```

---

## Reference Log (Reflog)

### 11. View local reference history
##### Purpose:
Shows the log of all movements of the local repository HEAD pointer (resets, commits, checkouts, merges). Reflog is a local safety net: it tracks *everything* you do, even if you delete a branch or hard reset a commit.

##### Syntax:
```bash
git reflog
```

---

## Common Mistakes & Solutions

### Mistake 1: Getting Trapped in Git Log
**Problem**: You ran `git log` and your terminal froze with a colon (`:`) at the bottom, and typing commands doesn't work.
**Solution**: Git uses a terminal pager (usually `less`) for long outputs. Simply press **`q`** to quit and return to your prompt.

### Mistake 2: Missing Renamed File Logs
**Problem**: Running `git log <file>` shows an empty log or very short history because the file was renamed in the past.
**Solution**: Append the `--follow` flag to instruct Git to search history past the rename boundaries:
```bash
git log --follow <file>
```

---

## Best Practices
- **Use graphical visualizations**: Make terminal logs easy to read by adding formatting options:
  ```bash
  git log --oneline --graph --all --decorate
  ```
- **Use reflog as a safety net**: Remember that Git rarely deletes anything permanently. If you run a destructive `git reset --hard` and lose commits, run `git reflog` immediately to find the old commit hash and restore it.
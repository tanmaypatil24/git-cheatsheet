# 07. Moving and Renaming Files in Git

Git is intelligent when it comes to tracking file movements and renames. Unlike other version control systems, Git doesn't explicitly record a rename; instead, it automatically detects that a file's content has moved to a new location. Using the correct Git commands for moving and renaming ensures that your commit history remains clear and unbroken.

---

## Core Commands

### 1. Rename or Move a File / Directory
##### Purpose:
Moves or renames a file or directory while automatically staging the change in Git. This avoids manual deletion and untracked file creation.

##### Syntax:
```bash
git mv <source> <destination>
```

##### Real-world Example (Renaming a file):
```bash
git mv Index.txt Index.html
```

##### Real-world Example (Moving a file into a folder):
```bash
git mv styles.css src/assets/styles.css
```

---

### 2. Forced Move / Rename
##### Purpose:
Forces a file to be renamed or moved, which is particularly useful on case-insensitive filesystems (like default macOS or Windows filesystems) when only changing the letter casing of a file name.

##### Syntax:
```bash
git mv -f <source> <destination>
```

##### Real-world Example (Changing casing of a filename on Windows):
If you try to run `git mv readme.md README.md` on a Windows system, Git may give an error like `bad source, source=readme.md, destination=README.md`. Use `-f` to force it:
```bash
git mv -f readme.md README.md
```

---

## Under the Hood: How Git Tracks Renames
Git does not store metadata about renames. Instead, it relies on content similarity.
- If a file is deleted in one path and created in another path with very similar content, Git's `git diff` and `git log` tools will automatically detect this as a **rename** (typically requiring at least 50% content similarity).
- To see rename detection in logs, you can run:
  ```bash
  git log --follow <file>
  ```
  The `--follow` flag is crucial because it instructs Git to continue showing the history of the file *before* it was renamed.

---

## Common Mistakes & Solutions

### Mistake 1: Renaming via File Explorer / Command Line instead of Git
**Problem**: You renamed a file using the OS File Explorer or standard OS terminal `mv` or `rename` command. Now `git status` shows the old file as `deleted` and the new file as `untracked`.
**Solution**:
1. Run `git add <new-file>` and `git add <old-file>` to stage both the deletion and addition. Git will automatically detect this as a rename.
2. Alternatively, prevent this entirely by using `git mv` directly.

### Mistake 2: Breaking Git File History
**Problem**: You renamed a file and then ran `git log <new-file>` but lost the history prior to the rename.
**Solution**: Use the `--follow` flag:
```bash
git log --follow <new-file>
```

---

## Best Practices
- **Always use `git mv`**: It is faster, stages the changes automatically, and prevents errors.
- **Do not mix heavy edits and renames**: If you rename a file, commit that rename *first* in its own commit, then make heavy content modifications in a subsequent commit. This ensures Git's similarity index easily catches the rename (100% match) without being confused by edits.

# 02. Setting Up & Configuring Git

Before using Git, you must configure your identity (username and email address). This information is permanently baked into every single commit you make, establishing clear authorship in version control history.

---

## Identity Setup

### 1. Set Global Username
##### Purpose:
Sets a name that identifies who made the commits in your version history.

##### Syntax:
```bash
git config --global user.name "[Firstname Lastname]"
```

##### Real-world Example:
```bash
git config --global user.name "Tanmay Patil"
```

---

### 2. Set Global Email
##### Purpose:
Sets the email address that will be associated with each of your commits.

##### Syntax:
```bash
git config --global user.email "[your-email@domain.com]"
```

##### Real-world Example:
```bash
git config --global user.email "tanmay.patil@example.com"
```

---

## Editor & UI Configurations

### 3. Enable Command-Line Colors
##### Purpose:
Enables automatic command-line coloring for Git output (making logs, diffs, and branch statuses easy to review).

##### Syntax:
```bash
git config --global color.ui auto
```

---

### 4. Configure VS Code as the Default Editor
##### Purpose:
Configures Visual Studio Code as your default text editor for writing commit messages and interactive rebases.

##### Syntax:
```bash
git config --global core.editor "code --wait"
```

> [!NOTE]
> The `--wait` flag is essential; it tells Git to pause the command line until you save and close the file tab in VS Code.

---

### 5. Configure Vim as the Default Editor (Fallback)
##### Purpose:
Configures the default terminal editor Vim for writing commit messages.

##### Syntax:
```bash
git config --global core.editor vi
```

> [!TIP]
> **How to Exit Vim**: If you find yourself trapped in a Vim commit message editor:
> 1. Press `Esc` to enter Command Mode.
> 2. Type `:wq` (write and quit) or `:q!` (quit without saving).
> 3. Press `Enter`.

---

### 6. Cache Git Credentials
##### Purpose:
Tells Git to store your credentials in disk, so you don't have to enter your password/token every time you push or pull.

##### Syntax:
```bash
git config credential.helper store
```

---

## Reviewing Git Configurations

### 7. View All Configurations
##### Purpose:
Lists all active configuration variables that Git can read, showing values from all scopes combined.

##### Syntax:
```bash
git config --list
```

---

### 8. View Configurations by Scope
##### Purpose:
Displays configuration settings applied specifically at a local, global, or system scope.

##### Syntax:
```bash
# Repository-specific configurations
git config --local --list

# User-specific configurations
git config --global --list

# System-wide configurations
git config --system --list
```

---

### 9. Edit Git Config File Directly
##### Purpose:
Opens your active global Git configuration file (`.gitconfig`) directly in your configured text editor.

##### Syntax:
```bash
git config --global --edit
```

---

## Configuration Scopes Explained

Git configurations are read from three different hierarchy levels:

| Scope | Location | Description |
| :--- | :--- | :--- |
| `--local` | `<repo>/.git/config` | Applied only to the current repository. Overrides global and system configurations. |
| `--global` | `~/.gitconfig` | Applied to all repositories for the current OS user. |
| `--system` | `/etc/gitconfig` | Applied system-wide to all users and all repositories on the machine. |

---

## Getting Help

### Use the Help Flag
##### Purpose:
Opens a detailed manual page of a Git command directly in your browser or terminal.

##### Syntax:
```bash
git <command> --help
# OR
git help <command>
```

##### Real-world Example:
```bash
git commit --help
```

---

## Best Practices
- **Configure matching GitHub emails**: Make sure the email you set with `git config --global user.email` matches an email registered to your GitHub account. If they do not match, GitHub won't display your profile avatar or count your commits in your green contribution graph.
- **Set a default branch name**: Modern Git uses `main` instead of `master` as the default branch name. Configure it globally:
  ```bash
  git config --global init.defaultBranch main
  ```
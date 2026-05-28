# 16. Advanced Git Config, SSH Setup & Aliases

As you master Git, configuring your local environment to maximize productivity and secure your connection to remote servers (like GitHub) is highly valuable. This chapter covers advanced Git configurations, setting up SSH key pairs, and creating custom Git aliases to save keystrokes.

---

## SSH Key Setup for GitHub

Using SSH keys allows you to authenticate your local machine with GitHub securely without entering your username and password for every push and pull.

### Step-by-Step SSH Configuration

#### Step 1: Generate a New SSH Key
##### Purpose:
Generates a highly secure SSH key pair using the modern Ed25519 algorithm.

##### Syntax:
```bash
ssh-keygen -t ed25519 -C "[your-github-email]"
```

##### Real-world Example:
```bash
ssh-keygen -t ed25519 -C "tanmay.patil@example.com"
```
*Note: Press `Enter` to accept the default file location, and optionally enter a secure passphrase.*

---

#### Step 2: Start the SSH Agent
##### Purpose:
Launches the background SSH agent service to manage your keys.

##### Syntax:
```bash
# Windows (PowerShell - run as Administrator if needed)
Start-Service ssh-agent
Set-Service -Name ssh-agent -StartupType Automatic

# macOS / Linux
eval "$(ssh-agent -s)"
```

---

#### Step 3: Add Key to the Agent
##### Purpose:
Registers your newly generated private key with the active SSH agent.

##### Syntax:
```bash
ssh-add ~/.ssh/id_ed25519
```

---

#### Step 4: Add the Key to Your GitHub Account
1. Copy the public key contents to your clipboard:
   ```bash
   # Windows (PowerShell)
   Get-Content ~/.ssh/id_ed25519.pub | clip
   
   # macOS
   pbcopy < ~/.ssh/id_ed25519.pub
   
   # Linux
   cat ~/.ssh/id_ed25519.pub
   ```
2. Open your web browser and go to GitHub -> **Settings** -> **SSH and GPG keys** -> **New SSH Key**.
3. Give it a descriptive Title (e.g. `Work Laptop`), paste the key in the **Key** field, and click **Add SSH key**.

---

#### Step 5: Test Connection
##### Purpose:
Verifies that your local machine can securely authenticate with GitHub.

##### Syntax:
```bash
ssh -T git@github.com
```

##### Real-world Output:
```text
Hi tanmaypatil24! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## Custom Git Aliases

Git aliases allow you to create custom shortcuts for longer or frequently typed commands. They are declared in your global `.gitconfig` file.

### Setting Up Aliases

You can set aliases from the command line:
```bash
git config --global alias.<shortcut> "<command>"
```

### Premium Time-Saving Aliases List
Here is a list of highly productive aliases to add to your `~/.gitconfig`:

```ini
[alias]
    # Quick status and branch viewing
    st = status
    co = checkout
    sw = switch
    br = branch
    ci = commit
    
    # Beautiful graphical logs
    lg = log --oneline --graph --decorate --all
    
    # Unstage files quickly
    unstage = restore --staged
    
    # Discard local changes in working tree
    discard = restore
    
    # Amend the last commit without modifying message
    amend = commit --amend --no-edit
    
    # Undo the last commit locally, keeping your code staged
    undo = reset --soft HEAD~1
```

##### Real-world Example (using custom aliases):
```bash
# Instead of typing git log --oneline --graph --decorate --all:
git lg

# Instead of typing git commit --amend --no-edit:
git amend
```

---

## Advanced Configurations

### 1. Configure Automatic Pruning on Fetch
##### Purpose:
Instructs Git to delete local references to branches that were deleted on the remote server (`origin`) whenever you run `git fetch` or `git pull`.

##### Syntax:
```bash
git config --global fetch.prune true
```

---

### 2. Auto-Stash on Rebase
##### Purpose:
Automatically stashes your local uncommitted edits before a rebase begins, and pops them when the rebase completes. This saves you from stashing manually before pulls!

##### Syntax:
```bash
git config --global rebase.autoStash true
```

---

## Best Practices
- **Never commit your private keys**: Your private key (`id_ed25519`) must remain secure on your local hard drive. Never push `.ssh` folder contents to any repository.
- **Use meaningful aliases**: Don't alias everything—only abbreviate commands that you type dozens of times a day to avoid forgetting core Git syntax.

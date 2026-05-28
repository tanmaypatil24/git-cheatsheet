# 01. Terminal Basics for Git Users

To work effectively with Git, having a basic comfort level with the Command Line Interface (CLI) is essential. Git commands are run inside the terminal, and navigating your system's directory structure is the first step in version control.

---

## Core Navigation & Directory Commands

### 1. List Directory Contents
##### Purpose:
Lists all files and folders in the current working directory.

##### Syntax:
```bash
ls [options]
```

##### Real-world Example:
```bash
ls
# List all files, including hidden ones (like the .git folder)
ls -a
# List files with detailed information (permissions, size, owner)
ls -la
```

---

### 2. List Contents of a Specific Folder
##### Purpose:
Lists files inside a specified directory without moving into it.

##### Syntax:
```bash
ls <foldername>
```

##### Real-world Example:
```bash
ls src/components
```

---

### 3. Print Working Directory
##### Purpose:
Prints the absolute path of the directory you are currently working in.

##### Syntax:
```bash
pwd
```

---

### 4. Change Directory
##### Purpose:
Jumps from the current directory into a different specified directory.

##### Syntax:
```bash
cd <path>
```

##### Real-world Example:
```bash
cd C:\Users\username\Projects\my-git-project
# Jump directly to your user home directory
cd ~
```

---

### 5. Move to Parent Directory
##### Purpose:
Jumps one level up into the parent folder of your current directory.

##### Syntax:
```bash
cd ..
```

---

### 6. Create an Empty Directory
##### Purpose:
Creates a new, empty directory inside the current folder.

##### Syntax:
```bash
mkdir <foldername>
```

##### Real-world Example:
```bash
mkdir git-cheatsheet
```

---

### 7. Open File Explorer to Current Folder
##### Purpose:
Opens the native file browser (Windows Explorer) focused on the current directory.

##### Syntax:
```bash
start .
```

---

## File Manipulation & Terminal Control

### 8. Clear the Terminal Screen
##### Purpose:
Clears the visual clutter in your command-line interface.

##### Syntax:
```bash
clear
```

---

### 9. Quit out of a Command / Pager
##### Purpose:
Exits interactive CLI pagers (like `git log` or `less` screens).

##### Syntax:
```bash
q
```

---

### 10. Delete a File
##### Purpose:
Deletes a specified file permanently.

##### Syntax:
```bash
rm <filename>
```

##### Real-world Example:
```bash
rm temp-notes.txt
```

---

### 11. Delete a Directory Recursively
##### Purpose:
Deletes a folder and all of its contents (files and subfolders) permanently.

##### Syntax:
```bash
rm -rf <foldername>
```

> [!WARNING]
> The `rm -rf` command is extremely destructive. It bypasses the recycle bin and immediately deletes the target. Double-check your path before running it!

---

## Common Mistakes & Solutions

### Mistake: Typing `cd folder` and getting "No such file or directory"
**Problem**: The folder either doesn't exist, or you misspelled it, or you are not in the parent folder of the directory you want to enter.
**Solution**: Run `pwd` to check where you are, then run `ls` to see what folders are actually available in your current directory.

---

## Best Practices
- **Use Tab Autocomplete**: Instead of typing out long folder names, type the first few letters and press `Tab` to autocomplete the name.
- **Avoid spaces in filenames and foldernames**: Use hyphens (`my-project`) or underscores (`my_project`) to make navigation simpler in the terminal.
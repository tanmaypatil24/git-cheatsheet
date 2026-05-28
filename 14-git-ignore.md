# 14. Everything About Git Ignore (.gitignore)

In software development, directories contain files that should **never** be committed to version control. These include local settings, system cache files, compiled build outputs, dependencies, and sensitive credentials. Git uses a special configuration file called `.gitignore` to skip tracking these files automatically.

---

## Why Ignore Files?

1. **Security**: Avoid committing private keys, database passwords, and personal API tokens.
2. **Speed & Size**: Do not upload massive directories (like `node_modules/` or compilation folders) which can slow down download and build times.
3. **OS-specific files**: Avoid cluttering repositories with local system-generated files (like `.DS_Store` on macOS or `Thumbs.db` on Windows) which have no value to developers on other platforms.

---

## How to Set Up a `.gitignore` File

1. Create a file named exactly `.gitignore` (with the dot prefix, no extension) in the root directory of your Git repository.
2. Add files or matching patterns inside the file (each file or pattern on a new line).
3. Stage and commit the `.gitignore` file:
   ```bash
   git add .gitignore
   git commit -m "chore: configure gitignore rules"
   ```

---

## Pattern Matching Syntax & Globs

The `.gitignore` file uses standard wildcard patterns (similar to shell globbing) to match files:

| Pattern | Match | Description |
| :--- | :--- | :--- |
| `*.notes` | `notes.notes`, `list.notes` | Ignores all files with a `.notes` extension in any folder. |
| `logs/` | `/logs/info.log`, `/src/logs/` | Ignores any directory named `logs` and all of its contents. |
| `/config.json` | `/config.json` | Ignores `config.json` in the **root** folder only (does not match `/src/config.json`). |
| `build/*.js` | `build/app.js` | Ignores `.js` files inside the `/build` directory, but not in its subdirectories (like `/build/static/app.js`). |
| `build/**/*.js` | `build/static/js/app.js` | Ignores `.js` files inside the `/build` directory and all nested subdirectories recursively. |
| `!important.notes` | `important.notes` | The exclamation mark (`!`) negates a rule, meaning this specific file will **never** be ignored, even if other rules would ignore it. |
| `# Comment` | *None* | Lines starting with a hash symbol (`#`) are treated as comments and ignored. |

---

## Ignoring an Already Tracked File

If a file was already staged or committed *before* you added it to `.gitignore`, Git will continue tracking it regardless of what you put in `.gitignore`. To stop tracking it:

##### Purpose:
Removes a file from tracking while keeping it on your local system.

##### Syntax:
```bash
git rm --cached <filename>
```

##### Real-world Example:
```bash
# Stop tracking config.json without deleting it from your hard drive
git rm --cached config.json
git commit -m "chore: stop tracking config.json"
```

---

## A Standard Web Project `.gitignore` Example

Here is a practical, production-ready `.gitignore` file for modern JS/Web projects:

```text
# Dependency folders
node_modules/
jspm_packages/

# Build and distribution directories
dist/
build/
.next/
.nuxt/

# Environment variables & secrets (CRITICAL)
.env
.env.local
.env.development.local
.env.test.local
.env.production.local
*.pem
*.key

# System Files
.DS_Store
Thumbs.db
desktop.ini

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*
logs/
*.log
```

---

## Best Practices
- **Configure `.gitignore` on day one**: Initialize your `.gitignore` file during your very first commit (`git init`) to prevent accidentally committing dependencies or logs.
- **Use online templates**: Don't write `.gitignore` files from scratch. Use reliable generators like [gitignore.io](https://www.toptal.com/developers/gitignore) or GitHub's official templates repository.
- **Never ignore your `.gitignore` file itself**: The `.gitignore` configuration must be committed to the repository so all team members share the same exclusion rules.

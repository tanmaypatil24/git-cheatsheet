# 24. Automating with Git Hooks & Husky

Git Hooks are custom scripts that Git runs automatically before or after specific operations (such as committing, pushing, or receiving). They are incredibly useful for enforcing code quality guidelines, running automated tests, formatting code (linting), and verifying commit messages before any code is saved or shared.

---

## How Git Hooks Work Locally

Every initialized Git repository contains a hidden directory located at `.git/hooks/`. By default, Git populates this folder with example shell scripts:

```text
.git/hooks/
├── pre-commit.sample
├── prepare-commit-msg.sample
├── commit-msg.sample
├── pre-push.sample
└── ...
```

### Activating a Hook Manually:
1. Navigate to `.git/hooks/`.
2. Rename an example file to remove the `.sample` extension (e.g. rename `pre-commit.sample` to `pre-commit`).
3. Edit the file to add custom shell commands (e.g. running your linter).
4. Make the script executable:
   ```bash
   chmod +x .git/hooks/pre-commit
   ```

---

## Common Git Hook Triggers

| Hook Name | Trigger Point | Use Case |
| :--- | :--- | :--- |
| **`pre-commit`** | Runs before writing the commit message. Can block commit. | Running linters, formatting code, checking for syntax errors. |
| **`commit-msg`** | Runs after writing commit message. Can block commit. | Verifying that the commit message conforms to a specific pattern (e.g. Conventional Commits). |
| **`pre-push`** | Runs before uploading commits to remote. Can block push. | Running unit tests or integration suites to prevent breaking remote builds. |
| **`post-merge`** | Runs after a merge completes successfully. | Automatically installing dependencies (e.g. `npm install`) if `package.json` was updated. |

---

## Bypassing Git Hooks in Emergencies

If you have configured a `pre-commit` or `pre-push` hook, but need to bypass automated scripts in an emergency (e.g. saving an hotfix immediately without running a long unit-test suite):

##### Syntax:
```bash
git commit -m "emergency hotfix" --no-verify
```

---

## Modern Git Hook Management with Husky

Configuring hook scripts inside `.git/hooks/` is difficult because the `.git/` folder is never committed to GitHub. To share Git hooks across your entire development team, JS projects use a utility called **Husky**.

### Step-by-Step Husky Configuration (Node/NPM)

#### Step 1: Install Husky
```bash
npm install husky --save-dev
```

#### Step 2: Initialize Husky configuration
```bash
npx husky init
```
This automatically:
- Creates a `.husky/` directory in your root folder.
- Configures your `package.json` to initialize hooks on install: `"prepare": "husky"`.
- Generates a default `pre-commit` file in `.husky/pre-commit`.

#### Step 3: Write Hook Actions
Open `.husky/pre-commit` and add the scripts you want to run automatically. For example, to format your code with Prettier and run lint checks before committing:

```bash
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

# Run linter and formatter
npm run lint
npm run format
```

Now, whenever a team member runs `git commit`, Husky intercepts the command, formats/tests the code, and blocks the commit if any code errors are found!

---

## Enforcing Commit Messages (Commitlint)

You can use Husky in combination with **Commitlint** to verify that everyone on your team writes standardized commit messages (e.g., following Conventional Commits).

#### Step 1: Install Commitlint
```bash
npm install --save-dev @commitlint/config-conventional @commitlint/cli
```

#### Step 2: Configure Commitlint Rules
Create a configuration file named `commitlint.config.js` in your root folder:
```javascript
module.exports = { extends: ['@commitlint/config-conventional'] };
```

#### Step 3: Create the Commit-Msg Hook
Register the hook with Husky:
```bash
echo "npx --no -- commitlint --edit \$1" > .husky/commit-msg
```
Now, trying to commit with a messy message like `fixed it` will be blocked by Commitlint! Only standard messages like `fix: resolve auth validation typo` will succeed.

---

## Best Practices
- **Do not overload pre-commit hooks**: A `pre-commit` hook should execute in under 10 seconds. Avoid running slow, end-to-end integration tests here; save those for the `pre-push` hook or your CI/CD server.
- **Ensure hooks are executable**: On macOS/Linux, if a newly created hook script is ignored by Git, run `chmod +x .husky/<hook-name>` to give the shell execution privileges.
- **Keep team workflows consistent**: Always use Husky or comparable tools (like `pre-commit` in Python ecosystems) to commit hook configurations to GitHub so your entire engineering team shares the same standard.

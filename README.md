# 🚀 The Ultimate Git & GitHub Cheatsheet

[![Git Version](https://img.shields.io/badge/git-2.45+-orange.svg?style=for-the-badge&logo=git)](https://git-scm.com/)
[![GitHub](https://img.shields.io/badge/github-ready-black.svg?style=for-the-badge&logo=github)](https://github.com/)
[![Status](https://img.shields.io/badge/status-production--ready-success.svg?style=for-the-badge)](#)

Welcome to the **Ultimate Git & GitHub Cheatsheet**! This repository is a clean, structured, highly professional reference designed for daily development usage, interview revision, and quick mastering of version control.

Whether you are a terminal beginner committing your first lines of code or a senior engineer orchestrating complex interactive rebases, multi-branch workflows, and CI/CD pipelines, this guide covers everything with zero fluff and maximum practicality.

---

## 🧭 Repository Navigation Map

The cheatsheet is divided into **30 structured, self-contained chapters** covering the entire spectrum of version control.

### 📁 Phase 1: Git Foundations (The Basics)

| Chapter | Topic | Key Commands |
| :--- | :--- | :--- |
| **[Chapter 01](01-terminal-basics.md)** | 🖥️ Terminal Basics | `ls`, `cd`, `pwd`, `mkdir`, `rm` |
| **[Chapter 02](02-git-setup.md)** | ⚙️ Initial Git Setup | `git config`, `user.name`, `core.editor` |
| **[Chapter 03](03-git-create.md)** | 🏗️ Creating Repositories | `git init`, `git clone`, `git status` |
| **[Chapter 04](04-staging-area.md)** | 📥 The Staging Area | `git add`, `git restore --staged`, `git add -p` |
| **[Chapter 05](05-local-changes.md)** | ✍️ Committing Changes | `git commit -m`, `git commit --amend`, `git diff` |
| **[Chapter 06](06-search-commit-history.md)** | 🔍 Searching & Logs | `git log`, `git grep`, `git blame`, `git reflog` |
| **[Chapter 07](07-move-rename.md)** | 📦 Moving & Renaming | `git mv`, `git mv -f`, rename tracking |
| **[Chapter 08](08-branches-tags-basics.md)** | 🌿 Branching & Tagging | `git switch`, `git switch -c`, `git tag` |
| **[Chapter 09](09-updating-publishing.md)** | 🌐 Remotes & Publishing | `git remote add`, `git push`, `git fetch` |
| **[Chapter 10](10-merge-rebase-basics.md)** | 🔀 Merge vs. Rebase | `git merge`, `git rebase` basics |

### 📁 Phase 2: Undoing & Workspace Control

| Chapter | Topic | Key Commands |
| :--- | :--- | :--- |
| **[Chapter 11](11-reset-revert-basics.md)** | 🔄 Reset vs. Revert | `git reset --hard`, `git revert`, `git clean` |
| **[Chapter 12](12-github-repositories.md)** | 🐙 GitHub Integration | `git push -u origin`, `origin/main` tracking |
| **[Chapter 13](13-fetching-pulling.md)** | 📥 Fetching vs. Pulling | `git pull --rebase`, `git fetch`, force-with-lease |
| **[Chapter 14](14-git-ignore.md)** | 🚫 Git Ignore Rules | `.gitignore` formatting, pattern matching |
| **[Chapter 15](15-stash-git.md)** | 🎒 Workspace Stashing | `git stash`, `git stash pop`, `git stash -u` |

### 📁 Phase 3: Advanced Operations & Collaboration

| Chapter | Topic | Key Commands |
| :--- | :--- | :--- |
| **[Chapter 16](16-git-config-advanced.md)** | 🔑 SSH Keys & Aliases | `ssh-keygen`, global `.gitconfig` alias scripts |
| **[Chapter 17](17-cherry-pick-reflog.md)** | 🍒 Cherry-Pick & Reflog | `git cherry-pick`, deep Reflog recovery, detached HEAD |
| **[Chapter 18](18-interactive-rebase-squash.md)** | 🔨 History Rewriting | `git rebase -i`, squash, fixup, reword, drop |
| **[Chapter 19](19-advanced-tags.md)** | 🏷️ Releases & SemVer | `git tag -a`, Semantic Versioning, pushing tags |
| **[Chapter 20](20-github-collaboration.md)** | 🤝 Forking & PR Workflows | `upstream` sync, pull requests, open-source setup |

### 📁 Phase 4: Enterprise Git & DevOps

| Chapter | Topic | Key Concepts |
| :--- | :--- | :--- |
| **[Chapter 21](21-resolving-merge-conflicts.md)** | 💥 Conflict Resolution | Marker parsing, `git mergetool`, Meld/VS Code setup |
| **[Chapter 22](22-advanced-workflows.md)** | 📐 Git Flow vs. Trunk | Git-Flow AVH, Trunk-Based Development, Monorepos |
| **[Chapter 23](23-git-submodules-worktrees.md)** | 🌳 Submodules & Worktrees | `git submodule`, `git worktree add` for multitasking |
| **[Chapter 24](24-git-hooks.md)** | 🪝 Git Hooks & Husky | `pre-commit`, Husky, Commitlint integration |
| **[Chapter 25](25-git-internals.md)** | 🔬 Git Under the Hood | Blobs, Trees, Commits, Refs, plumbing cat-file |
| **[Chapter 26](26-git-lfs-attributes.md)** | 💾 Large File Storage (LFS) | Git LFS config, `.gitattributes` line-endings |
| **[Chapter 27](27-git-security.md)** | 🛡️ Security & Purging | GPG Signatures, `git-filter-repo` history purging |
| **[Chapter 28](28-github-actions-cicd.md)** | ⚙️ GitHub Actions CI/CD | YAML test configuration, skip ci, status pipelines |
| **[Chapter 29](29-conventional-commits.md)** | 📋 Conventional Commits | Standardize prefix structures, automated changelogs |
| **[Chapter 30](30-git-roadmap.md)** | 🗺️ Progressive Roadmap | Beginner-to-Expert roadmap, visual tooling list |

---

## ⚡ Quick Start: Most-Used Commands Reference

If you are in a rush, here are the most frequently used commands that every developer runs daily:

```bash
# 1. Start a new repository
git init

# 2. Check changes and status
git status

# 3. Diff staged changes
git diff --staged

# 4. Stage and commit changes (Conventional Commit style)
git add .
git commit -m "feat: implement payment validation"

# 5. Clean update from remote main using rebase (Linear history)
git pull --rebase origin main

# 6. Push features safely to origin branch
git push -u origin feature/login
```

---

## 🛠️ Suggested Practice Workflow

To get the most out of this cheatsheet, we suggest adopting this clean workflow for your daily project commits:

```text
  [ Code ] ➔ [ git status ] ➔ [ git diff ] ➔ [ git add -p ]
                                                   │
  [ git push ] 🠔 [ git pull --rebase ] 🠔 [ git commit ]
```

1. **Audit modifications**: Run `git status` and `git diff` before doing anything.
2. **Stage selectively**: Use patch staging (`git add -p`) to review your code blocks line-by-line while staging.
3. **Draft commit**: Write a structured commit using [Conventional Commits style](29-conventional-commits.md) (`git commit -m "feat: ..."`).
4. **Pull safely**: Pull remote updates using rebase (`git pull --rebase origin main`).
5. **Publish**: Push features using `git push`.

---

## 🔌 Bonus Productivity Tools (Extensions)

Enhance your GitHub browser experience with these highly recommended, developer-proven extensions:

1. **[Octotree](https://www.octotree.io/)**: Adds a full, interactive file tree sidebar on the left side of GitHub pages, allowing you to browse repositories without opening endless tabs.
2. **[GitZip for GitHub](https://gitzip.org/)**: Enables double-clicking empty space next to folders/files to instantly download them individually as a `.zip` package.
3. **[Refined GitHub](https://github.com/refined-github/refined-github)**: Adds over 200 UX improvements to the default GitHub interface, including gray whitespace dots, clickable issue links, and visual feedback avatars.

---

## 🤝 Contribution Guidelines

This cheatsheet is a community-first developer resource. Contributions are highly welcome!

1. **Fork** the repository and create your custom feature branch:
   ```bash
   git switch -c feature/improved-git-hooks
   ```
2. Make your edits following the standard [Conventional Commits](29-conventional-commits.md) style.
3. Keep descriptions highly technical, concise, and focused on real-world application.
4. Open a **Pull Request** explaining what changes were introduced and why they improve the cheatsheet.

---

## 🎯 Master Mastery Roadmap

If you are looking to progressively master Git step-by-step, check out the comprehensive **[Progressive Git Mastery Roadmap](30-git-roadmap.md)** containing visual interactive tools, the Pro Git Book guidelines, and VS Code productivity extensions.

---

*Author: Tanmay Patil (GitHub: [@tanmaypatil15](https://github.com/tanmaypatil15))*  
*Made with ❤️ for developers worldwide.*

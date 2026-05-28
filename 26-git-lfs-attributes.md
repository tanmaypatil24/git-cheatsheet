# 26. Git Large File Storage (LFS) & .gitattributes

Git was built to track text-based source code files. When you try to track large binary assets (such as high-res graphics, audio samples, compiled binaries, video packages, or machine learning models), the repository size explodes. This is because Git downloads the complete history of every version of every binary file ever committed. **Git Large File Storage (LFS)** and the **`.gitattributes`** file solve this by storing heavy binary assets on external servers and replacing them with lightweight pointer files inside Git.

---

## 1. Git Large File Storage (LFS)

Git LFS replaces heavy files with a tiny 3-line pointer file that contains metadata (file size, GPG verification, and a SHA-256 hash pointing to the actual binary stored on an external LFS cloud host like GitHub). The binary is downloaded *only* when you checkout the branch, saving gigabytes of transfer data.

```text
version https://git-lfs.github.com/spec/v1
oid sha256:7b5a192e4c8f9d0c...
size 14205832
```

### Installing and Configuring Git LFS

#### Step 1: Install Git LFS locally
You only need to run this command once on your computer to set up the system-wide LFS filter:
```bash
git lfs install
```

#### Step 2: Track Specific Binary Formats
Tell Git LFS which file extensions it should intercept and track:
```bash
git lfs track "*.mp4"
git lfs track "*.psd"
git lfs track "assets/models/**"
```
*This command generates or updates a `.gitattributes` file in your repository root.*

#### Step 3: Commit the Configuration
You must commit the `.gitattributes` file to ensure all team members use the same LFS rules:
```bash
git add .gitattributes
git commit -m "chore: configure git lfs tracking for videos and assets"
```

#### Step 4: Add and Push Files Normally
Add your large files normally. Git LFS handles the transfers transparently behind the scenes:
```bash
git add assets/promo-video.mp4
git commit -m "media: add promo video asset"
git push origin main
```

---

## 2. Managing `.gitattributes`

The `.gitattributes` file is a special configuration file in your repository root that defines custom path-specific attributes (like line endings, merge strategies, and LFS filters) for files in your codebase.

### Core Features of `.gitattributes`

#### A. Enforcing Line Endings (CRLF vs LF)
A classic cross-platform bug is **Line Endings**: Windows uses Carriage Return Line Feed (`CRLF`) whereas macOS/Linux uses Line Feed (`LF`). This leads to Git showing entire files as modified when developers switch platforms. You can enforce a uniform line-ending standard in `.gitattributes`:

```text
# Set default behavior to automatic text line normalization
* text=auto

# Enforce Unix-style LF line endings on all source code files
*.js text eol=lf
*.html text eol=lf
*.css text eol=lf

# Enforce Windows-style CRLF line endings on batch scripts
*.bat text eol=crlf
```

#### B. Marking Binary Files explicitly
Tell Git to treat specific file formats as binary so it doesn't try to merge them or display code diffs:
```text
*.png binary
*.jpg binary
```

---

## Complete `.gitattributes` Configuration Example

Here is a practical, production-ready `.gitattributes` file combining line normalization, binary formats, and LFS:

```text
# ----------------------------------------------------------------------
# Line normalizations (ensure cross-platform consistency)
# ----------------------------------------------------------------------
* text=auto

*.js text eol=lf
*.jsx text eol=lf
*.ts text eol=lf
*.tsx text eol=lf
*.json text eol=lf
*.html text eol=lf
*.css text eol=lf
*.md text eol=lf

# ----------------------------------------------------------------------
# Binary formats (prevent text comparison diffs)
# ----------------------------------------------------------------------
*.png binary
*.jpg binary
*.gif binary
*.ico binary

# ----------------------------------------------------------------------
# Git LFS Filters (Large Assets)
# ----------------------------------------------------------------------
*.mp4 filter=lfs diff=lfs merge=lfs -text
*.zip filter=lfs diff=lfs merge=lfs -text
*.psd filter=lfs diff=lfs merge=lfs -text
*.pdf filter=lfs diff=lfs merge=lfs -text
```

---

## Common Mistakes & Solutions

### Mistake 1: Tracking a File in LFS *After* Committing It
**Problem**: You committed `large-video.mp4` to your repository, realized it was too big, installed LFS, and ran `git lfs track "*.mp4"`. Your repository size is still massive because the historical commit retains the full raw binary.
**Solution**: You must rewrite your history to migrate existing files to LFS. Use Git LFS's migration utility:
```bash
git lfs migrate import --include="*.mp4" --everything
```
*Warning: This rewrites commit history. Ensure you push using `--force` afterward, and notify teammates.*

### Mistake 2: Missing LFS Assets on Clone
**Problem**: A teammate cloned the repository, but all LFS tracked video or graphic files show up as broken, corrupt files on their hard drive.
**Solution**: They do not have Git LFS installed, so Git cloned the 3-line pointer files instead of the binaries. To solve it, install LFS and pull assets down explicitly:
```bash
git lfs install
git lfs pull
```

---

## Best Practices
- **Commit `.gitattributes` early**: Always set up your `.gitattributes` and LFS rules at the start of a project before committing binary files.
- **Set up GPG signature verification**: When using LFS, configure push verification to ensure binary assets uploaded are untampered.

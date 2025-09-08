# Git & GitHub with Termux — Complete Tutorial (Beginner → Advanced)

A comprehensive, professional guide to managing Git and GitHub entirely from **Termux on Android**. This README is designed to be copy‑paste friendly and safe to publish. Replace the placeholder values exactly where indicated.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Understand Android Paths in Termux](#understand-android-paths-in-termux)
3. [Initial Setup](#initial-setup)
4. [Configure Git (use your own identity)](#configure-git-use-your-own-identity)
5. [Authenticate with GitHub](#authenticate-with-github)
   - [Option A: SSH (recommended)](#option-a-ssh-recommended)
   - [Option B: HTTPS + Personal Access Token](#option-b-https--personal-access-token)
   - [Option C: GitHub CLI (optional)](#option-c-github-cli-optional)
6. [Create a New Repository from a Local Folder](#create-a-new-repository-from-a-local-folder)
7. [Clone an Existing Repository](#clone-an-existing-repository)
8. [Daily Commands & Workflow](#daily-commands--workflow)
9. [Branching, Rebasing, and Merging](#branching-rebasing-and-merging)
10. [Ignore Files and Attributes](#ignore-files-and-attributes)
11. [Large Files with Git LFS](#large-files-with-git-lfs)
12. [Submodules](#submodules)
13. [Tags and Releases](#tags-and-releases)
14. [GitHub Actions (CI) — Minimal Example](#github-actions-ci--minimal-example)
15. [Recommended Aliases & Quality of Life](#recommended-aliases--quality-of-life)
16. [Security Notes](#security-notes)
17. [Troubleshooting (Android/Termux Specific)](#troubleshooting-androidtermux-specific)
18. [FAQ](#faq)
19. [Appendix: Quick Reference](#appendix-quick-reference)

---

## Prerequisites
- Android phone with Termux installed.
- Internet access.
- A GitHub account.

Optional but helpful:
- A GitHub Personal Access Token (PAT) if you prefer HTTPS.
- A basic understanding of shell commands.

> Tip: Prefer working inside your Termux **home directory** (e.g., `~/projects`) to avoid Android shared-storage quirks. You can still access Downloads when needed.

---

## Understand Android Paths in Termux
- Termux home: `~` (e.g., `/data/data/com.termux/files/home`)
- Shared storage shortcut (after permission): `~/storage/shared/`
- Downloads shortcut: `~/storage/downloads/` → `/storage/emulated/0/Download`

Create a projects folder in home (recommended):
```bash
mkdir -p ~/projects && cd ~/projects
```

Grant storage access (for Downloads/DCIM etc.):
```bash
termux-setup-storage
```
Allow the permission when prompted.

---

## Initial Setup
Update packages and install tools:
```bash
pkg update -y && pkg upgrade -y
pkg install -y git openssh
# Optional editors/tools
pkg install -y nano vim curl unzip
```
Set a default editor (choose one):
```bash
# Use nano (simple)
git config --global core.editor 'nano -w'
# Or use vim
git config --global core.editor 'vim'
```

---

## Configure Git (use your own identity)
Replace the placeholders with your data:
- `<YOUR_NAME>` → your full name or handle
- `<YOUR_EMAIL>` → the email associated with your GitHub account

```bash
git config --global user.name "<YOUR_NAME>"
git config --global user.email "<YOUR_EMAIL>"

# Sensible defaults for Termux/Linux
git config --global init.defaultBranch main
# Android/shared storage may flip the executable bit unexpectedly
git config --global core.fileMode false
# Normalize line endings from any source to LF on commit
git config --global core.autocrlf input
```
Verify:
```bash
git config --global --list
```

---

## Authenticate with GitHub
Pick **one** method. SSH is recommended for convenience and security.

### Option A: SSH (recommended)

1) Generate an SSH key (replace email):
```bash
ssh-keygen -t ed25519 -C "<YOUR_EMAIL>"
# Press Enter to accept the default path (~/.ssh/id_ed25519)
# Optionally set a passphrase for better security
```

2) (Optional) Start an agent and add your key if you set a passphrase:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

3) Copy the **public** key and add it to GitHub → Settings → SSH and GPG keys → New SSH key:
```bash
cat ~/.ssh/id_ed25519.pub
# Copy the entire single line output and paste into GitHub
```

4) Test the connection:
```bash
ssh -T git@github.com
# Expect a greeting that confirms authentication
```

### Option B: HTTPS + Personal Access Token
- Create a token in GitHub → Settings → Developer settings → Personal access tokens.
- Scope: at minimum, `repo` for private repositories.
- Use the token **instead of a password** when Git prompts.

Placeholders:
- `<GITHUB_USERNAME>` → your GitHub handle
- `<PERSONAL_ACCESS_TOKEN>` → your generated token

Example (first push will prompt for username and token):
```bash
git remote add origin https://github.com/<GITHUB_USERNAME>/<REPO_NAME>.git
# When asked for password, paste the token (not your GitHub password)
```

### Option C: GitHub CLI (optional)
If available on your Termux setup, the CLI simplifies auth and common tasks.
```bash
pkg install -y gh || true
# Then
gh auth login
```
Follow the prompts to authenticate via browser or token.

---

## Create a New Repository from a Local Folder
This is how to upload an existing local project to a new GitHub repository.

Placeholders you will replace:
- `<LOCAL_PROJECT_DIR>` → path to your project (e.g., `~/storage/downloads/my-project` or `~/projects/my-project`)
- `<GITHUB_USERNAME>` → your GitHub handle
- `<REPO_NAME>` → repository name you created on GitHub

```bash
cd <LOCAL_PROJECT_DIR>

# Initialize the repository if not already initialized
git init

# Stage and commit all files
git add .
git commit -m "Initial commit"

# Add the remote — choose SSH or HTTPS
# SSH:
git remote add origin git@github.com:<GITHUB_USERNAME>/<REPO_NAME>.git
# HTTPS:
# git remote add origin https://github.com/<GITHUB_USERNAME>/<REPO_NAME>.git

# Set the default branch and push
git branch -M main
git push -u origin main
```

If you see a "dubious ownership" or permission error when working under shared storage, mark the directory safe (replace path):
```bash
git config --global --add safe.directory <ABSOLUTE_PATH_TO_YOUR_PROJECT>
```
You can get the absolute path with `pwd`.

---

## Clone an Existing Repository
Placeholders:
- `<GITHUB_USERNAME>` and `<REPO_NAME>` as before

```bash
# SSH
git clone git@github.com:<GITHUB_USERNAME>/<REPO_NAME>.git

# HTTPS
git clone https://github.com/<GITHUB_USERNAME>/<REPO_NAME>.git

cd <REPO_NAME>
```

---

## Daily Commands & Workflow
Status, diffs, and history:
```bash
git status
git diff
git log --oneline --graph --decorate --all
```

Typical loop:
```bash
# Update local main before starting work
git switch main
git pull --ff-only

# Create a feature branch
git switch -c feature/<FEATURE_NAME>

# Make changes, then stage & commit
git add -A
git commit -m "<COMMIT_MESSAGE>"

# Publish the branch
git push -u origin feature/<FEATURE_NAME>
```

Open a Pull Request (choose one):
- From GitHub web: compare `feature/<FEATURE_NAME>` into `main`.
- With GitHub CLI:
```bash
gh pr create --fill --head feature/<FEATURE_NAME>
```

After merge, clean up locally:
```bash
git switch main
git pull --ff-only
git branch -d feature/<FEATURE_NAME>
```

---

## Branching, Rebasing, and Merging
Keep a clean history by rebasing your feature branch on top of `main`:
```bash
git fetch origin
git rebase origin/main
# Resolve conflicts if any → edit files →
git add <FILE>
git rebase --continue
```
Prefer fast‑forward merges where possible:
```bash
git merge --ff-only feature/<FEATURE_NAME>
```
If you want a merge commit even when fast‑forward is possible:
```bash
git merge --no-ff feature/<FEATURE_NAME>
```

Undo tactics:
```bash
# Discard unstaged changes in a file
git restore <FILE>
# Undo the last commit but keep changes staged
git reset --soft HEAD~1
# Create a new commit that reverts a specific commit
git revert <COMMIT_SHA>
```

Stash for quick context switches:
```bash
git stash
# Later
git stash pop
```

---

## Ignore Files and Attributes
Create a `.gitignore` at repo root:
```
# Dependencies and caches
node_modules/
*.log
.tmp/

# Environment/config
.env
.env.*

# OS/editor noise
.DS_Store
Thumbs.db
*.swp
```

Useful `.gitattributes` examples:
```
# Ensure text files use LF endings (good for Android/Linux)
* text=auto eol=lf

# Treat images and binaries correctly
*.png binary
*.jpg binary
*.pdf binary

# Shell scripts should be normalized to LF
*.sh text eol=lf
```

---

## Large Files with Git LFS
Track large/binary files efficiently:
```bash
pkg install -y git-lfs || true

git lfs install
git lfs track "*.mp4" "*.psd" "*.zip"
# This writes patterns to .gitattributes

git add .gitattributes
git add <LARGE_FILE>
git commit -m "Track large assets with LFS"
git push
```

---

## Submodules
Embed another repository inside your project:
```bash
git submodule add https://github.com/<OWNER>/<OTHER_REPO>.git vendor/other

git commit -m "Add submodule"
```
After cloning a project that contains submodules:
```bash
git submodule update --init --recursive
```

---

## Tags and Releases
Lightweight versioning with tags:
```bash
git tag -a v1.0.0 -m "First stable release"
git push origin v1.0.0
```
Create a GitHub Release from the tag using the web UI or GitHub CLI.

---

## GitHub Actions (CI) — Minimal Example
Add a workflow file at `.github/workflows/ci.yml`:
```yaml
name: CI
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      - name: Install deps
        run: npm ci
      - name: Lint & test
        run: |
          npm run lint --if-present
          npm test --if-present
```
Commit and push — the workflow runs automatically on GitHub.

---

## Recommended Aliases & Quality of Life
```bash
# A compact, decorated log view
git config --global alias.lg "log --oneline --graph --decorate --all"
# Shortcuts
git config --global alias.st status
git config --global alias.cm "commit -m"
```
Usage:
```bash
git lg
```

---

## Security Notes
- Prefer **SSH** or **GitHub CLI** over storing HTTPS tokens.
- If you must use HTTPS + token, never commit or share your token. Treat it like a password.
- Avoid committing secrets (`.env`, API keys). Use `.gitignore` to exclude them.
- Consider enabling 2FA on GitHub.

---

## Troubleshooting (Android/Termux Specific)

### 1) Permission denied (publickey)
- Ensure your SSH public key is added to GitHub.
- Test with `ssh -T git@github.com`.
- If you set a passphrase, start the agent and add the key:
  ```bash
  eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519
  ```

### 2) fatal: detected dubious ownership
- Common under shared storage. Mark the directory as safe:
  ```bash
  git config --global --add safe.directory <ABSOLUTE_PATH_TO_REPO>
  ```

### 3) HTTPS asks for password and fails
- Use a **Personal Access Token** (PAT) instead of your GitHub password.

### 4) Line-ending noise in diffs
- Ensure:
  ```bash
  git config --global core.autocrlf input
  ```
- And add `* text=auto eol=lf` in `.gitattributes`.

### 5) Executable-bit flips on files
- Keep `core.fileMode=false` (already set above).

### 6) Working under Downloads vs Home
- Android shared storage can have metadata quirks. Prefer repos under `~/projects` whenever possible.

### 7) Git LFS not found
- Try installing with `pkg install git-lfs`. If unavailable on your device/repo mirrors, consider installing a prebuilt binary or use SSH/HTTPS without LFS for non‑large files.

---

## FAQ
**Q: Where exactly do I put my own data?**
- In commands, replace placeholders wrapped like `<THIS>`:
  - `<YOUR_NAME>`, `<YOUR_EMAIL>` in Git config
  - `<GITHUB_USERNAME>`, `<REPO_NAME>` in remotes
  - `<LOCAL_PROJECT_DIR>` when `cd`‑ing into your project
  - `<FEATURE_NAME>` and `<COMMIT_MESSAGE>` for branches and commits
  - `<ABSOLUTE_PATH_TO_REPO>` when marking a safe directory

**Q: Should I use SSH or HTTPS?**
- SSH is convenient and avoids repeated token prompts. HTTPS + token is fine if you prefer it.

**Q: Can I work entirely from Downloads?**
- Yes, but if you hit permission or ownership warnings, move the project to `~/projects` or mark the directory as safe.

---

## Appendix: Quick Reference

### Quick Start — New Repo from Local Folder
```bash
cd <LOCAL_PROJECT_DIR>
git init
git add .
git commit -m "Initial commit"
git branch -M main
# Add one of the following remotes and push:
# SSH
git remote add origin git@github.com:<GITHUB_USERNAME>/<REPO_NAME>.git
# HTTPS
# git remote add origin https://github.com/<GITHUB_USERNAME>/<REPO_NAME>.git

git push -u origin main
```

### Quick Start — Clone & Contribute
```bash
git clone git@github.com:<GITHUB_USERNAME>/<REPO_NAME>.git
cd <REPO_NAME>
git switch -c feature/<FEATURE_NAME>
# edit files
git add -A
git commit -m "<COMMIT_MESSAGE>"
git push -u origin feature/<FEATURE_NAME>
```

### Useful Logs
```bash
git log --oneline --graph --decorate --all
git lg
```

---

End of guide.

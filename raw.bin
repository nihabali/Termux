# Git & GitHub with Termux — Complete Guide

This guide explains how to manage Git and GitHub entirely from **Termux on Android**. It is designed to be clean, professional, and copy‑paste friendly. Every command is written in separate blocks so you can copy them one by one.

---

## 1. Install Git in Termux

```bash
pkg update && pkg upgrade -y
pkg install git -y
termux-setup-storage
```

**Explanation:**  
- Updates Termux packages.  
- Installs Git.  
- Grants Termux access to your phone storage.  

---

## 2. Configure Git (One-time Setup)

```bash
git config --global user.name "your-github-username"
git config --global user.email "your-github-email"
```

**Explanation:**  
This sets your GitHub username and email for commits.  

---

## 3. Initialize a Repository

Go to your project folder (example: `crosshair`) and run:

```bash
cd /storage/emulated/0/Download/crosshair
git init
git branch -M main
```

**Explanation:**  
- `git init` starts a new repository.  
- `git branch -M main` renames the default branch to `main`.  

---

## 4. Connect to GitHub Repository

```bash
git remote add origin https://github.com/your-username/your-repo.git
```

**Explanation:**  
Links your local project with the GitHub repository.  

If you get an error `remote origin already exists`, reset it:

```bash
git remote remove origin
git remote add origin https://github.com/your-username/your-repo.git
```

---

## 5. Stage and Commit Files

```bash
git add .
git commit -m "Initial upload"
```

**Explanation:**  
- `git add .` stages all files.  
- `git commit -m` saves the changes locally.  

---

## 6. Push Files to GitHub

### If the GitHub repo is empty:
```bash
git push -u origin main
```

### If the GitHub repo already has files (like README.md):
```bash
git pull origin main --allow-unrelated-histories
git push origin main
```

### If you want to replace everything on GitHub with local files:
```bash
git push origin main --force
```

---

## 7. Clone an Existing Repository

```bash
git clone https://github.com/your-username/your-repo.git
```

**Explanation:**  
Downloads a GitHub repo to Termux.  

---

## 8. Update Local Repository (Pull Changes)

```bash
git pull origin main
```

**Explanation:**  
Fetches and merges latest changes from GitHub.  

---

## 9. Replace Remote Repository

To remove and set a new remote:

```bash
git remote remove origin
git remote add origin https://github.com/your-username/new-repo.git
```

---

## 10. Reset Repository Completely

If you want to delete all Git settings and start fresh:

```bash
rm -rf .git
git init
git branch -M main
git remote add origin https://github.com/your-username/your-repo.git
```

---

## 11. Using HTTPS vs SSH

### HTTPS (simpler, asks for username & password/token):
```bash
git clone https://github.com/your-username/your-repo.git
```

### SSH (requires SSH key setup, no password each time):
```bash
git clone git@github.com:your-username/your-repo.git
```

To generate SSH key in Termux:
```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
cat ~/.ssh/id_rsa.pub
```

Copy the output and add it to your GitHub SSH keys.  

---

## 12. Create a Pull Request (PR)

1. Fork the repository on GitHub.  
2. Clone your fork in Termux.  
3. Create a new branch:  

```bash
git checkout -b feature-branch
```

4. Make changes and commit:  

```bash
git add .
git commit -m "Added new feature"
```

5. Push branch:  

```bash
git push origin feature-branch
```

6. Open GitHub website → Create Pull Request.  

---

## 13. Common Errors & Fixes

- **Error:** `remote origin already exists`  
  **Fix:**  
  ```bash
  git remote remove origin
  git remote add origin https://github.com/your-username/your-repo.git
  ```

- **Error:** `failed to push some refs`  
  **Fix (merge with remote):**  
  ```bash
  git pull origin main --allow-unrelated-histories
  git push origin main
  ```  
  **Fix (overwrite remote):**  
  ```bash
  git push origin main --force
  ```

- **Error:** `Reinitialized existing Git repository`  
  **Fix:**  
  ```bash
  rm -rf .git
  git init
  ```

---

# Conclusion

With these commands, you can fully manage Git and GitHub from Termux — including repository setup, uploads, replacements, pull requests, and error handling.

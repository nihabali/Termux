# Termux Git & GitHub – Complete Tutorial (Beginner to Advanced)

## 1. What is Termux?
**Termux** is a powerful Terminal app for Android.  
It allows you to use your phone like a mini Linux system, run Git, GitHub, programming tools, etc.

---

## 2. Install Termux
- Do not download from Play Store (outdated version).  
- Download from the official release:  
  [Termux official GitHub](https://github.com/termux/termux-app/releases)

---

## 3. First Setup
Update & upgrade all packages:

```bash
pkg update && pkg upgrade -y
```
This updates package lists and upgrades installed packages.

---

## 4. Install Git
```bash
pkg install git -y
```
This installs Git.

```bash
git --version
```
Check if Git is installed.

---

## 5. Create a GitHub Account
Go to [https://github.com](https://github.com) and create a free account.

---

## 6. Configure Git (Name & Email)
```bash
git config --global user.name "Your Name"
```
Set your username.

```bash
git config --global user.email "your_email@example.com"
```
Set your email (use the same as GitHub).

```bash
git config --list
```
Check configurations.

---

## 7. Clone a Repository (Download Project)
```bash
git clone https://github.com/username/repo.git
```
This downloads a repository.

```bash
cd repo
```
Enter the project folder.

---

## 8. Upload Your Own Project to GitHub
```bash
mkdir myproject && cd myproject
```
Create a new folder.

```bash
echo "# My First Project" > README.md
```
Create a README file.

```bash
git init
```
Initialize Git inside the folder.

```bash
git add .
```
Add all files.

```bash
git commit -m "First commit"
```
Save changes.

```bash
git branch -M main
```
Rename branch to main.

```bash
git remote add origin https://github.com/username/myproject.git
```
Connect GitHub repo.

```bash
git push -u origin main
```
Upload to GitHub.

---

## 9. Personal Access Token (PAT)
GitHub no longer allows password for push. Use Token.

Path:  
`Settings → Developer settings → Personal access tokens → Tokens (classic)`

- Generate a new token (`repo` scope)  
- Copy the token  
- Use it instead of password when pushing

---

## 10. SSH Key Setup (Best for Auto Login)
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Generate SSH key.

```bash
cat ~/.ssh/id_rsa.pub
```
View the public key.

Add it to GitHub:  
`Settings → SSH and GPG Keys → New SSH key`

```bash
ssh -T git@github.com
```
Test SSH connection.

---

## 11. Credential Helper – Auto Login without Password
Save credentials so you don’t type them every time.

### (i) Permanent Save
```bash
git config --global credential.helper store
```
Credentials saved in `~/.git-credentials`.

### (ii) Temporary Cache
```bash
git config --global credential.helper 'cache --timeout=3600'
```
Credentials cached for 1 hour (3600 seconds).

---

## 12. GitHub CLI (gh) – Browser Style Login
### Install GitHub CLI
```bash
pkg install gh -y
```
Install GitHub CLI.

### Login
```bash
gh auth login
```
Login via browser link and code. After this, GitHub CLI commands work without asking credentials.

---

## 13. Upload File from Phone to GitHub
### Enable Storage Access
```bash
termux-setup-storage
```
Grant storage permission.

### Copy File
```bash
cp /storage/emulated/0/Download/test.txt ~/myproject/
```
Copy file into your project folder.

### Upload File
```bash
cd ~/myproject
git add test.txt
git commit -m "Added test.txt"
git push
```
File uploaded to GitHub.

---

## 14. Useful Termux Tools
```bash
pkg install nano -y
```
Install nano (text editor).

```bash
nano file.txt
```
Edit file inside Termux.

```bash
pkg install tree -y
```
Install tree to view folder structure.

```bash
tree
```
Show folder structure.

```bash
pkg install python -y
```
Install Python.

```bash
pkg install nodejs -y
```
Install Node.js.

```bash
pkg install zip unzip -y
```
Install zip/unzip.

---

## 15. Git Command Cheat Sheet
```bash
git status
```
Check file changes.

```bash
git add file
```
Add specific file.

```bash
git commit -m "Message"
```
Save changes.

```bash
git push
```
Upload to GitHub.

```bash
git pull
```
Get updates from GitHub.

```bash
git checkout -b branch
```
Create new branch.

```bash
git checkout main
```
Switch to main branch.

```bash
git merge branch
```
Merge branch into current.

```bash
git reset --soft HEAD~1
```
Undo last commit (keep changes).

---

## Conclusion
Now you know:  
- How to install Termux & Git  
- Configure Git & GitHub  
- Use Token, SSH, Credential Helper, and GitHub CLI  
- Upload files from phone to GitHub  
- Useful tools and commands  

You can now manage GitHub professionally from your phone.

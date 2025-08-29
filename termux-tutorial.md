# Termux Tutorial (Comprehensive Guide)

**Audience:** Beginners who want to understand Termux from A to Z.

**Scope:** This file explains how Termux works, how to use it effectively, and what you can do with it beyond the basic setup. If you haven’t set up Termux yet, see the [Basic Setup Guide](./termux-basic.md).

---

## Official Resources

- **GitHub Repository (source code):** <https://github.com/termux/termux-app>
- **GitHub Releases (APK downloads):** <https://github.com/termux/termux-app/releases>
- **F-Droid Download Page:** <https://f-droid.org/en/packages/com.termux/>
- **Documentation & Wiki:** <https://wiki.termux.com/>

---

## Introduction

Termux is a powerful Android application that provides:
1. A **terminal emulator** – a command-line interface where you type commands.
2. A **Linux environment** – where you can install packages, run code, and build projects.

With Termux, you can:
- Manage files and folders
- Install and use programming languages
- Connect to servers
- Run a local web server
- Use Git to manage projects
- Practice Linux skills directly on your phone

---

## The Shell Prompt

When you open Termux, you’ll see a shell prompt that looks like this:
```sh
$
```
This is where you type commands. For example:
```sh
echo "Hello Termux"
```
prints `Hello Termux` to the screen.

---

## File and Directory Management

Linux-style file and folder navigation works in Termux.

### Common Commands
- Show current location:
  ```sh
  pwd
  ```
- List files:
  ```sh
  ls
  ls -la   # include hidden files
  ```
- Create a new folder:
  ```sh
  mkdir projects
  ```
- Create a new file:
  ```sh
  touch notes.txt
  ```
- Enter a folder:
  ```sh
  cd projects
  ```
- Go back one level:
  ```sh
  cd ..
  ```
- Copy a file:
  ```sh
  cp notes.txt backup.txt
  ```
- Move/rename a file:
  ```sh
  mv notes.txt ideas.txt
  ```
- Delete a file or folder:
  ```sh
  rm ideas.txt
  rm -rf projects   # delete a folder recursively
  ```

> **Warning:** `rm` permanently deletes files. There is no recycle bin.

---

## Editing Files

Termux supports text editors like **nano** and **vim**.

- Open a file in nano:
  ```sh
  nano file.txt
  ```
- Save changes: `Ctrl + O`, then press `Enter`
- Exit nano: `Ctrl + X`

Nano is beginner-friendly; vim is more advanced.

---

## Package Management

Termux has its own package manager (`pkg`) to install and manage software.

- Update package list:
  ```sh
  pkg update
  ```
- Upgrade all installed packages:
  ```sh
  pkg upgrade
  ```
- Search for a package:
  ```sh
  pkg search python
  ```
- Install a package:
  ```sh
  pkg install python
  ```
- Uninstall a package:
  ```sh
  pkg uninstall python
  ```

---

## Networking Basics

- Test connectivity:
  ```sh
  ping google.com
  ```
- Download content:
  ```sh
  curl https://example.com
  wget https://example.com/file.zip
  ```
- Connect to a server via SSH:
  ```sh
  ssh user@server-ip
  ```

---

## Using Git

Git is widely used for version control. You can use it inside Termux.

- Install Git:
  ```sh
  pkg install git
  ```
- Clone a repository:
  ```sh
  git clone https://github.com/username/repo.git
  ```
- Check status:
  ```sh
  git status
  ```
- Stage changes:
  ```sh
  git add filename
  ```
- Commit changes:
  ```sh
  git commit -m "Your message"
  ```
- Push changes:
  ```sh
  git push origin main
  ```

---

## Running a Local Server

You can run a simple HTTP server using Python:
```sh
python -m http.server 8080
```
Now visit `http://localhost:8080` in your browser to view the contents of the folder.

---

## Useful Tips & Shortcuts

- **Volume Down = Ctrl** (e.g., `Volume Down + C` = Ctrl + C)
- **Volume Up + Q/K** = toggle extra keys row
- **termux-reload-settings** = reload Termux configuration
- Use `clear` to clear the screen
- Use `history` to see previously used commands
- Press `↑` (up arrow) to repeat the last command

---

## What You Can Do With Termux

- Learn and practice Linux commands
- Run programming languages (Python, Node.js, C, C++, Go, etc.)
- Host small local servers
- Manage GitHub repositories
- Automate tasks with shell scripts
- Experiment with network tools

---

## Conclusion

Termux turns your Android device into a portable Linux workstation. By learning the basics of file management, packages, networking, and version control, you can unlock a huge range of possibilities directly from your phone. Whether you are a beginner learning Linux or a developer managing code, Termux is a flexible tool to have at hand.

For setup instructions, see the [Basic Setup Guide](./termux-basic.md). For more details, explore the official [Termux Wiki](https://wiki.termux.com/).
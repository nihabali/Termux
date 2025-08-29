# Python Installation Guide (Termux A–Z)

## Introduction
Python is one of the most popular programming languages. By installing Python inside Termux, you can run scripts, start local servers, practice coding, or even do automation and data analysis directly on your Android device. This guide explains step-by-step how to install, update, and use Python in Termux.

---

## Installing Python

### Step 1: Update packages
```bash
pkg update && pkg upgrade
```
This ensures everything is up to date.

### Step 2: Install Python
```bash
pkg install python
```
This installs the latest **stable release** of Python available in Termux repositories.

> **Note:** Termux repositories are updated frequently. If you need the absolute latest release that is not yet available in Termux, you can compile it manually from source (explained below).

---

## Installing the Latest Python Manually (Advanced)

1. Install required dependencies:
   ```bash
   pkg install build-essential clang python git wget
   pkg install libffi-dev openssl-dev bzip2 libbz2 libsqlite liblzma
   ```

2. Download the latest source code from the official Python website:
   ```bash
   wget https://www.python.org/ftp/python/3.x.y/Python-3.x.y.tgz
   ```
   Replace `3.x.y` with the latest version number. See releases here: https://www.python.org/ftp/python/

3. Extract the archive:
   ```bash
   tar -xvzf Python-3.x.y.tgz
   cd Python-3.x.y
   ```

4. Configure and compile:
   ```bash
   ./configure
   make
   make install
   ```

This way you can run the absolute latest version of Python.

---

## Verifying Installation

Check Python version:
```bash
python --version
```
or
```bash
python3 --version
```

Check pip version (Python’s package manager):
```bash
pip --version
```

---

## Using Python

### Start Python shell
```bash
python
```
Example inside the shell:
```python
print("Hello Termux")
```
Exit with:
```python
exit()
```
or press `Ctrl + D`.

### Run a Python file
1. Create a file:
   ```bash
   nano hello.py
   ```
   Inside the file, write:
   ```python
   print("Hello, Termux Python!")
   ```
   Save and exit.

2. Run the file:
   ```bash
   python hello.py
   ```

---

## Package Management with pip

- Install a package:
  ```bash
  pip install requests
  ```
- Upgrade a package:
  ```bash
  pip install --upgrade requests
  ```
- Show installed packages:
  ```bash
  pip list
  ```

---

## Virtual Environments

To manage dependencies per project, use virtual environments.

Create and activate:
```bash
python -m venv myenv
source myenv/bin/activate
```

Now all packages will be installed inside `myenv`.

Deactivate with:
```bash
deactivate
```

---

## Conclusion

For most users, simply running `pkg install python` is enough to start using Python in Termux. This provides a stable, updated version. If you require the absolute latest release, you can compile it manually from source. With Python inside Termux, you can learn programming, run servers, and develop projects — all from your Android device.

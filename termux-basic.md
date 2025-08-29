# Termux Basic Setup (A–Z)

**Audience:** Absolute beginners.

**Scope:** This document covers *only* the initial, safe setup of Termux on Android—installation, first‑run configuration, storage access, essential commands, and a few quality‑of‑life tweaks. No advanced usage or programming stacks here.

---

## Official Links

- **Download (F‑Droid):** <https://f-droid.org/en/packages/com.termux/>
- **Download (GitHub Releases):** <https://github.com/termux/termux-app/releases>
- **Source code (GitHub):** <https://github.com/termux/termux-app>
- **Documentation & Wiki:** <https://wiki.termux.com/>

> **Note about Google Play:** Termux is visible on Google Play, but that build is maintained separately and has limitations. For most users, the recommended sources are **F‑Droid** or **GitHub Releases** (links above).

---

## Requirements & Recommendations

- **Android version:** Android 7.0 (Nougat) or newer is recommended for full package support.
- **One source only:** Install Termux **from a single source** (F‑Droid *or* GitHub). Do **not** mix sources or plugins signed by different keys. If you want to switch sources later, **uninstall** all Termux apps/plugins first, then reinstall from the new source.
- **Storage:** You can work entirely inside Termux without special permissions, but to access shared storage (Downloads, DCIM, etc.) you’ll enable it via a Termux command (explained below).

---

## Choose Your Installation Path

### Option 1 — F‑Droid (recommended for most users)
1. Open the F‑Droid Termux page: <https://f-droid.org/en/packages/com.termux/>.
2. Tap **Download APK** and install it.

### Option 2 — GitHub Releases (when you want the newest release)
1. Open releases: <https://github.com/termux/termux-app/releases>.
2. Download the latest **APK** (usually the universal build) and install it.

> **Don’t install plugins from a different source** than your base Termux app. Keep everything from the *same* source to avoid signature conflicts.

---

## First Run: Update the Base System

When you first open Termux you’ll see a shell prompt like `$`. Run these in order:

```sh
pkg update
```
**What it does:** Refreshes the package index (the list of what’s available). You’ll see how many packages can be upgraded.

```sh
pkg upgrade
```
**What it does:** Upgrades all installed packages to their latest versions. You may be asked to confirm; press `y` and Enter.

> **Tip:** `pkg` is a friendly wrapper around `apt`. You can usually prefer `pkg` for simplicity.

If you see repository errors like *“repository is under maintenance or down”*:

```sh
termux-change-repo
```
**What it does:** Opens a menu to switch to a working mirror. Select a nearby or recommended mirror for the **main** repository (and any others you use), then re‑run `pkg update`.

To inspect your current Termux environment (including active mirrors):

```sh
termux-info
```
**What it does:** Prints diagnostic information—useful when troubleshooting.

---

## Enable Access to Shared Storage

If you want Termux to see your device’s shared folders (Downloads, Pictures, etc.):

```sh
termux-setup-storage
```
**What it does:** Requests Android permission and creates the directory `~/storage` containing symlinks to common shared folders:

- `~/storage/downloads` → your Downloads
- `~/storage/shared` → top‑level shared storage
- `~/storage/dcim`, `~/storage/pictures`, `~/storage/music`, `~/storage/movies`
- `~/storage/external-1` (if an SD card or USB drive is present)

> **Important:** Executing programs directly from shared storage is restricted by Android. Keep scripts and executables under your Termux **home** directory (explained next).

---

## Know Your Folders

- **Home directory (`$HOME`):** `/data/data/com.termux/files/home`  
  Your personal workspace. Put projects, scripts, and config files here.

- **Prefix (`$PREFIX`):** `/data/data/com.termux/files/usr`  
  Installed packages live here. Don’t edit files here unless you know what you’re doing.

Quick checks:

```sh
echo $HOME
echo $PREFIX
pwd        # shows your current directory
ls -la     # list files (including hidden ones)
```

---

## Essential Packages (optional but helpful)

Install a few basics to make life easier:

```sh
pkg install nano less curl
```
**What they do:**
- `nano` — beginner‑friendly text editor (open a file: `nano filename`; save: `Ctrl+O`, exit: `Ctrl+X`).
- `less` — handy pager for reading long outputs (`command | less`; quit with `q`).
- `curl` — download or fetch URLs (`curl -I https://example.com`).

Searching and installing packages:

```sh
pkg search <name>
pkg install <package>
pkg list-all | less
```
**What they do:**
- `pkg search` — find packages by name/description.
- `pkg install` — install a package.
- `pkg list-all` — list everything available; pipe to `less` to scroll.

Cleaning up cached package files:

```sh
apt clean
```
**What it does:** Frees space by clearing downloaded package archives.

---

## Basic Shell Navigation

```sh
ls           # list files
ls -la       # long listing including hidden files
pwd          # print current directory
cd           # go to your home directory
cd <folder>  # change into a folder
mkdir <dir>  # create a directory
cp A B       # copy A to B
mv A B       # move/rename A to B
rm <file>    # remove file (careful!)
```

> **Caution:** `rm` permanently deletes. There is no recycle bin.

---

## Add an “Extra Keys” Row (Quality of Life)

Touch keyboards lack keys like Esc, Tab, Ctrl. Termux provides a configurable extra key row.

1. Create the config folder (if it doesn’t exist):
   ```sh
   mkdir -p ~/.termux
   ```
2. Open the properties file:
   ```sh
   nano ~/.termux/termux.properties
   ```
3. Add this two‑row layout (paste exactly):
   ```
   extra-keys = [['ESC','/','-','HOME','UP','END','PGUP'],['TAB','CTRL','ALT','LEFT','DOWN','RIGHT','PGDN']]
   ```
4. Reload settings:
   ```sh
   termux-reload-settings
   ```

**Helpful hardware key combos:**
- **Volume Down** acts as **Ctrl**. Example: Volume‑Down + `L` ⇢ clear screen.
- **Volume Up + Q/K** toggles the extra keys view.
- **Volume Up + E** ⇢ Esc, **Volume Up + T** ⇢ Tab, **Volume Up + 1..0** ⇢ F1..F10.

---

## Troubleshooting

- **Repository errors (maintenance/down):** Run `termux-change-repo` and select another mirror, then `pkg update`.
- **“App not installed” when switching sources:** Uninstall all Termux apps/plugins first, then install everything from the new source (don’t mix F‑Droid and GitHub builds).
- **Storage not visible:** Re‑run `termux-setup-storage` and grant permission. Your shared folders should appear under `~/storage/`.

---

## Quick Reference (cheat sheet)

| Task | Command |
|---|---|
| Refresh package list | `pkg update` |
| Upgrade installed packages | `pkg upgrade` |
| Search for a package | `pkg search <name>` |
| Install a package | `pkg install <package>` |
| Change package mirror | `termux-change-repo` |
| Show environment info | `termux-info` |
| Enable shared storage | `termux-setup-storage` |
| Reload Termux settings | `termux-reload-settings` |

---

## What’s Next

This file intentionally covers *only* the basic setup. For hands‑on usage, scripting, editors, SSH, and more, you can create a separate tutorial file (e.g., `termux-tutorial.md`) and build from here using the Wiki as your primary reference: <https://wiki.termux.com/>.

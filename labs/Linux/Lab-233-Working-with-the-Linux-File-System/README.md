# 🐧 Lab 05 — Working with the Linux File System (Lab 233)

> **Domain:** Linux | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Navigate and manage the Linux file system using the command line. Covers directory structure, file operations, permissions, and essential Linux commands used daily in cloud engineering roles.

---

## 📚 What I Did

Completed 3 main tasks with 19 steps total, including a final submission report.

### Task 1 — File System Navigation
- Explored the Linux directory tree (`/`, `/home`, `/etc`, `/var`, `/tmp`)
- Used `pwd`, `ls`, `cd` to navigate
- Understood absolute vs relative paths

### Task 2 — File & Directory Operations
- Created, moved, copied, and deleted files and directories
- Used `mkdir`, `touch`, `cp`, `mv`, `rm`, `rmdir`
- Explored `cat`, `less`, `head`, `tail` for reading file contents

### Task 3 — Permissions & Ownership
- Read and interpreted permission strings (`rwxr-xr--`)
- Changed permissions with `chmod`
- Changed ownership with `chown`
- Understood user, group, and other permission categories

---

## 🧠 Key Concepts Covered

### Linux Directory Structure
```
/                   Root of the file system
├── home/           User home directories
├── etc/            Configuration files
├── var/            Variable data (logs, databases)
├── tmp/            Temporary files (cleared on reboot)
├── usr/            User programs and utilities
├── bin/            Essential command binaries
└── proc/           Virtual filesystem for system info
```

### Essential Commands
```bash
# Navigation
pwd                 # Print working directory
ls -la              # List all files with details
cd /path/to/dir     # Change directory
cd ..               # Go up one level

# File operations
touch file.txt      # Create empty file
mkdir -p dir/sub    # Create directory (and parents)
cp source dest      # Copy file
mv source dest      # Move / rename file
rm -rf dir/         # Remove directory recursively

# Reading files
cat file.txt        # Print entire file
less file.txt       # Scroll through file
head -n 10 file.txt # First 10 lines
tail -n 10 file.txt # Last 10 lines
grep "word" file    # Search for pattern
```

### Linux Permissions
```
-rwxr-xr--   1   tumelo   group   1024   Apr 7   file.txt
 │││││││││
 │││││││└└─ Other: read only (r--)
 ││││└└└─── Group: read + execute (r-x)
 │└└└─────── Owner: read + write + execute (rwx)
 └─────────── File type (- = file, d = directory)
```

```bash
chmod 755 script.sh     # rwxr-xr-x
chmod 644 config.txt    # rw-r--r--
chmod +x script.sh      # Add execute permission
chown tumelo:group file # Change owner and group
```

---

## 💡 Key Takeaways

1. **Everything in Linux is a file** — devices, processes, sockets — it's files all the way down.
2. **Permissions control everything** — a misconfigured permission is the #1 cause of "permission denied" errors.
3. **`-la` is your best friend** — `ls -la` shows hidden files, permissions, sizes, and owners at once.
4. **Absolute paths are safer in scripts** — relative paths break when scripts run from different directories.
5. **`man` is built-in documentation** — `man chmod` gives you the full manual for any command.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)

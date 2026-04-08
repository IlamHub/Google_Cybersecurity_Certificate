# Lab: Manage Files with Linux Commands

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47125035?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Starting Directory: `/home/analyst`
- Privileges: Standard user

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Keeping a well-organized directory structure makes it easier to detect anomalies and locate evidence quickly.
- Creating, moving, and deleting files are routine tasks during log management and incident documentation.
- Editing files directly in the terminal (without a GUI) is an essential skill when working on remote servers.

---

## Directory Structure Overview

### Before:

```
home
└── analyst
    ├── notes
    │   ├── Q3patches.txt
    │   └── tempnotes.txt
    ├── reports
    │   ├── Q1patches.txt
    │   └── Q2patches.txt
    └── temp
```

### After:

```
home
└── analyst
    ├── logs
    ├── notes
    │   └── tasks.txt
    └── reports
        ├── Q1patches.txt
        ├── Q2patches.txt
        └── Q3patches.txt
```

---

## Task 1: Create a New Directory

Create a dedicated `logs` subdirectory to store future log files.

```bash
mkdir logs
```

Verify it was created:

```bash
ls
```

**Expected Output:**

```
logs  notes  reports  temp
```

---

## Task 2: Remove a Directory

Remove the `temp` directory since it is no longer needed.

```bash
rmdir temp
```

Verify it was removed:

```bash
ls
```

**Expected Output:**

```
logs  notes  reports
```

> **Note:** `rmdir` only removes empty directories. If the directory contains files, you would need to use `rm -r` instead.

---

## Task 3: Move a File

Move `Q3patches.txt` from the `notes` directory to the `reports` directory.

### Navigate to `notes`

```bash
cd /home/analyst/notes
```

### Move the File

```bash
mv Q3patches.txt /home/analyst/reports/
```

### Verify the Move

```bash
ls /home/analyst/reports
```

**Expected Output:**

```
Q1patches.txt  Q2patches.txt  Q3patches.txt
```

> **Note:** `mv` can also be used to rename a file by specifying a new filename as the destination instead of a directory path.

---

## Task 4: Remove a File

Delete the unused `tempnotes.txt` file from the `notes` directory.

```bash
rm tempnotes.txt
```

Verify it was removed:

```bash
ls
```

**Expected Output:**

```
(no files listed)
```

---

## Task 5: Create a New File

Create an empty `tasks.txt` file in the `notes` directory to document completed tasks.

```bash
touch tasks.txt
```

Verify it was created:

```bash
ls
```

**Expected Output:**

```
tasks.txt
```

---

## Task 6: Edit a File

Open `tasks.txt` in the nano text editor and add task notes.

### Open the File

```bash
nano tasks.txt
```

### Add the Following Text

```
Completed tasks
1. Managed file structure in /home/analyst
```

### Save and Exit

1. Press `CTRL+X` to exit
2. Press `Y` to confirm saving
3. Press `ENTER` to confirm the filename

### Clear the Shell

```bash
clear
```

### Verify the File Contents

```bash
cat tasks.txt
```

**Expected Output:**

```
Completed tasks
1. Managed file structure in /home/analyst
```

> **Note:** The standard save sequence in nano is `CTRL+O` to save, then `CTRL+X` to exit. In browser-based lab environments, `CTRL+O` is intercepted by the browser, so the `CTRL+X` → `Y` → `ENTER` sequence is used instead.

# Lab: Manage Authorization

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47125083?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `researcher2`
- Group: `research_team`
- Starting Directory: `/home/researcher2`
- Privileges: Standard user

---

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Misconfigured file permissions are a common security vulnerability — they can allow unauthorized users to read, modify, or execute sensitive files.
- Auditing and correcting permissions is a routine hardening task that prevents privilege escalation and data leakage.
- The principle of least privilege means users and groups should only have the minimum access they need to do their job.

---

## Permission String Reference

Every file and directory has a 10-character permission string. For example:

```
drwxrwxrwx
```

| Position | Characters     | Meaning                                 |
| -------- | -------------- | --------------------------------------- |
| 1        | `d` or `-` | `d` = directory, `-` = regular file |
| 2-4      | `rwx`        | User (owner) permissions                |
| 5-7      | `rwx`        | Group permissions                       |
| 8-10     | `rwx`        | Other (everyone else) permissions       |

Each permission slot uses `r` (read), `w` (write), `x` (execute), or `-` (not granted).

---

## Task 1: Check File and Directory Details

### Navigate to the `projects` Directory

```bash
cd projects
```

### List Files with Permissions

```bash
ls -l
```

**Expected Output:**

```
drwx--x--- 2 researcher2 research_team 4096 ... drafts
-rw-rw-rw- 1 researcher2 research_team   46 ... project_k.txt
-rw-r----- 1 researcher2 research_team   46 ... project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 ... project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 ... project_t.txt
```

> **Q:** What group owns the files in the `projects` directory?
> **A:** `research_team`

### Check for Hidden Files

```bash
ls -la
```

> **Note:** The `-a` flag includes hidden files in the output. Hidden files in Linux start with a period (`.`).

> **Q:** Which file is hidden in the `projects` directory?
> **A:** `.project_x.txt`

---

## Task 2: Change File Permissions

### Rule: No file should allow "other" users to write.

Check current permissions:

```bash
ls -l
```

> **Q:** Which file grants write permissions to other users?
> **A:** `project_k.txt` (permission string: `-rw-rw-rw-`)

### Remove Write Permission for "Other" on `project_k.txt`

```bash
chmod o-w project_k.txt
```

---

### Rule: `project_m.txt` should only be readable/writable by the user — not the group or other.

Check current group permissions on `project_m.txt`:

> **Q:** What are the group permissions on `project_m.txt`?
> **A:** Read only (`r--`)

### Remove Group Read Permission on `project_m.txt`

```bash
chmod g-r project_m.txt
```

> **Note:** In `chmod`, permission targets are:
>
> - `u` = user (owner)
> - `g` = group
> - `o` = other
>
> Use `+` to add and `-` to remove permissions. For example: `chmod o-w file.txt`

---

## Task 3: Change File Permissions on a Hidden File

### Rule: `.project_x.txt` is archived — no one should be able to write to it, but both user and group can still read it.

Check hidden file permissions:

```bash
ls -la
```

> **Q:** Which owner types have incorrect write permissions on `.project_x.txt`?
> **A:** Both the user and the group have write permissions (should not).

### Remove Write from User and Group, Ensure Group Can Read

```bash
chmod u-w,g-w,g+r .project_x.txt
```

> **Note:** Multiple permission changes can be chained with a comma in a single `chmod` command.
> Always include the leading `.` when referencing hidden files.

---

## Task 4: Change Directory Permissions

### Rule: Only `researcher2` should be able to access the `drafts` directory — no group access.

Check current permissions on `drafts`:

```bash
ls -l
```

> **Q:** Does the group have execute permissions on the `drafts` directory?
> **A:** Yes — the group currently has execute (`x`) access, which allows them to enter the directory.

### Remove Group Execute Permission from `drafts`

```bash
chmod g-x drafts
```

> **Note:** Execute permission on a directory controls the ability to enter it and access its contents — not just run scripts. Removing `x` from a directory effectively locks out that owner type entirely.

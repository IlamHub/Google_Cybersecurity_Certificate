# Lab: Find Files with Linux Commands

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47124875?parent=lti_session

## Objective

Use Linux commands to manage file permissions and ownership.

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Starting Directory: `/home/analyst`
- Privileges: Standard user

## Why This Matters (Cybersecurity Context)

In a real **SOC (Security Operations Center)** environment:

- Investigating **unauthorized access** often means navigating to and reading user access reports stored on remote servers.
- You'll rarely have a graphical interface — the shell is your primary tool.
- Knowing how to quickly locate and read files is critical during active incident response.

---

## Task 1: Get the Current Directory Information

### Display Your Working Directory

```bash
pwd
```

**Expected Output:**

```
/home/analyst
```

### List Contents of the Current Directory

```bash
ls
```

**Expected Output:**

```
logs  projects  reports  temp
```

> ** Q:** How many directories does the current working directory contain?
> ** A:** Four — `logs`, `projects`, `reports`, and `temp`.

---

## Task 2: Change Directory and List Subdirectories

### Navigate to the `reports` Directory

Using a **relative path:**

```bash
cd reports
```

Using an **absolute path:**

```bash
cd /home/analyst/reports
```

> **Note:** A **relative path** starts from your current location (no leading `/`). An **absolute path** starts from the root of the filesystem (begins with `/`).

### List Contents of `reports`

```bash
ls
```

**Expected Output:**

```
users
```

> ** Q:** What is the name of the subdirectory in `/home/analyst/reports`?
> **A:** `users`

---

## Task 3: Locate and Read the Contents of a File

### Navigate to the `users` Subdirectory

```bash
cd /home/analyst/reports/users
```

Or using a relative path (if already inside `reports`):

```bash
cd users
```

### List Files in the Directory

```bash
ls
```

### Display the Contents of `Q1_added_users.txt`

```bash
cat Q1_added_users.txt
```

Or using an absolute path:

```bash
cat /home/analyst/reports/users/Q1_added_users.txt
```

> **Note:** `cat` prints the full contents of a file directly to the shell.

> ** Q:** What department does the employee with username `aezra` work in?
> **A:** Human Resources

> ** Q:** What is the `employee_id` of `mreed` in the Information Technology department?
> **A:** `1104`

---

## Task 4: Navigate to a Directory and Locate a File

### Navigate to the `logs` Directory

```bash
cd /home/analyst/logs
```

### List Files in the Directory

```bash
ls
```

**Expected Output:**

```
server_logs.txt
```

### Display the First 10 Lines of the Log File

```bash
head server_logs.txt
```

> **Note:** `head` displays the first 10 lines of a file by default. To specify a custom number of lines, use the `-n` flag:
>
> ```bash
> head -n 20 server_logs.txt
> ```

> ** Q:** How many warning messages are in the first 10 lines of `server_logs.txt`?
> ** A:** 3

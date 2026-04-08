# Lab: Filter with grep

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47124987?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Starting Directory: `/home/analyst`
- Privileges: Standard user

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Log files can contain thousands of lines — manually scanning them is not practical.
- `grep` lets you instantly filter for errors, suspicious usernames, or specific events.
- Piping commands together allows you to build powerful, efficient one-liners for incident response and user auditing.

---

## Task 1: Search for Error Messages in a Log File

### Navigate to the `logs` Directory

```bash
cd logs
```

### Filter `server_logs.txt` for Error Entries

```bash
grep error server_logs.txt
```

> **Note:** The first argument passed to `grep` is the string you're searching for. The second argument is the file to search through.
> If a command hangs, press `CTRL+C` to force the shell back to the prompt.

> **Q:** How many error lines are there in `server_logs.txt`?
> **A:** Six

---

## Task 2: Find Files Containing Specific Strings

### Navigate to the `users` Directory

```bash
cd /home/analyst/reports/users
```

### List Only Files Containing "Q1" in Their Names

```bash
ls | grep Q1
```

> **Note:** The pipe character `|` sends the output of one command into another as input. Here, `ls` lists all files, and `grep` filters that list to only show matches.

> **Q:** How many files contain "Q1" in their names?
> **A:** Three

### List Only Files Containing "access" in Their Names

```bash
ls | grep access
```

> **Q:** How many files contain "access" in their names?
> **A:** Four

---

## Task 3: Search More File Contents

### List Files in the Current Directory

```bash
ls
```

### Search for a Specific Username in a File

```bash
grep jhill Q2_deleted_users.txt
```

> **Q:** Is the username `jhill` listed in `Q2_deleted_users.txt`?
> **A:** Yes

### Search for Users Added to a Specific Department

```bash
grep "Human Resources" Q4_added_users.txt
```

> **Note:** When searching for a string that contains spaces, wrap it in quotes so `grep` treats it as a single argument.

> **Q:** How many users were added to the Human Resources department in Q4?
> **A:** Two

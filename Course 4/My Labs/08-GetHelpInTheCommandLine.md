# Lab: Get Help in the Command Line

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47128654?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Starting Directory: `/home/analyst`
- Privileges: Standard user

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- You won't always remember every command or option — knowing how to look things up quickly is just as important as memorizing them.
- The built-in Linux help system lets you work efficiently on remote servers without needing internet access or external documentation.
- Discovering the right command for a task using `apropos` is a practical skill when dealing with unfamiliar systems during an investigation.

---

## Task 1: Learn More About Commands

### Get a Quick Description of a Command

```bash
whatis cat
```

**Expected Output:**

```
cat (1) - concatenate files and print on the standard output
```

> **Q:** What are the first two words of the description returned by `whatis cat`?
> **A:** "concatenate files"

---

### Get the Full Manual for a Command

```bash
man cat
```

> Navigate the manual page:
>
> - Press `ENTER` to scroll one line at a time
> - Press `SPACE` to jump to the next page
> - Press `Q` to exit

> **Q:** Which option numbers all output lines of the `cat` command?
> **A:** `-n, --number`

---

### Search for a Command by Keyword

```bash
apropos -a first part file
```

> **Note:** The `-a` flag requires all keywords to match, narrowing the results. If the first search does not return what you need, try adjusting your keywords.

> **Q:** Which command returns the first part of a file?
> **A:** `head`

---

## Task 2: Explore the `useradd` Command

You need to set an expiration date for a temporary user account but are unsure which option to use.

```bash
man useradd
```

> Scroll through the manual to find the option related to expiration dates.

> **Q:** Which option sets an expiration date for a temporary user account?
> **A:** `-e`

---

## Task 3: Explore the `rm` and `rmdir` Commands

You need to quickly remind yourself of the difference between these two commands.

```bash
whatis rm
whatis rmdir
```

> **Q:** Which command removes only empty directories?
> **A:** `rmdir`

> **Note:** `rm` removes files and can remove directories with the `-r` flag regardless of contents. `rmdir` will only succeed on an empty directory.

---

## Task 4: Determine Which Command to Use

You need to create a new group but cannot remember the command. Search using keywords:

```bash
apropos -a create new group
```

> **Q:** Which command creates a new group?
> **A:** `groupadd`

# Lab: Examine Input/Output in the Linux Shell

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47124804?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Privileges: Standard user (no `sudo` needed for this lab)

## Why This Matters (Cybersecurity Context)

In a real **SOC (Security Operations Center)** environment:

- You'll constantly input commands into the shell and need to interpret the output.
- Quick math (e.g., counting false positives, calculating login attempt rates) is part of daily analysis.
- Keeping a clean shell environment helps you stay focused during incident response.

---

## Task 1: Generate Output with `echo`

The `echo` command outputs a specified string of text to the shell.

### Basic Output

```bash
echo hello
```

**Expected Output:**

```
hello
```

### With Quotation Marks

```bash
echo "hello"
```

**Expected Output:**

```
hello
```

> **Note:** The output is identical. Quotes are optional here, but they group characters together — useful when your string contains special characters that the shell might otherwise misinterpret.

### Output Your Name

```bash
echo "Your Name"
```

**Expected Output:**

```
Your Name
```

---

## Task 2: Generate Output with `expr`

The `expr` command performs basic mathematical calculations directly in the shell — handy for quick on-the-fly analysis.

> **Important:** All terms and operators **must** be separated by spaces.
> `expr 32 - 8` — correct
> `expr 32-8` — incorrect

### Calculate False Positives

You have **32 total alerts**, but only **8 required action**. How many are false positives?

```bash
expr 32 - 8
```

**Expected Output:**

```
24
```

### Calculate Annual Login Attempts

An average of **3500 login attempts** are made per month. How many are expected in a year?

```bash
expr 3500 * 12
```

**Expected Output:**

```
42000
```

---

## Task 3: Clear the Bash Shell

When your screen fills with previous commands and output, use `clear` to reset the view.

```bash
clear
```

> All previous input and output will be wiped, and the cursor returns to the top-left of the shell window — giving you a clean slate to work from.

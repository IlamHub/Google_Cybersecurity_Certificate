# Lab: Managing File Permissions in Linux

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47124098?parent=lti_session

## Objective

Use Linux commands to manage file permissions and ownership.

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Privileges: `sudo` access available

## Why This Matters (Cybersecurity Context)

In a real **SOC (Security Operations Center)** environment:

- You may need to quickly install tools like Suricata to detect attacks.
- You may use tcpdump to capture suspicious traffic for analysis.
- Managing tools efficiently is critical during incident response.

---

## Task 1: Ensure APT is Installed

### Command:

```bash
apt
```

**Expected Output:**

> Displays APT version and usage info.

**Verification:**
APT is installed if you see help/usage information.

---

## Task 2: Install and Uninstall Suricata

### Install Suricata

```bash
sudo apt install suricata
```

> Press `ENTER` to confirm installation.

### Verify Installation

```bash
suricata
```

**Expected Output:**

> Displays version and usage info.

### Uninstall Suricata

```bash
sudo apt remove suricata
```

> Press `ENTER` to confirm.

### Verify Removal

```bash
suricata
```

**Expected Output:**

```
-bash: /usr/bin/suricata: No such file or directory
```

---

## Task 3: Install tcpdump

### Command:

```bash
sudo apt install tcpdump
```

**Purpose:**

> Captures and analyzes network traffic — used heavily in incident response.

---

## Task 4: List Installed Applications

### Command:

```bash
apt list --installed
```

### What to Look For:

Search for:

```
tcpdump
```

**Example Output:**

```
tcpdump/... [installed]
```

---

## Task 5: Reinstall Suricata

### Reinstall:

```bash
sudo apt install suricata
```

> Press `ENTER` to confirm.

### Verify Installation Again:

```bash
apt list --installed
```

**Expected Output:**

```
suricata/... [installed]
tcpdump/... [installed]
```

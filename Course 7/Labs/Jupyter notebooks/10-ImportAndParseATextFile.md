# Activity: Import and Parse a Text File

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Import and Parse a Text File
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

Security logs are often stored in text files. To analyze them, security analysts must import and parse these files. Python provides built-in functions that make this process efficient — allowing analysts to read, write, and append to text files with minimal code.

In this lab, Python file handling is practiced in the context of reading a security login log and creating an IP address allow list file.

---

## Scenario

Two file-handling tasks are completed in this lab:

1. Importing and parsing an existing security log file (`login.txt`), including appending a missing log entry.
2. Creating a new text file (`allow_list.txt`) containing IP addresses approved to access restricted information.

---

## Task 1 — Opening a File with a `with` Statement

**Code:**

```python
# Assign `import_file` to the name of the text file that contains the security log file

import_file = "login.txt"

# First line of the `with` statement
# Use `open()` to import security log file and store it as a string

with open(import_file, "r") as file:
```

**Output:**

```
(error — the with statement body is empty at this stage)
```

The `with` statement is used for file handling in Python. It automatically closes the file once the indented block finishes executing — even if an error occurs. The `open()` function takes two arguments: the filename and the mode. `"r"` means the file is opened for **reading**. The `as file` part assigns the file object to the variable `file` for use inside the block.

---

## Task 2 — Reading the File with `.read()`

**Code:**

```python
import_file = "login.txt"

with open(import_file, "r") as file:

    # Use `.read()` to read the imported file and store the result in a variable named `text`

    text = file.read()

# Display the contents of `text`

print(text)
```

**Output:**

```
username,ip_address,time,date
tshah,192.168.92.147,15:26:08,2022-05-10
dtanaka,192.168.98.221,9:45:18,2022-05-09
tmitchel,192.168.110.131,14:13:41,2022-05-11
daquino,192.168.168.144,7:02:35,2022-05-08
eraab,192.168.170.243,1:45:14,2022-05-11
jlansky,192.168.238.42,1:07:11,2022-05-11
acook,192.168.52.90,9:56:48,2022-05-10
asundara,192.168.58.217,23:17:52,2022-05-12
jclark,192.168.214.49,20:49:00,2022-05-10
cjackson,192.168.247.153,19:36:42,2022-05-12
jclark,192.168.197.247,14:11:04,2022-05-12
apatel,192.168.46.207,17:39:42,2022-05-10
mabadi,192.168.96.244,10:24:43,2022-05-12
iuduike,192.168.131.147,17:50:00,2022-05-11
abellmas,192.168.60.111,13:37:05,2022-05-10
gesparza,192.168.148.80,6:30:14,2022-05-11
cgriffin,192.168.4.157,23:04:05,2022-05-09
alevitsk,192.168.210.228,8:10:43,2022-05-08
eraab,192.168.24.12,11:29:27,2022-05-11
jsoto,192.168.25.60,5:09:21,2022-05-09
```

The `.read()` method reads the entire file and returns it as a single string. The result is stored in `text` and then printed. The log contains columns for username, IP address, time, and date — one login entry per line.

---

## Task 3 — Splitting the File Content into Lines with `.split()`

**Code:**

```python
import_file = "login.txt"

with open(import_file, "r") as file:
    text = file.read()

# Display the contents of `text` split into separate lines

print(text.split())
```

**Output:**

```
['username,ip_address,time,date', 'tshah,192.168.92.147,15:26:08,2022-05-10', 'dtanaka,192.168.98.221,9:45:18,2022-05-09', 'tmitchel,192.168.110.131,14:13:41,2022-05-11', ...]
```

**Question 1 — What do you notice about the output before and after using `.split()`?**

Before `.split()`, the entire file is one large string with newline characters (`\n`) separating each line. After calling `.split()`, Python breaks the string at every whitespace (including newlines) and returns a **list of strings** — one element per log entry. This makes each individual record far easier to process programmatically, such as iterating through entries or checking specific fields. Note that `.split()` does not modify the `text` variable itself — it only changes what is displayed.

---

## Task 4 — Appending a Missing Log Entry with `"a"` Mode

**Code:**

```python
import_file = "login.txt"

missing_entry = "jrafael,192.168.243.140,4:56:27,2022-05-09"

# Open the file in append mode and write the missing entry

with open(import_file, "a") as file:
    file.write("\n" + missing_entry)

# Read and display the updated file

with open(import_file, "r") as file:
    text = file.read()

print(text)
```

**Output:**

```
username,ip_address,time,date
tshah,192.168.92.147,15:26:08,2022-05-10
...
jsoto,192.168.25.60,5:09:21,2022-05-09
jrafael,192.168.243.140,4:56:27,2022-05-09
```

**Question 2 — What do you notice about the position of the entry that was added?**

The missing entry `"jrafael,192.168.243.140,4:56:27,2022-05-09"` appears at the very end of the file. This is expected behavior — the `"a"` (append) mode positions the write cursor at the **end of the existing file content**, so new data is always added after whatever is already there. This is different from `"w"` (write) mode, which would overwrite the entire file. Using `"a"` is the correct choice when adding entries to an existing log without losing prior data.

> **Note:** A `"\n"` is prepended to the missing entry to ensure it starts on a new line rather than being concatenated directly to the last line of the file.

---

## Task 5 — Setting Up the Allow List File

**Code:**

```python
# Assign `import_file` to the name of the text file that you want to create

import_file = "allow_list.txt"

# Assign `ip_addresses` to a list of IP addresses that are allowed to access the restricted information

ip_addresses = "192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246"

# Display both variables

print(import_file)
print(ip_addresses)
```

**Output:**

```
allow_list.txt
192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246
```

The target filename is `"allow_list.txt"` and the content to be written is a space-separated string of 11 approved IP addresses. This file will serve as documentation of which IPs are permitted to access restricted systems.

---

## Task 6 — Writing the IP Addresses to a New File with `"w"` Mode

**Code:**

```python
import_file = "allow_list.txt"

ip_addresses = "192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246"

# Create a `with` statement to write to the text file

with open(import_file, "w") as file:

    # Write `ip_addresses` to the text file

    file.write(ip_addresses)
```

**Output:**

```
(no output — the file is written silently)
```

Opening a file with `"w"` mode creates the file if it doesn't exist, or **overwrites** it entirely if it does. The `.write()` method writes the string stored in `ip_addresses` directly to the file. Since this is a new file, no prior content is lost. This mode is appropriate when creating a fresh document from scratch.

---

## Task 7 — Reading Back the Written File to Verify

**Code:**

```python
import_file = "allow_list.txt"

ip_addresses = "192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246"

# Write to the file

with open(import_file, "w") as file:
    file.write(ip_addresses)

# Read the file back and store in `text`

with open(import_file, "r") as file:
    text = file.read()

# Display the contents of `text`

print(text)
```

**Output:**

```
192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246
```

The content written to `allow_list.txt` is confirmed by reading it back and printing it. The output exactly matches the `ip_addresses` string that was written. This read-after-write pattern is a good practice to verify that file operations completed as expected.

---

## File Contents Reset

The following code resets `login.txt` to its original state. This is useful if the lab needs to be repeated or if the file was accidentally modified.

```python
login_file = """username,ip_address,time,date
tshah,192.168.92.147,15:26:08,2022-05-10
dtanaka,192.168.98.221,9:45:18,2022-05-09
tmitchel,192.168.110.131,14:13:41,2022-05-11
daquino,192.168.168.144,7:02:35,2022-05-08
eraab,192.168.170.243,1:45:14,2022-05-11
jlansky,192.168.238.42,1:07:11,2022-05-11
acook,192.168.52.90,9:56:48,2022-05-10
asundara,192.168.58.217,23:17:52,2022-05-12
jclark,192.168.214.49,20:49:00,2022-05-10
cjackson,192.168.247.153,19:36:42,2022-05-12
jclark,192.168.197.247,14:11:04,2022-05-12
apatel,192.168.46.207,17:39:42,2022-05-10
mabadi,192.168.96.244,10:24:43,2022-05-12
iuduike,192.168.131.147,17:50:00,2022-05-11
abellmas,192.168.60.111,13:37:05,2022-05-10
gesparza,192.168.148.80,6:30:14,2022-05-11
cgriffin,192.168.4.157,23:04:05,2022-05-09
alevitsk,192.168.210.228,8:10:43,2022-05-08
eraab,192.168.24.12,11:29:27,2022-05-11
jsoto,192.168.25.60,5:09:21,2022-05-09
"""

with open("login.txt", "w") as file:
    file.write(login_file)
```

---

## Conclusion

**Key takeaways from this lab:**

- The **`with` statement** is the standard way to handle files in Python — it automatically closes the file when the block ends, preventing resource leaks even if an error occurs.
- **`open(filename, "r")`** opens a file for reading; **`"w"`** opens for writing (creates or overwrites); **`"a"`** opens for appending (adds to the end without overwriting).
- The **`.read()` method** reads the entire file content and returns it as a single string.
- The **`.write()` method** writes a string to the open file — what gets written depends on the mode used to open the file.
- The **`.split()` method** converts a multi-line string into a list of individual strings — making log entries easier to process one at a time.
- Always use **append mode `"a"`** when adding to an existing log file to avoid overwriting historical records — a critical practice in security logging.
- A **read-after-write** pattern (write then immediately read back) is useful for confirming that file operations completed correctly.

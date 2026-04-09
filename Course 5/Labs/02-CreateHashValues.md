# Create Hash Values

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47139394?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Starting Directory: `/home/analyst`
- Privileges: Standard user

---

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Hash functions are used to verify the integrity of files — if even a single byte changes, the hash changes completely.
- Malware authors often disguise malicious programs as legitimate ones. Comparing hash values lets you detect tampering even when two files look visually identical.
- Tools like `sha256sum` are standard in file integrity monitoring, malware analysis, and incident response workflows.

---

## Background: Hash Functions

A hash function takes any input and produces a fixed-length string called a hash value (or digest). Key properties:

- The same input always produces the same hash.
- A tiny change in the input produces a completely different hash.
- Hash values cannot be reversed to recover the original data.

SHA-256 is a widely used hashing algorithm that produces a 256-bit (64 character) hash value.

---

## Task 1: Generate Hashes for Files

### List the Home Directory

```bash
ls
```

**Expected Output:**

```
file1.txt  file2.txt
```

### Display the Contents of Both Files

```bash
cat file1.txt
cat file2.txt
```

**Expected Output (both files):**

```
X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*
```

> **Q:** Do the contents of the two files appear identical?
> **A:** Yes — they look the same to the naked eye.

---

### Generate the SHA-256 Hash for Each File

```bash
sha256sum file1.txt
sha256sum file2.txt
```

**Expected Output:**

```
131f95c51cc819465fa1797f6ccacf9d494aaaff46fa3eac73ae63ffbdfd8267  file1.txt
2558ba9a4cad1e69804ce03aa2a029526179a91a5e38cb723320e83af9ca017b  file2.txt
```

> **Q:** Do both files produce the same hash value?
> **A:** No — the hashes are completely different, which means the file contents are not identical despite appearing so in `cat`.

> **Note:** This is a key security insight. Visual inspection is not reliable for detecting tampering — hash comparison is.

---

## Task 2: Compare Hashes

### Write Each Hash to a Separate File

```bash
sha256sum file1.txt >> file1hash
sha256sum file2.txt >> file2hash
```

> **Note:** The `>>` operator appends output to a file. If the file does not exist, it is created automatically.

### Display the Stored Hashes

```bash
cat file1hash
cat file2hash
```

### Compare the Two Hash Files Byte by Byte

```bash
cmp file1hash file2hash
```

**Expected Output:**

```
file1hash file2hash differ: char 1, line 1
```

> **Note:** The `cmp` command compares two files byte by byte and reports the exact position of the first difference. In this case, the hashes differ from the very first character, confirming the files are not identical.

> **Q:** Based on the hash values, is `file1.txt` different from `file2.txt`?
> **A:** Yes — the differing hashes confirm the file contents are not the same.

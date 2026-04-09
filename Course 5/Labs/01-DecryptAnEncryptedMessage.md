# Decrypt an Encrypted Message

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47139257?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Starting Directory: `/home/analyst`
- Privileges: Standard user

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Understanding encryption and decryption is fundamental to protecting and recovering data.
- Ransomware attacks encrypt victim files — knowing how ciphers work helps analysts assess the scope of an incident and recover data when possible.
- Tools like `openssl` are widely used in security operations for encrypting, decrypting, and verifying file integrity.

---

## Background: The Caesar Cipher

The Caesar cipher is one of the oldest encryption methods. It works by shifting each letter in the alphabet by a fixed number of positions. For example, with a left shift of 3:

```
Encrypted:  d e f g ...
Original:   a b c d ...
```

So `d` decrypts to `a`, `e` to `b`, and so on. The Linux `tr` command can be used to apply this mapping and reverse the cipher.

---

## Task 1: Read the Contents of a File

### List the Home Directory

```bash
ls /home/analyst
```

**Expected Output:**

```
Q1.encrypted  README.txt  caesar
```

### Read the README

```bash
cat README.txt
```

**Expected Output:**

```
Hello,
All of your data has been encrypted. To recover your data, you will need to
solve a cipher. To get started look for a hidden file in the caesar subdirectory.
```

> The README instructs you to look for a hidden file inside the `caesar` subdirectory.

---

## Task 2: Find a Hidden File

### Navigate to the `caesar` Directory

```bash
cd caesar
```

### List All Files Including Hidden Ones

```bash
ls -a
```

**Expected Output:**

```
.  ..  .leftShift3
```

> Hidden files in Linux begin with a period (`.`). They are invisible to a standard `ls` but visible with the `-a` flag.

### Read the Hidden File

```bash
cat .leftShift3
```

The contents will appear scrambled — this is the Caesar cipher with a left shift of 3.

### Decrypt the Caesar Cipher

```bash
cat .leftShift3 | tr "d-za-cD-ZA-C" "a-zA-Z"
```

**Expected Output:**

```
In order to recover your files you will need to enter the following command:

openssl aes-256-cbc -pbkdf2 -a -d -in Q1.encrypted -out Q1.recovered -k ettubrute
```

> **How `tr` works here:** The first argument `"d-za-cD-ZA-C"` is the encrypted character set (shifted by 3). The second argument `"a-zA-Z"` is the original character set. The command maps each shifted character back to its original letter, effectively reversing the cipher.

### Return to the Home Directory

```bash
cd ~
```

---

## Task 3: Decrypt a File

Use the `openssl` command revealed in the previous task to decrypt the encrypted file.

```bash
openssl aes-256-cbc -pbkdf2 -a -d -in Q1.encrypted -out Q1.recovered -k ettubrute
```

### Command Breakdown

| Flag / Option         | Meaning                                                    |
| --------------------- | ---------------------------------------------------------- |
| `aes-256-cbc`       | Symmetric encryption algorithm used (AES with 256-bit key) |
| `-pbkdf2`           | Adds extra security to the key derivation process          |
| `-a`                | Specifies Base64 encoding for the output                   |
| `-d`                | Decrypt mode                                               |
| `-in Q1.encrypted`  | Input file to decrypt                                      |
| `-out Q1.recovered` | Output file to write the decrypted data to                 |
| `-k ettubrute`      | Password used to decrypt the file                          |

### Verify the Decrypted File Exists

```bash
ls
```

**Expected Output:**

```
Q1.encrypted  Q1.recovered  README.txt  caesar
```

### Read the Recovered File

```bash
cat Q1.recovered
```

**Expected Output:**

```
If you are able to read this, then you have successfully decrypted the classic
cipher text. You recovered the encryption key that was used to encrypt this
file. Great work!
```

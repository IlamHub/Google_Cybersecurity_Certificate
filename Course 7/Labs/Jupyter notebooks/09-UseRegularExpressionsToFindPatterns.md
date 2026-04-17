# Activity: Use Regular Expressions to Find Patterns

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Use Regular Expressions to Find Patterns
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

Security analysts often analyze log files containing information about login attempts, device activity, and network connections. Regular expressions (regex) allow analysts to efficiently extract important information from strings and files by defining flexible search patterns.

In this lab, regular expressions are used to extract device IDs from a device log and valid IP addresses from a network login log, then flag those that require further investigation.

---

## Scenario

Two main tasks are automated in this lab:

1. Extracting device IDs that start with `"r15"` — indicating an OS that requires an update.
2. Extracting valid IP addresses from a login log and comparing them to a flagged address list.

---

## Task 1 — Importing the `re` Module

**Code:**

```python
# Import the `re` module in Python

import re
```

The `re` module is Python's built-in library for regular expressions. It must be imported before any regex functions like `re.findall()` can be used. No output is produced by this import statement.

---

## Task 2 — Displaying the Device Log

**Code:**

```python
# Assign `devices` to a string containing device IDs

devices = "r262c36 67bv8fy 41j1u2e r151dm4 1270t3o 42dr56i r15xk9h 2j33krk 253be78 ac742a1 r15u9q5 zh86b2l ii286fq 9x482kt 6oa6m6u x3463ac i4l56nq g07h55q 081qc9t r159r1u"

# Display the contents of `devices`

print(devices)
```

**Output:**

```
r262c36 67bv8fy 41j1u2e r151dm4 1270t3o 42dr56i r15xk9h 2j33krk 253be78 ac742a1 r15u9q5 zh86b2l ii286fq 9x482kt 6oa6m6u x3463ac i4l56nq g07h55q 081qc9t r159r1u
```

The log contains 20 space-separated device IDs. The goal is to extract only those that begin with `"r15"` — the devices running the outdated OS.

---

## Task 3 — Writing the Regex Pattern for Device IDs

**Code:**

```python
# Assign `target_pattern` to a regular expression pattern for finding device IDs that start with "r15"

target_pattern = "r15\w+"
```

**Output:**

```
(no output — only a variable assignment)
```

**Question 1 — What regular expression pattern did you use? What would happen if each component were missing?**

The pattern used is `"r15\w+"`. Here is what each component does:

- `r15` — a literal string that anchors the match to device IDs beginning with exactly those three characters. Without this prefix, the pattern would match device IDs that don't start with `"r15"`.
- `\w` — a regex symbol that matches any single **word character** — letters, digits, or underscores. Without `\w`, the pattern would only match the literal string `"r15"` with nothing after it, missing the rest of each device ID.
- `+` — a quantifier meaning **one or more** occurrences of the preceding element (`\w`). Without `+`, the pattern would only match `"r15"` followed by exactly one character, returning truncated results like `"r15x"` instead of `"r15xk9h"`.

---

## Task 4 — Extracting Matching Device IDs with `re.findall()`

**Code:**

```python
devices = "r262c36 67bv8fy 41j1u2e r151dm4 1270t3o 42dr56i r15xk9h 2j33krk 253be78 ac742a1 r15u9q5 zh86b2l ii286fq 9x482kt 6oa6m6u x3463ac i4l56nq g07h55q 081qc9t r159r1u"

target_pattern = "r15\w+"

# Use `re.findall()` to find the device IDs that start with "r15" and display the results

print(re.findall(target_pattern, devices))
```

**Output:**

```
['r151dm4', 'r15xk9h', 'r15u9q5', 'r159r1u']
```

`re.findall(pattern, string)` scans through the string and returns a list of all non-overlapping matches. Four device IDs beginning with `"r15"` are found — these are the devices that need an OS update.

---

## Task 5 — Displaying the Network Login Log

**Code:**

```python
log_file = "eraab 2022-05-10 6:03:41 192.168.152.148 \niuduike 2022-05-09 6:46:40 192.168.22.115 \nsmartell 2022-05-09 19:30:32 192.168.190.178 \narutley 2022-05-12 17:00:59 1923.1689.3.24 \nrjensen 2022-05-11 0:59:26 192.168.213.128 \naestrada 2022-05-09 19:28:12 1924.1680.27.57 \nasundara 2022-05-11 18:38:07 192.168.96.200 \ndkot 2022-05-12 10:52:00 1921.168.1283.75 \nabernard 2022-05-12 23:38:46 19245.168.2345.49 \ncjackson 2022-05-12 19:36:42 192.168.247.153 \njclark 2022-05-10 10:48:02 192.168.174.117 \nalevitsk 2022-05-08 12:09:10 192.16874.1390.176 \njrafael 2022-05-10 22:40:01 192.168.148.115 \nyappiah 2022-05-12 10:37:22 192.168.103.10654 \ndaquino 2022-05-08 7:02:35 192.168.168.144"

# Display contents of `log_file`

print(log_file)
```

**Output:**

```
eraab 2022-05-10 6:03:41 192.168.152.148 
iuduike 2022-05-09 6:46:40 192.168.22.115 
smartell 2022-05-09 19:30:32 192.168.190.178 
arutley 2022-05-12 17:00:59 1923.1689.3.24 
...
```

Each line contains a username, date, login time, and IP address. Some IP addresses are malformed due to data collection errors — the goal is to extract only the valid ones.

---

## Task 6 — Writing the Regex Pattern for IP Addresses (Strict: 3 Digits per Segment)

**Code:**

```python
# Assign `pattern` to a regular expression that matches IP addresses of the form xxx.xxx.xxx.xxx

pattern = "\d\d\d\.\d\d\d\.\d\d\d\.\d\d\d"
```

**Output:**

```
(no output — only a variable assignment)
```

- `\d` — matches a single digit (0–9).
- `\d\d\d` — matches exactly three consecutive digits.
- `\.` — matches a literal period. The backslash is needed because `.` on its own in regex means "any character" — the backslash escapes it to mean a literal dot.
- The full pattern repeats this four times separated by `\.`, targeting the `xxx.xxx.xxx.xxx` format.

---

## Task 7 — Extracting IP Addresses (Strict Pattern)

**Code:**

```python
pattern = "\d\d\d\.\d\d\d\.\d\d\d\.\d\d\d"

print(re.findall(pattern, log_file))
```

**Output:**

```
['192.168.152.148', '192.168.190.178', '192.168.213.128', '192.168.247.153', '192.168.174.117', '192.168.148.115', '192.168.168.144']
```

**Question 2 — What was extracted? What was not extracted? Are any unextracted IPs valid?**

Seven IP addresses were extracted — all with exactly three digits per segment. Several were missed:

- `192.168.22.115` — not extracted because the third segment `"22"` has only two digits, which doesn't match the strict `\d\d\d` requirement.
- `192.168.96.200` — missed for the same reason (`"96"` is two digits).
- `192.168.103.10654` — not extracted because its last segment has five digits.

Both `192.168.22.115` and `192.168.96.200` are valid IP addresses that were incorrectly excluded. The pattern needs to be made more flexible to capture them.

---

## Task 8 — Updating the Pattern with `\d+`

**Code:**

```python
# Update `pattern` to allow any number of digits per segment

pattern = "\d+\.\d+\.\d+\.\d+"

print(re.findall(pattern, log_file))
```

**Output:**

```
['192.168.152.148', '192.168.22.115', '192.168.190.178', '1923.1689.3.24', '192.168.213.128', '1924.1680.27.57', '192.168.96.200', '1921.168.1283.75', '19245.168.2345.49', '192.168.247.153', '192.168.174.117', '192.16874.1390.176', '192.168.148.115', '192.168.103.10654', '192.168.168.144']
```

**Question 3 — What gets extracted? Do all extracted IPs have between one and three digits per segment?**

All IP-like patterns are now extracted — but the results include invalid addresses like `"1923.1689.3.24"` and `"19245.168.2345.49"`, which have segments with four or five digits. The `+` quantifier means "one or more digits" with no upper limit, so it over-matches. The pattern needs to be constrained to between one and three digits per segment.

---

## Task 9 — Constraining Digit Count with Curly Brackets `{1,3}`

**Code:**

```python
# Assign `pattern` to a regular expression that matches only valid IP addresses

pattern = "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"

# Use `re.findall()` and store the output in `valid_ip_addresses`

valid_ip_addresses = re.findall(pattern, log_file)

# Display the contents of `valid_ip_addresses`

print(valid_ip_addresses)
```

**Output:**

```
['192.168.152.148', '192.168.22.115', '192.168.190.178', '192.168.213.128', '192.168.96.200', '192.168.247.153', '192.168.174.117', '192.168.148.115', '192.168.168.144']
```

**Question 4 — What do you notice about the extracted IPs compared to the previous two tasks?**

The `{1,3}` quantifier restricts each segment to between one and three digits — exactly what a valid IPv4 segment requires. Compared to Task 7 (too strict — missed short segments) and Task 8 (too loose — included long invalid segments), this pattern correctly extracts all nine valid IP addresses while excluding the malformed ones. This is the final, correct pattern for this use case.

---

## Task 10 — Displaying the Flagged IP Address List

**Code:**

```python
# Assign `flagged_addresses` to a list of previously flagged IP addresses

flagged_addresses = ["192.168.190.178", "192.168.96.200", "192.168.174.117", "192.168.168.144"]

# Display the contents of `flagged_addresses`

print(flagged_addresses)
```

**Output:**

```
['192.168.190.178', '192.168.96.200', '192.168.174.117', '192.168.168.144']
```

Four IP addresses have been previously flagged for unusual activity and are stored for comparison against the extracted valid IPs.

---

## Task 11 — Iterating Through Valid IPs and Flagging Matches

**Code:**

```python
log_file = "eraab 2022-05-10 6:03:41 192.168.152.148 \niuduike 2022-05-09 6:46:40 192.168.22.115 \nsmartell 2022-05-09 19:30:32 192.168.190.178 \narutley 2022-05-12 17:00:59 1923.1689.3.24 \nrjensen 2022-05-11 0:59:26 192.168.213.128 \naestrada 2022-05-09 19:28:12 1924.1680.27.57 \nasundara 2022-05-11 18:38:07 192.168.96.200 \ndkot 2022-05-12 10:52:00 1921.168.1283.75 \nabernard 2022-05-12 23:38:46 19245.168.2345.49 \ncjackson 2022-05-12 19:36:42 192.168.247.153 \njclark 2022-05-10 10:48:02 192.168.174.117 \nalevitsk 2022-05-08 12:09:10 192.16874.1390.176 \njrafael 2022-05-10 22:40:01 192.168.148.115 \nyappiah 2022-05-12 10:37:22 192.168.103.10654 \ndaquino 2022-05-08 7:02:35 192.168.168.144"

pattern = "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"

valid_ip_addresses = re.findall(pattern, log_file)

flagged_addresses = ["192.168.190.178", "192.168.96.200", "192.168.174.117", "192.168.168.144"]

# Loop through valid_ip_addresses and check each against the flagged list

for address in valid_ip_addresses:
    if address in flagged_addresses:
        print("The IP address", address, "has been flagged for further analysis.")
    else:
        print("The IP address", address, "does not require further analysis.")
```

**Output:**

```
The IP address 192.168.152.148 does not require further analysis.
The IP address 192.168.22.115 does not require further analysis.
The IP address 192.168.190.178 has been flagged for further analysis.
The IP address 192.168.213.128 does not require further analysis.
The IP address 192.168.96.200 has been flagged for further analysis.
The IP address 192.168.247.153 does not require further analysis.
The IP address 192.168.174.117 has been flagged for further analysis.
The IP address 192.168.148.115 does not require further analysis.
The IP address 192.168.168.144 has been flagged for further analysis.
```

The `for` loop iterates over each valid IP. The `in` operator checks membership in `flagged_addresses` on every iteration. Four IPs are flagged — `192.168.190.178`, `192.168.96.200`, `192.168.174.117`, and `192.168.168.144` — matching exactly the addresses in the `flagged_addresses` list. These are the accounts that warrant further investigation.

---

## Conclusion

**Key takeaways from this lab:**

- The **`re` module** must be imported before any regular expression functions can be used.
- **`re.findall(pattern, string)`** returns a list of all non-overlapping matches of the pattern found in the string.
- **`\w`** matches any word character (letters, digits, underscores); **`\d`** matches any digit (0–9); **`\.`** matches a literal period.
- The **`+` quantifier** means one or more occurrences — useful but can over-match if not bounded.
- **Curly brackets `{min,max}`** provide precise control over the number of repetitions — `\d{1,3}` ensures each IP segment has between one and three digits, filtering out malformed addresses.
- Combining **regex extraction** with a **`for` loop and `in` operator** creates a complete pipeline: extract relevant data from raw logs, then automatically flag entries that match a known threat list.
- Iterating through regex results and comparing against a flagged list is a core pattern in **automated log analysis** — a routine task in SOC (Security Operations Center) workflows.

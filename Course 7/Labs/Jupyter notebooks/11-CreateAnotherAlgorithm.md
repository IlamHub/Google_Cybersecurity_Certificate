# Activity: Create Another Algorithm

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Create Another Algorithm
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

An important part of cybersecurity is controlling access to restricted content. In this lab, a text file containing allowed IP addresses is parsed and updated by removing addresses that no longer have access. Python makes it possible to automate this entire process through an algorithm built step by step and ultimately wrapped in a reusable function.

---

## Scenario

As a security analyst, an algorithm is developed that:

1. Reads an allow list of IP addresses from `allow_list.txt`.
2. Removes any IP addresses that appear in a `remove_list`.
3. Writes the cleaned list back to the original file.
4. Wraps the entire process in a reusable `update_file()` function.

---

## Task 1 — Displaying the Import File and Remove List

**Code:**

```python
# Assign `import_file` to the name of the file

import_file = "allow_list.txt"

# Assign `remove_list` to a list of IP addresses that are no longer allowed

remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# Display both variables

print(import_file)
print(remove_list)
```

**Output:**

```
allow_list.txt
['192.168.97.225', '192.168.158.170', '192.168.201.40', '192.168.58.57']
```

**Question 1 — What do you observe about the output above?**

`import_file` is a string containing the filename. `remove_list` is a Python list of four IP address strings — these are the addresses whose access has been revoked and that need to be removed from the allow list file. The algorithm's job is to cross-reference these two pieces of data and clean the file accordingly.

---

## Task 2 — Opening the File with a `with` Statement

**Code:**

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# First line of the `with` statement

with open(import_file, "r") as file:
```

**Output:**

```
(error — with statement body is empty at this stage)
```

The `with open(import_file, "r")` statement opens the file in read mode. Using `with` ensures the file is automatically closed once the block finishes. The file object is bound to the variable `file` for use inside the block.

---

## Task 3 — Reading the File into `ip_addresses`

**Code:**

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:

    # Use `.read()` to read the imported file and store it in `ip_addresses`

    ip_addresses = file.read()

# Display `ip_addresses`

print(ip_addresses)
```

**Output:**

```
192.168.218.160 192.168.97.225 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246
```

**Question 2 — Do you notice any IP addresses in the allow list that are also in the `remove_list`?**

Yes — `192.168.97.225` appears in both the allow list file and in `remove_list`. This is the address (and any others matching the remove list) that the algorithm must identify and delete from the file. At this stage, the data is stored as one large string — it needs to be converted to a list before individual IPs can be removed.

---

## Task 4 — Converting the String to a List with `.split()`

**Code:**

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:
    ip_addresses = file.read()

# Use `.split()` to convert `ip_addresses` from a string to a list

ip_addresses = ip_addresses.split()

# Display `ip_addresses`

print(ip_addresses)
```

**Output:**

```
['192.168.218.160', '192.168.97.225', '192.168.145.158', '192.168.108.13', '192.168.60.153', '192.168.96.200', '192.168.247.153', '192.168.3.252', '192.168.116.187', '192.168.15.110', '192.168.39.246']
```

`.split()` with no arguments splits the string at every whitespace (spaces, newlines, tabs) and returns a list of individual strings. Each IP address is now a separate element in the list, making it possible to iterate through them and check for matches against `remove_list`.

---

## Task 5 — Building the `for` Loop to Iterate Through IP Addresses

**Code:**

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:
    ip_addresses = file.read()

ip_addresses = ip_addresses.split()

# Build iterative statement — loop variable named `element`

for element in ip_addresses:

    # Display `element` in every iteration

    print(element)
```

**Output:**

```
192.168.218.160
192.168.97.225
192.168.145.158
192.168.108.13
192.168.60.153
192.168.96.200
192.168.247.153
192.168.3.252
192.168.116.187
192.168.15.110
192.168.39.246
```

The `for` loop visits each IP address in `ip_addresses` one at a time, assigning it to the loop variable `element`. This sets up the structure needed for the next step — adding a conditional check inside the loop to identify and remove flagged addresses.

---

## Task 6 — Adding a Conditional to Remove Flagged IPs

**Code:**

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:
    ip_addresses = file.read()

ip_addresses = ip_addresses.split()

for element in ip_addresses:

    # If the current element is in `remove_list`, remove it from `ip_addresses`

    if element in remove_list:
        ip_addresses.remove(element)

# Display the updated `ip_addresses`

print(ip_addresses)
```

**Output:**

```
['192.168.218.160', '192.168.145.158', '192.168.108.13', '192.168.60.153', '192.168.96.200', '192.168.247.153', '192.168.3.252', '192.168.116.187', '192.168.15.110', '192.168.39.246']
```

The `if element in remove_list` conditional checks each IP on every iteration. When a match is found, `.remove()` deletes the first occurrence of that element from `ip_addresses`. The result is a cleaned list with `192.168.97.225` removed. The other three addresses in `remove_list` (`192.168.158.170`, `192.168.201.40`, `192.168.58.57`) were not in the allow list to begin with, so no further removals occur.

---

## Task 7 — Writing the Updated List Back to the File

**Code:**

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:
    ip_addresses = file.read()

ip_addresses = ip_addresses.split()

for element in ip_addresses:
    if element in remove_list:
        ip_addresses.remove(element)

# Convert `ip_addresses` back to a string for writing

ip_addresses = " ".join(ip_addresses)

# Rewrite the original file with the updated content

with open(import_file, "w") as file:
    file.write(ip_addresses)
```

**Output:**

```
(no output — the file is rewritten silently)
```

Before writing back to the file, `" ".join(ip_addresses)` converts the list back into a single string with spaces between each IP address. This is necessary because `.write()` requires a string argument. Opening the file with `"w"` mode then **overwrites** the original contents with the updated, cleaned list. Using `"w"` is appropriate here because the intent is to fully replace the old allow list with the new one.

---

## Task 8 — Reading and Verifying the Updated File

**Code:**

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:
    ip_addresses = file.read()

ip_addresses = ip_addresses.split()

for element in ip_addresses:
    if element in remove_list:
        ip_addresses.remove(element)

ip_addresses = " ".join(ip_addresses)

with open(import_file, "w") as file:
    file.write(ip_addresses)

# Read the updated file and verify

with open(import_file, "r") as file:
    text = file.read()

print(text)
```

**Output:**

```
192.168.218.160 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246
```

The read-after-write confirms the file was updated correctly. `192.168.97.225` is no longer in the allow list. The remaining 10 IP addresses are all valid and none match the revoked addresses in `remove_list`.

---

## Task 9 — Wrapping the Algorithm in a Function

**Code:**

```python
# Define `update_file()` that takes in `import_file` and `remove_list` as parameters

def update_file(import_file, remove_list):

    # Read the initial contents of the file

    with open(import_file, "r") as file:
        ip_addresses = file.read()

    # Convert the string to a list

    ip_addresses = ip_addresses.split()

    # Remove IPs that are in `remove_list`

    for element in ip_addresses:
        if element in remove_list:
            ip_addresses.remove(element)

    # Convert the list back to a string

    ip_addresses = " ".join(ip_addresses)

    # Overwrite the file with the updated content

    with open(import_file, "w") as file:
        file.write(ip_addresses)
```

**Output:**

```
(no output — function is defined, not called)
```

**Question 3 — What are the benefits of incorporating the algorithm into a single function?**

Wrapping the algorithm in `update_file()` provides several key benefits:

- **Reusability** — the function can be called anytime with any filename and any remove list, without rewriting the logic.
- **Simplicity** — a single function call like `update_file("allow_list.txt", remove_list)` replaces 15+ lines of code at every usage point.
- **Maintainability** — if the logic needs to change (e.g., handling duplicates differently), the update is made in one place and applies everywhere the function is called.
- **Readability** — a named function with descriptive parameters makes the code's intent immediately clear to anyone reading it.
- **Scalability** — the same function can be applied to multiple different allow list files across the organization with no code duplication.

---

## Task 10 — Calling `update_file()` with a New Remove List

**Code:**

```python
def update_file(import_file, remove_list):

    with open(import_file, "r") as file:
        ip_addresses = file.read()

    ip_addresses = ip_addresses.split()

    for element in ip_addresses:
        if element in remove_list:
            ip_addresses.remove(element)

    ip_addresses = " ".join(ip_addresses)

    with open(import_file, "w") as file:
        file.write(ip_addresses)

# Call `update_file()` with the allow list file and a new remove list

update_file("allow_list.txt", ["192.168.25.60", "192.168.140.81", "192.168.203.198"])

# Read and display the updated file

with open("allow_list.txt", "r") as file:
    text = file.read()

print(text)
```

**Output:**

```
192.168.218.160 192.168.145.158 192.168.108.13 192.168.60.153 192.168.96.200 192.168.247.153 192.168.3.252 192.168.116.187 192.168.15.110 192.168.39.246
```

The function is called with a new set of IP addresses to remove. Since none of the three addresses in the new `remove_list` (`192.168.25.60`, `192.168.140.81`, `192.168.203.198`) exist in the current allow list, the file remains unchanged from its previous state. This confirms the function handles cases where remove list entries are not present in the file without errors.

---

## Conclusion

**Key takeaways from this lab:**

- **Reading and writing files** with `open()`, `.read()`, and `.write()` is the foundation of automated log and access list management in Python.
- **`.split()`** converts a string into a list — essential for iterating over individual IP addresses rather than one large blob of text.
- **`" ".join(list)`** converts a list back into a space-separated string before writing it back to a file — the reverse of `.split()`.
- A **`for` loop with a nested `if` and `.remove()`** provides a clean pattern for filtering unwanted entries from a list.
- Using `"w"` mode intentionally **overwrites** the file — appropriate when replacing old access records with a fully updated version.
- Wrapping a multi-step algorithm in a **function** with parameters makes it reusable, readable, and easy to maintain across different files and remove lists.
- This lab demonstrates a complete **file-based access control automation** workflow — a pattern commonly used in real SOC (Security Operations Center) environments for managing allow and block lists.

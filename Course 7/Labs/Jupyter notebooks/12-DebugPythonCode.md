# Activity: Debug Python Code

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Debug Python Code
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

One of the biggest challenges faced by analysts is ensuring that automated processes run smoothly. Debugging is an important practice that security analysts incorporate in their work to identify errors in code and resolve them so that the code achieves the desired outcome.

In this lab, three categories of Python errors are identified and fixed: **syntax errors**, **exceptions** (runtime errors), and **logic errors**.

---

## Scenario

Code similar to what was written in earlier labs is presented here — but each cell contains deliberate errors. The task is to read the code, run it, identify what's wrong, and fix it.

---

## Task 1 — Syntax Error: Missing Colon in `for` Loop

**Buggy Code:**

```python
for i in range(10)
    print("Connection cannot be established")
```

**Error:**

```
SyntaxError: expected ':'
```

**Fixed Code:**

```python
# For loop that iterates over a range of numbers
# and displays a message each iteration

for i in range(10):
    print("Connection cannot be established")
```

**Output:**

```
Connection cannot be established
Connection cannot be established
Connection cannot be established
Connection cannot be established
Connection cannot be established
Connection cannot be established
Connection cannot be established
Connection cannot be established
Connection cannot be established
Connection cannot be established
```

**Question 1 — What happens when you run the code before modifying it? How can you fix it?**

Running the buggy code raises a `SyntaxError` because the `for` statement is missing a colon (`:`) at the end. In Python, the colon is required to signal the start of the loop body. Adding `:` after `range(10)` resolves the error and allows the loop to execute all 10 iterations correctly.

---

## Task 2 — Syntax Error: Missing Closing Quote in a List

**Buggy Code:**

```python
usernames_list = ["djames", "jpark", "tbailey", "zdutchma "esmith", "srobinso", "dcoleman", "fbautist"]
```

**Error:**

```
SyntaxError: invalid syntax
```

**Fixed Code:**

```python
# Assign `usernames_list` to a list of usernames

usernames_list = ["djames", "jpark", "tbailey", "zdutchma", "esmith", "srobinso", "dcoleman", "fbautist"]

# Display `usernames_list`

print(usernames_list)
```

**Output:**

```
['djames', 'jpark', 'tbailey', 'zdutchma', 'esmith', 'srobinso', 'dcoleman', 'fbautist']
```

**Question 2 — What happens when you run the code before modifying it? How can you fix it?**

The code raises a `SyntaxError` because the string `"zdutchma` is missing its closing quotation mark — it reads `"zdutchma "esmith"` instead of `"zdutchma", "esmith"`. Python sees everything between the opening quote of `"zdutchma` and the closing quote of `esmith"` as one malformed string, causing a syntax error. Adding `"` after `zdutchma` and a comma to separate the two strings fixes the issue.

---

## Task 3 — Syntax Error: Missing Closing Parenthesis

**Buggy Code:**

```python
print("update needed".upper()
```

**Error:**

```
SyntaxError: '(' was never closed
```

**Fixed Code:**

```python
# Display a message in upper case

print("update needed".upper())
```

**Output:**

```
UPDATE NEEDED
```

**Question 3 — What happens when you run the code before modifying it? What is causing the error? How can you fix it?**

Running the buggy code raises a `SyntaxError` because the `print()` call is missing its closing parenthesis `)`. Python opened a parenthesis for `print(` but never found a matching closing `)`, so it reports the parenthesis was never closed. Adding the missing `)` at the end resolves the error and the string is displayed in uppercase as expected.

---

## Task 4 — Two Syntax Errors + One Exception (NameError + IndentationError + Assignment Operator)

**Buggy Code:**

```python
usernames_list = ["djames", "jpark", "tbailey", "zdutchma", "esmith", "srobinso", "dcoleman", "fbautist"]

username = "esmith"

for name in username_list:       # Error 1: wrong variable name (NameError)
    if name = username:           # Error 2: assignment `=` instead of comparison `==`
    print("The user is an approved user")  # Error 3: missing indentation
```

**Fixed Code:**

```python
# Assign `usernames_list` to a list of approved usernames

usernames_list = ["djames", "jpark", "tbailey", "zdutchma", "esmith", "srobinso", "dcoleman", "fbautist"]

# Assign `username` to a specific username

username = "esmith"

# For loop that iterates over `usernames_list` and checks for a match

for name in usernames_list:

    # Check if `name` matches `username`

    if name == username:
        print("The user is an approved user")
```

**Output:**

```
The user is an approved user
```

**Question 4 — What happens when you run the code before modifying it? What is causing the errors? How can you fix them?**

Three errors existed in this cell:

1. **NameError** — the loop iterates over `username_list` but the variable is named `usernames_list` (with an `s`). Python raises `NameError: name 'username_list' is not defined` because the variable doesn't exist. Fix: correct the name to `usernames_list`.
2. **SyntaxError** — the condition `if name = username` uses `=` (assignment) instead of `==` (comparison). In Python, `=` assigns a value and is not valid inside an `if` condition — only `==` tests equality. Fix: change `=` to `==`.
3. **IndentationError** — the `print()` statement is not indented inside the `if` block. Python requires the body of an `if` statement to be indented. Fix: indent `print()` by one level inside the `if`.

---

## Task 5 — Exception: Index Out of Range (IndexError)

**Buggy Code:**

```python
usernames_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]

username = "eraab"

if username == usernames_list[5]:
    print("This username is the final one in the list.")
```

**Error:**

```
IndexError: list index out of range
```

**Fixed Code:**

```python
# Assign `usernames_list` to a list of usernames

usernames_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]

# Assign `username` to a specific username

username = "eraab"

# Determine whether `username` is the final username in `usernames_list`

if username == usernames_list[4]:
    print("This username is the final one in the list.")
```

**Output:**

```
This username is the final one in the list.
```

**Question 5 — What happens when you run the code before modifying it? What type of error is this? How can you fix it?**

Running the buggy code raises an `IndexError: list index out of range`. This is a **runtime exception** — the syntax is valid, but the operation fails during execution. The list `usernames_list` has 5 elements at indices `0` through `4`. Accessing index `5` is out of bounds since it doesn't exist. Since `"eraab"` is the last element, it sits at index `4`, not `5`. Fix: change `usernames_list[5]` to `usernames_list[4]`.

---

## Task 6 — Syntax Error + Exception: Broken `with` Statement and Wrong `.split()` Call

**Buggy Code:**

```python
with open(import_file, "r") as file    # Error 1: missing colon
    ip_addresses = file.read()

ip_addresses = split.ip_addresses()    # Error 2: method called on wrong object
```

**Fixed Code:**

```python
# Assign `import_file` to the name of the text file

import_file = "allow_list.txt"

# Assign `remove_list` to a list of IP addresses that are no longer allowed

remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# With statement that reads the text file and stores its contents in `ip_addresses`

with open(import_file, "r") as file:
    ip_addresses = file.read()

# Convert `ip_addresses` from a string to a list

ip_addresses = ip_addresses.split()

# For loop that removes revoked IP addresses

for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)

# Display `ip_addresses` after the removal process

print(ip_addresses)
```

**Output:**

```
['192.168.218.160', '192.168.145.158', '192.168.108.13', '192.168.60.153', '192.168.96.200', '192.168.247.153', '192.168.3.252', '192.168.116.187', '192.168.15.110', '192.168.39.246']
```

**Question 6 — What happens when you run the code before modifying it? What is causing the errors? How can you fix them?**

Two errors existed:

1. **SyntaxError** — the `with open(...)` line is missing a colon `:` at the end. Python requires a colon after every compound statement header (`with`, `for`, `if`, `def`, etc.). Fix: add `:` after `as file`.
2. **AttributeError** — `split.ip_addresses()` is written in the wrong order. `.split()` is a string method that must be called **on the string object** — not as a standalone function with the string as an argument. The correct syntax is `ip_addresses.split()`. Fix: reverse the order to `ip_addresses.split()`.

---

## Task 7 — Logic Errors: Wrong Index Assignments in Conditionals

**Buggy Code:**

```python
system = "OS 2"
patch_schedule = ["March 1st", "April 1st", "May 1st"]

if system == "OS 1":
    print("Patch date:", patch_schedule[2])   # Should be index 0

elif system == "OS 2":
    print("Patch date:", patch_schedule[0])   # Should be index 1

elif system == "OS 3":
    print("Patch date:", patch_schedule[2])   # Correct, but OS 1 was wrong
```

**Output (buggy — when `system = "OS 2"`):**

```
Patch date: March 1st
```

**Fixed Code:**

```python
# Assign `system` to a specific operating system as a string

system = "OS 2"

# Assign `patch_schedule` to a list of patch dates in order of operating system

patch_schedule = ["March 1st", "April 1st", "May 1st"]

# Conditional statement with corrected index assignments

if system == "OS 1":
    print("Patch date:", patch_schedule[0])

elif system == "OS 2":
    print("Patch date:", patch_schedule[1])

elif system == "OS 3":
    print("Patch date:", patch_schedule[2])
```

**Output (fixed — when `system = "OS 2"`):**

```
Patch date: April 1st
```

**Question 7 — What happens when you run the code before modifying it? What is causing the logic errors? How can you fix them?**

The buggy code produces no `SyntaxError` or exception — it runs without crashing. This makes **logic errors** the hardest type to detect. The problem is in the index values used in each branch:

- `OS 1` should map to `patch_schedule[0]` (`"March 1st"`), but the code used `patch_schedule[2]` (`"May 1st"`).
- `OS 2` should map to `patch_schedule[1]` (`"April 1st"`), but the code used `patch_schedule[0]` (`"March 1st"`).
- `OS 3` correctly maps to `patch_schedule[2]` (`"May 1st"`).

The fix is to align each OS branch with the correct index: `OS 1 → [0]`, `OS 2 → [1]`, `OS 3 → [2]`. Testing with different `system` values and comparing the output against the expected patch schedule is the correct debugging approach for logic errors.

---

## Conclusion

**Key takeaways from this lab:**

- Python errors fall into three main categories, each requiring a different debugging approach:
  - **Syntax errors** — caught before the code runs; caused by violations of Python grammar (missing colons, unmatched quotes/parentheses, wrong operators). Fix by carefully reading the error message and the flagged line.
  - **Exceptions (runtime errors)** — the syntax is valid but the code fails during execution (e.g., `NameError`, `IndexError`, `AttributeError`). Fix by understanding what the error type means and tracing the variable or operation that caused it.
  - **Logic errors** — the code runs without crashing but produces incorrect results. These are the hardest to catch because Python cannot flag them automatically. Fix by testing with known inputs and comparing actual vs. expected outputs.
- **One error at a time** is the recommended debugging strategy — fix the first error, re-run, then address the next.
- Common mistakes to watch for: missing `:` after loop/conditional headers, `=` vs `==` in conditions, off-by-one index errors, misspelled variable names, and reversed method call syntax (e.g., `split.ip_addresses()` vs `ip_addresses.split()`).

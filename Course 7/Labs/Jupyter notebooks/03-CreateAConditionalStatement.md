# Activity: Create a Conditional Statement

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Create a Conditional Statement
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

Conditional statements are a powerful structure that help in achieving automation when you need to make sure conditions are met before certain actions are executed. For example, security analysts can use conditional statements in Python to check if users are approved to access a device.

In this lab, conditional statements are practiced in Python.

---

## Scenario

As a security analyst, the following tasks must be completed:

1. Check whether a user's operating system requires an update.
2. Investigate login attempts to a specific device — determining if attempts were made by approved users during organization hours.

---

## Task 1 — Basic `if` Statement for OS Check

**Code:**

```python
# Assign a variable named `system` to a specific operating system

system = "OS 2"

# If OS 2 is running, then display a "no update needed" message

if system == "OS 2":
    print("no update needed")
```

**Output:**

```
no update needed
```

---

## Task 2 — Testing the `if` Statement with Different OS Values

**Code:**

```python
# Assign `system` to a specific operating system

system = "OS 1"

# If OS 2 is running, then display a "no update needed" message

if system == "OS 2":
    print("no update needed")
```

**Output:**

```
(no output)
```

**Question 1 — What happens when OS 2 is running? What happens when OS 1 is running?**

When `system = "OS 2"`, the condition `system == "OS 2"` evaluates to `True` and `"no update needed"` is displayed. When `system = "OS 1"`, the condition evaluates to `False` and nothing is displayed — the `print()` inside the `if` block is skipped entirely.

---

## Task 3 — Adding an `else` Branch

**Code:**

```python
# Assign `system` to a specific operating system

system = "OS 3"

# If OS 2 is running, then display a "no update needed" message
# Otherwise, display an "update needed" message

if system == "OS 2":
    print("no update needed")
else:
    print("update needed")
```

**Output:**

```
update needed
```

**Question 2 — What happens when OS 2 is running? What happens when OS 2 is not running?**

When `system = "OS 2"`, the `if` condition is `True` and `"no update needed"` is printed. When `system` is anything other than `"OS 2"` (including `"OS 1"`, `"OS 3"`, or any random value), the `else` branch executes and `"update needed"` is printed.

---

## Task 4 — Adding `elif` Statements for Specificity

**Code:**

```python
# Assign `system` to a specific operating system

system = "OS 4"

# If OS 2 is running, then display a "no update needed" message
# Otherwise if OS 1 is running, display an "update needed" message
# Otherwise if OS 3 is running, display an "update needed" message

if system == "OS 2":
    print("no update needed")
elif system == "OS 1":
    print("update needed")
elif system == "OS 3":
    print("update needed")
```

**Output:**

```
(no output)
```

**Question 3 — What happens for each OS value?**

- `"OS 2"` → prints `"no update needed"`
- `"OS 1"` → prints `"update needed"`
- `"OS 3"` → prints `"update needed"`
- Any other value (e.g. `"OS 4"`) → no output, since no condition matches and there is no `else` branch

Using `elif` instead of `else` prevents unrecognized values from accidentally triggering the update message.

---

## Task 5 — Combining `elif` Conditions with `or`

**Code:**

```python
# Assign `system` to a specific operating system

system = "OS 4"

# If OS 2 is running, then display a "no update needed" message
# Otherwise if either OS 1 or OS 3 is running, display an "update needed" message

if system == "OS 2":
    print("no update needed")
elif system == "OS 1" or system == "OS 3":
    print("update needed")
```

**Output:**

```
(no output)
```

**Question 4 — What do you observe about this conditional?**

This conditional behaves exactly the same as the two-`elif` version in Task 4. The difference is purely stylistic — the `or` operator combines both OS checks into a single `elif` line, making the code more concise and easier to read. This is a Python best practice: avoid repeating logic when a logical operator can express it more cleanly.

---

## Task 6 — Checking Approved Users with `or`

**Code:**

```python
# Assign approved usernames

approved_user1 = "elarson"
approved_user2 = "bmoreno"

# Assign the username of the user trying to log in

username = "bmoreno"

# If the user is among the approved users, display access granted
# Otherwise, display access denied

if username == approved_user1 or username == approved_user2:
    print("This user has access to this device.")
else:
    print("This user does not have access to this device.")
```

**Output:**

```
This user has access to this device.
```

---

## Task 7 — Using the `in` Operator with an Allow List

**Code:**

```python
# Assign `approved_list` to a list of approved usernames

approved_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]

# Assign the username of the user trying to log in

username = "jhill"

# If the user is in the approved list, display access granted
# Otherwise, display access denied

if username in approved_list:
    print("This user has access to this device.")
else:
    print("This user does not have access to this device.")
```

**Output:**

```
This user does not have access to this device.
```

**Question 5 — What happens when an approved user tries to log in? What happens when an unapproved user tries to log in?**

When `username` is found inside `approved_list`, the `in` operator returns `True` and `"This user has access to this device."` is displayed. When `username` is not in the list, it returns `False` and `"This user does not have access to this device."` is displayed. Using `in` with a list is far more scalable than chaining multiple `or` comparisons as done in Task 6.

---

## Task 8 — Checking Login Time with a Boolean Variable

**Code:**

```python
# Assign `organization_hours` to a Boolean representing whether the user is logging in during organization hours

organization_hours = True

# If logging in during organization hours, display the appropriate message
# Otherwise, display that the attempt was made outside of organization hours

if organization_hours == True:
    print("Login attempt made during organization hours.")
else:
    print("Login attempt made outside of organization hours.")
```

**Output:**

```
Login attempt made during organization hours.
```

**Question 6 — What happens when the user logs in during organization hours? What happens outside of organization hours?**

When `organization_hours = True`, the `if` condition evaluates to `True` and the "during organization hours" message is displayed. When `organization_hours = False`, the condition is `False` and the `else` branch executes, displaying the "outside of organization hours" message.

---

## Task 9 — Combining Both Checks Separately

**Code:**

```python
# Approved list

approved_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]

# Username of the user trying to log in

username = "bmoreno"

# Check if username is approved

if username in approved_list:
    print("This user has access to this device.")
else:
    print("This user does not have access to this device.")

# Check if login is during organization hours

organization_hours = True

if organization_hours == True:
    print("Login attempt made during organization hours.")
else:
    print("Login attempt made outside of organization hours.")
```

**Output:**

```
This user has access to this device.
Login attempt made during organization hours.
```

**Question 7 — What happens for each scenario?**

- **Unapproved user:** The first `if` fails, printing the "no access" message. The code then independently checks `organization_hours` and prints the appropriate time message.
- **Approved user:** The first `if` succeeds, printing the "has access" message. Then `organization_hours` is checked separately.
- **Login outside hours:** Regardless of approval status, the second conditional catches this and prints the "outside of organization hours" message.

The two conditionals are independent — both always run, and both always produce output.

---

## Task 10 — Combining Both Checks with `and`

**Code:**

```python
# Approved list

approved_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]

# Username of the user trying to log in

username = "bmoreno"

# Login time flag

organization_hours = True

# Single conditional that checks both conditions together

if username in approved_list and organization_hours == True:
    print("Login attempt made by an approved user during organization hours.")
else:
    print("Username not approved or login attempt made outside of organization hours.")
```

**Output:**

```
Login attempt made by an approved user during organization hours.
```

**Question 8 — What happens in each scenario under this setup?**

- When the user is **approved AND logging in during organization hours**, both conditions are `True`, so the `and` operator returns `True` and the success message is displayed.
- When the user is **either unapproved OR logging in outside of hours** (or both), the `and` operator returns `False` and the combined warning message is displayed.

Using `and` consolidates two separate conditionals into a single, more concise check — a cleaner design when a single outcome depends on multiple conditions being true simultaneously.

---

## Conclusion

**Key takeaways from this lab:**

- **Conditional statements** (`if`, `elif`, `else`) allow code to make decisions and execute actions only when specific conditions are met — essential for automating security checks.
- The **`==` comparison operator** checks whether two values are equal and returns a Boolean result.
- The **`or` logical operator** allows a condition to be satisfied by more than one possible value, reducing code repetition.
- The **`and` logical operator** requires all conditions to be `True` simultaneously — useful for enforcing multiple security requirements at once.
- The **`in` operator** efficiently checks whether a value exists within a list, making it far more scalable than chaining multiple `or` comparisons when working with allow lists.
- Combining conditions with logical operators makes code more **concise and readable**, which is a professional best practice.

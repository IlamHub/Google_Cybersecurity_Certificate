# Activity: Assign Python Variables

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Assign Python Variables
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

Variables help security analysts keep track of a variety of security-related information. For example, analysts may need to create Python variables for the users who are allowed to log in, the number of login attempts permitted, and the current number of attempts a user has made.

In this lab, values are assigned to variables and their data types are examined.

---

## Scenario

As a security analyst responsible for automating analysis of login attempts made to a specific device, variables must be created to track relevant login information — including the device ID, approved usernames, maximum login attempts allowed, current login attempts, and login status.

---

## Task 1 — Assigning a String Variable

**Code:**

```python
# Assign the `device_id` variable to the device ID that only specified users can access

device_id = "72e08x0"

# Display `device_id`

print(device_id)
```

**Output:**

```
72e08x0
```

---

## Task 2 — Finding the Data Type of a String Variable

**Code:**

```python
# Assign the `device_id` variable to the device ID that only specified users can access

device_id = "72e08x0"

# Assign `device_id_type` to the data type of `device_id`

device_id_type = type(device_id)

# Display `device_id_type`

print(device_id_type)
```

**Output:**

```
<class 'str'>
```

**Question 1 — What do you observe about the data type of `device_id`?**

The data type of `device_id` is `str` (string). This is because the device ID `"72e08x0"` is enclosed in quotation marks, which tells Python to treat it as text rather than a number — even though it contains digits. Strings are used whenever data needs to be stored as a sequence of characters.

---

## Task 3 — Assigning a List Variable

**Code:**

```python
# Assign `username_list` to the list of usernames who are allowed to access the device

username_list = ["madebowa", "jnguyen", "tbecker", "nhersh", "redwards"]

# Display `username_list`

print(username_list)
```

**Output:**

```
['madebowa', 'jnguyen', 'tbecker', 'nhersh', 'redwards']
```

---

## Task 4 — Finding the Data Type of a List Variable

**Code:**

```python
# Assign `username_list` to the list of usernames who are allowed to access the device

username_list = ["madebowa", "jnguyen", "tbecker", "nhersh", "redwards"]

# Assign `username_list_type` to the data type of `username_list`

username_list_type = type(username_list)

# Display `username_list_type`

print(username_list_type)
```

**Output:**

```
<class 'list'>
```

**Question 2 — What do you observe about the data type of `username_list`?**

The data type is `list`. A list in Python is an ordered collection of items enclosed in square brackets `[]`, where each item is separated by a comma. Lists are useful in security contexts for storing multiple related values — like a set of approved usernames — under a single variable name.

---

## Task 5 — Reassigning a Variable to an Updated List

**Code:**

```python
# Assign `username_list` to the list of usernames who are allowed to access the device

username_list = ["madebowa", "jnguyen", "tbecker", "nhersh", "redwards"]

# Display `username_list`

print(username_list)

# Assign `username_list` to the updated list of usernames who are allowed to access the device

username_list = ["madebowa", "jnguyen", "tbecker", "nhersh", "redwards", "lpope"]

# Display `username_list`

print(username_list)
```

**Output:**

```
['madebowa', 'jnguyen', 'tbecker', 'nhersh', 'redwards']
['madebowa', 'jnguyen', 'tbecker', 'nhersh', 'redwards', 'lpope']
```

**Question 3 — What do you observe about the contents of `username_list`?**

The first `print()` shows the original list with 5 usernames. After reassigning the variable, the second `print()` shows the updated list with 6 usernames, now including `"lpope"`. Reassigning a variable in Python simply overwrites the previous value — the variable now points to the new list entirely.

---

## Task 6 — Assigning an Integer Variable

**Code:**

```python
# Assign `max_logins` to the value 3

max_logins = 3

# Assign `max_logins_type` to the data type of `max_logins`

max_logins_type = type(max_logins)

# Display `max_logins_type`

print(max_logins_type)
```

**Output:**

```
<class 'int'>
```

**Question 4 — What do you observe about the data type of `max_logins`?**

The data type is `int` (integer). Integers represent whole numbers without a decimal point. Since `3` is a plain whole number with no quotes around it, Python identifies it as an integer, which is appropriate for storing a count like the maximum number of login attempts.

---

## Task 7 — Assigning Another Integer Variable

**Code:**

```python
# Assign `login_attempts` to the value 2

login_attempts = 2

# Assign `login_attempts_type` to the data type of `login_attempts`

login_attempts_type = type(login_attempts)

# Display `login_attempts_type`

print(login_attempts_type)
```

**Output:**

```
<class 'int'>
```

**Question 5 — What do you observe about the data type of `login_attempts`?**

The data type is also `int`. Just like `max_logins`, the current number of login attempts is a whole number, so Python assigns it the integer data type. Both variables being integers means they can be directly compared using operators like `<=`.

---

## Task 8 — Evaluating a Boolean Expression

**Code:**

```python
# Assign `max_logins` to the value 3

max_logins = 3

# Assign `login_attempts` to the value 2

login_attempts = 2

# Determine whether the current number of login attempts a user has made is less than or equal to
# the maximum number of login attempts allowed, and display the resulting Boolean value

print(login_attempts <= max_logins)
```

**Output:**

```
True
```

**Question 6 — What is the output? What does this mean?**

The output is `True`. This means the current number of login attempts (`2`) is less than or equal to the maximum allowed (`3`), so the user has not exceeded the login limit. In a real security system, a result of `True` here would mean the user is still within the allowed threshold and their session should continue normally.

---

## Task 9 — Observing How Boolean Output Changes

**Code:**

```python
# Assign `max_logins` to the value 3

max_logins = 3

# Assign `login_attempts` to a value higher than the max

login_attempts = 4

# Determine whether the current number of login attempts a user has made is less than or equal to
# the maximum number of login attempts allowed, and display the resulting Boolean value

print(login_attempts <= max_logins)
```

**Output:**

```
False
```

**Question 7 — Based on different values assigned to `login_attempts`, what did you observe about the output?**

- When `login_attempts` is **less than or equal to** `max_logins` (e.g., `2 <= 3`), the output is `True`.
- When `login_attempts` **exceeds** `max_logins` (e.g., `4 <= 3`), the output is `False`.

This demonstrates how comparison operators work in Python to produce Boolean results. In a security context, a `False` result would trigger a lockout or alert — the user has exceeded the maximum number of allowed login attempts.

---

## Task 10 — Assigning a Boolean Variable Directly

**Code:**

```python
# Assign `login_status` to the Boolean value False

login_status = False

# Assign `login_status_type` to the data type of `login_status`

login_status_type = type(login_status)

# Display `login_status_type`

print(login_status_type)
```

**Output:**

```
<class 'bool'>
```

**Question 8 — What do you observe about the data type of `login_status`?**

The data type is `bool` (Boolean). Boolean variables can only hold one of two values: `True` or `False`. Note that in Python, these values are capitalized and written without quotes — using quotes would make them strings, not Booleans. In a login system, a Boolean like `login_status` is perfect for representing binary states such as "logged in" or "not logged in."

---

## Conclusion

**Key takeaways from this lab:**

- Python supports multiple **data types** relevant to security work: `str` (strings), `list`, `int` (integers), and `bool` (Booleans).
- The **`type()` function** is used to check the data type of any variable.
- Variables are assigned using the `=` operator and can be **reassigned** at any time — the variable takes on the new value immediately.
- **Comparison operators** like `<=` evaluate expressions and return a Boolean result (`True` or `False`), which forms the basis of conditional logic in security automation.
- **Boolean values** (`True` / `False`) are written without quotes and are capitalized in Python — they represent binary states and are essential for decision-making in code.

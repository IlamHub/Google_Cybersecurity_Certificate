# Activity: Create More Functions

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Create More Functions
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

Built-in functions are functions that exist within Python and can be called directly. User-defined functions are functions that analysts write for their specific needs. Both types play an important role in security analysis — for example, helping identify suspicious patterns in login attempts.

In this lab, built-in functions are used to analyze a list of failed login attempts, and a custom function is progressively built and improved to compare a user's daily logins to their average.

---

## Scenario

As a security analyst, two responsibilities are addressed in this lab:

1. Working with a list of failed login attempts per month to identify anomalies.
2. Defining and refining a function that flags unusual login activity based on ratio analysis.

---

## Task 1 — Sorting the Failed Login List

**Code:**

```python
# Assign `failed_login_list` to the list of the number of failed login attempts per month

failed_login_list = [119, 101, 99, 91, 92, 105, 108, 85, 88, 90, 264, 223]

# Sort `failed_login_list` in ascending numerical order and display the result

print(sorted(failed_login_list))
```

**Output:**

```
[85, 88, 90, 91, 92, 99, 101, 105, 108, 119, 223, 264]
```

**Question 1 — What do you observe from the output? Do you notice any outlying numbers?**

After sorting, the list reveals that most months had failed login attempts in the range of 85–119. However, two values stand out significantly — `223` and `264` — which are far above the rest of the data. These are outliers that suggest a sharp spike in failed attempts during those two months (November and December based on the original chronological order). These months would warrant further investigation for potential malicious activity such as a brute-force attack or credential stuffing campaign.

---

## Task 2 — Finding the Maximum Value

**Code:**

```python
# Assign `failed_login_list` to the list of the number of failed login attempts per month

failed_login_list = [119, 101, 99, 91, 92, 105, 108, 85, 88, 90, 264, 223]

# Determine the highest number of failed login attempts from `failed_login_list` and display the result

print(max(failed_login_list))
```

**Output:**

```
264
```

**Question 2 — What do you observe from the output?**

The `max()` function returns `264`, identifying November as the month with the highest number of failed login attempts. This is the specific month that should be prioritized for further investigation. Using `max()` avoids the need to manually scan the list and instantly pinpoints the value of interest.

---

## Task 3 — Defining `analyze_logins()` with Two Parameters

**Code:**

```python
# Define a function named `analyze_logins()` that takes in two parameters, `username` and `current_day_logins`

def analyze_logins(username, current_day_logins):

    # Display a message about how many login attempts the user has made that day

    print("Current day login total for", username, "is", current_day_logins)
```

**Output:**

```
(no output — the function is only defined, not called)
```

The function header uses `def` followed by the function name and two parameters in the parentheses. The body contains a single `print()` statement that uses both parameters. No output is produced until the function is called.

---

## Task 4 — Calling `analyze_logins()`

**Code:**

```python
# Define a function named `analyze_logins()`

def analyze_logins(username, current_day_logins):

    # Display a message about how many login attempts the user has made that day

    print("Current day login total for", username, "is", current_day_logins)

# Call `analyze_logins()`

analyze_logins("ejones", 9)
```

**Output:**

```
Current day login total for ejones is 9
```

**Question 3 — What does this function display? Would the output vary for different users?**

The function displays a message combining the `username` and `current_day_logins` arguments passed into it. Yes, the output would vary for different users — calling `analyze_logins("bmoreno", 4)` would display `"Current day login total for bmoreno is 4"`. Parameters make functions reusable across different inputs without needing to rewrite the logic.

---

## Task 5 — Adding a Third Parameter

**Code:**

```python
# Define a function named `analyze_logins()` with three parameters

def analyze_logins(username, current_day_logins, average_day_logins):

    # Display a message about how many login attempts the user has made that day

    print("Current day login total for", username, "is", current_day_logins)

    # Display a message about average number of login attempts the user has made that day

    print("Average logins per day for", username, "is", average_day_logins)

# Call `analyze_logins()`

analyze_logins("ejones", 9, 3)
```

**Output:**

```
Current day login total for ejones is 9
Average logins per day for ejones is 3
```

A third parameter `average_day_logins` has been added to give context to the current day's login count. The function now prints two lines per call — one for the daily total and one for the average — giving a fuller picture of the user's login behavior.

---

## Task 6 — Calculating and Displaying the Login Ratio

**Code:**

```python
# Define a function named `analyze_logins()` with three parameters

def analyze_logins(username, current_day_logins, average_day_logins):

    # Display a message about how many login attempts the user has made that day

    print("Current day login total for", username, "is", current_day_logins)

    # Display a message about average number of login attempts the user has made that day

    print("Average logins per day for", username, "is", average_day_logins)

    # Calculate the ratio of current day logins to average day logins

    login_ratio = current_day_logins / average_day_logins

    # Display a message about the ratio

    print(username, "logged in", login_ratio, "times as much as they do on an average day.")

# Call `analyze_logins()`

analyze_logins("ejones", 9, 3)
```

**Output:**

```
Current day login total for ejones is 9
Average logins per day for ejones is 3
ejones logged in 3.0 times as much as they do on an average day.
```

**Question 4 — What does this version display? Would the output vary for different users?**

This version now calculates `login_ratio` by dividing `current_day_logins` by `average_day_logins` and displays it in a third message. The output would vary for different users depending on their specific values. For example, a user with `current_day_logins = 2` and `average_day_logins = 4` would show a ratio of `0.5`, indicating less-than-average activity. A ratio of `3.0` like ejones's, on the other hand, suggests significantly elevated activity that may deserve attention.

> **Note:** If `average_day_logins` is `0`, Python will raise a `ZeroDivisionError`. This lab assumes all users have logged in at least once, keeping the average above zero.

---

## Task 7 — Adding a `return` Statement

**Code:**

```python
# Define a function named `analyze_logins()` with a return statement

def analyze_logins(username, current_day_logins, average_day_logins):

    # Display a message about how many login attempts the user has made that day

    print("Current day login total for", username, "is", current_day_logins)

    # Display a message about average number of login attempts the user has made that day

    print("Average logins per day for", username, "is", average_day_logins)

    # Calculate the ratio of current day logins to average day logins

    login_ratio = current_day_logins / average_day_logins

    # Return the ratio

    return login_ratio

# Call `analyze_logins()` and store the output in `login_analysis`

login_analysis = analyze_logins("ejones", 9, 3)

# Display a message about the `login_analysis`

print("ejones", "logged in", login_analysis, "times as much as they do on an average day.")
```

**Output:**

```
Current day login total for ejones is 9
Average logins per day for ejones is 3
ejones logged in 3.0 times as much as they do on an average day.
```

**Question 5 — How does this version compare to the previous versions?**

The key difference is the addition of `return login_ratio`. In the previous version, the ratio was only displayed inside the function and then discarded — it couldn't be used anywhere else in the program. With `return`, the value is sent back to the caller and stored in `login_analysis`. This makes the function far more versatile — the returned value can now be used in further logic, comparisons, or passed into other functions, as demonstrated in the next task.

---

## Task 8 — Using the Returned Value in a Conditional

**Code:**

```python
# Define a function named `analyze_logins()` with a return statement

def analyze_logins(username, current_day_logins, average_day_logins):

    # Display a message about how many login attempts the user has made that day

    print("Current day login total for", username, "is", current_day_logins)

    # Display a message about average number of login attempts the user has made that day

    print("Average logins per day for", username, "is", average_day_logins)

    # Calculate the ratio of current day logins to average day logins

    login_ratio = current_day_logins / average_day_logins

    # Return the ratio

    return login_ratio

# Call `analyze_logins()` and store the output in `login_analysis`

login_analysis = analyze_logins("ejones", 9, 3)

# Conditional statement that displays an alert if login activity is more than normal

if login_analysis >= 3:
    print("Alert! This account has more login activity than normal.")
```

**Output:**

```
Current day login total for ejones is 9
Average logins per day for ejones is 3
Alert! This account has more login activity than normal.
```

Since `login_analysis` holds the returned value of `3.0`, the condition `login_analysis >= 3` evaluates to `True`, and the alert is triggered. This is the complete, practical version of the function — it analyzes login data, returns a usable ratio, and integrates with downstream logic to automatically flag suspicious behavior.

---

## Conclusion

**Key takeaways from this lab:**

- **Built-in functions** like `sorted()` and `max()` provide immediate, efficient tools for analyzing data without writing custom logic from scratch.
- **Parameters** make functions flexible and reusable — the same function can produce different output depending on the arguments passed in.
- Functions can be **incrementally improved** — starting simple and adding parameters, calculations, and logic over time as requirements grow.
- The **`return` statement** sends a value back to the caller, making the function's output available for use in the rest of the program — in variables, conditionals, or other function calls.
- Combining a **function with a return value** and a **conditional statement** is a powerful pattern for automating security decisions, such as flagging accounts with abnormally high login activity.
- A `ZeroDivisionError` will occur if a divisor is `0` — input validation should be considered in production code to guard against this.

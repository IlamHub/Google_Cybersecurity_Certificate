# Activity: Define and Call a Function

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Define and Call a Function
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

As a security analyst, when writing Python code to automate a task, you'll often find yourself needing to reuse the same block of code more than once. This is why functions are important — you can call a function whenever you need the computer to execute those steps. Python provides both built-in functions and the tools to define your own.

In this lab, defining and calling functions in Python is practiced.

---

## Scenario

Two functions are developed in this lab:

1. An `alert()` function that displays a security warning message.
2. A `list_to_string()` function that converts a list of approved usernames into a single formatted string.

---

## Task 1 — Analyzing a Function Definition

**Code:**

```python
# Define a function named `alert()`

def alert():
    print("Potential security issue. Investigate further.")
```

**Output:**

```
(no output — the function is only defined, not called)
```

**Question 1 — Summarize what the user-defined function above does.**

The function `alert()` is defined using the `def` keyword. When called, it will execute the indented body — which contains a single `print()` statement. The output would be:

```
Potential security issue. Investigate further.
```

At this stage, defining the function simply tells Python what steps to follow when `alert()` is invoked. No code in the body runs until the function is explicitly called.

---

## Task 2 — Calling the `alert()` Function

**Code:**

```python
# Define a function named `alert()`

def alert():
    print("Potential security issue. Investigate further.")

# Call the `alert()` function

alert()
```

**Output:**

```
Potential security issue. Investigate further.
```

**Question 2 — What are the advantages of placing this code in a function rather than running it directly?**

Wrapping code in a function provides several advantages:

- **Reusability** — `alert()` can be called as many times as needed anywhere in the program without rewriting the `print()` statement each time.
- **Maintainability** — if the alert message needs to change, it only needs to be updated in one place (the function definition), rather than in every location the code appears.
- **Readability** — a named function like `alert()` makes the intent of the code immediately clear to anyone reading it.
- **Organization** — grouping related logic inside a function keeps the program structured and easier to debug.

---

## Task 3 — Function with a `for` Loop Inside

**Code:**

```python
# Define a function named `alert()` with a loop inside

def alert():
    for i in range(3):
        print("Potential security issue. Investigate further.")

# Call the `alert()` function

alert()
```

**Output:**

```
Potential security issue. Investigate further.
Potential security issue. Investigate further.
Potential security issue. Investigate further.
```

**Question 3 — How does this output compare to the previous version of `alert()`?**

The previous version of `alert()` printed the message once. This version prints it three times because a `for` loop with `range(3)` has been added to the function body. The function definition is the only thing that changed — the way `alert()` is called remains identical (`alert()`). This demonstrates that functions can contain any Python structure, including loops, conditionals, or other function calls, making them flexible and powerful.

---

## Task 4 — Writing a Function Header

**Code:**

```python
# Define a function named `list_to_string()`

def list_to_string():
```

**Note:** Running this cell alone produces an error because the function body is empty. The body will be completed in the next task. The `def` keyword followed by the function name and parentheses is called the **function header** — it declares the function's name and signals that its body follows on the indented lines below.

---

## Task 5 — Building the Function Body with a Loop

**Code:**

```python
# Define a function named `list_to_string()`

def list_to_string():

  # Store the list of approved usernames in a variable named `username_list`

  username_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab", "gesparza", "alevitsk", "wjaffrey"]

  # Write a for loop that iterates through the elements of `username_list` and displays each element

  for i in username_list:
    print(i)

# Call the `list_to_string()` function

list_to_string()
```

**Output:**

```
elarson
bmoreno
tshah
sgilmore
eraab
gesparza
alevitsk
wjaffrey
```

**Question 4 — What do you observe from the output above?**

Each username from `username_list` is printed on its own separate line. The `for` loop iterates through each element of the list one at a time, assigning it to the loop variable `i`, and the `print(i)` statement displays it. While this successfully shows all usernames, the data is spread across 8 lines — not yet combined into a single string, which is the ultimate goal of this function.

---

## Task 6 — Using String Concatenation to Combine Usernames

**Code:**

```python
# Define a function named `list_to_string()`

def list_to_string():

  # Store the list of approved usernames in a variable named `username_list`

  username_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab", "gesparza", "alevitsk", "wjaffrey"]

  # Assign `sum_variable` to an empty string

  sum_variable = ""

  # Concatenate each username to `sum_variable` in each iteration

  for i in username_list:
    sum_variable = sum_variable + i

  # Display the value of `sum_variable`

  print(sum_variable)

# Call the `list_to_string()` function

list_to_string()
```

**Output:**

```
elarsonbmorenotshahsgilmoreeraabgesparzaalevitskwjaffrey
```

**Question 5 — What do you observe from the output above?**

All 8 usernames have been successfully merged into one single string using the `+` operator (string concatenation). However, the result is difficult to read — all the names are jammed together with no separator between them. The `sum_variable` starts as an empty string `""` and grows with each iteration as each username is appended to it. The next task will fix the readability issue.

---

## Task 7 — Adding a Separator for Readability

**Code:**

```python
# Define a function named `list_to_string()`

def list_to_string():

  # Store the list of approved usernames in a variable named `username_list`

  username_list = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab", "gesparza", "alevitsk", "wjaffrey"]

  # Assign `sum_variable` to an empty string

  sum_variable = ""

  # Concatenate each username followed by a comma and space to `sum_variable`

  for i in username_list:
    sum_variable = sum_variable + i + ", "

  # Display the value of `sum_variable`

  print(sum_variable)

# Call the `list_to_string()` function

list_to_string()
```

**Output:**

```
elarson, bmoreno, tshah, sgilmore, eraab, gesparza, alevitsk, wjaffrey, 
```

**Question 6 — What do you notice about the output from the function call this time?**

The output is now far more readable — each username is clearly separated from the next by a comma and a space (`", "`). The only minor side effect is a trailing `", "` at the very end of the string after the last username, since the separator is appended after every element including the last one. In a production setting, this trailing separator could be cleaned up using Python's `.rstrip(", ")` method or by using `", ".join(username_list)` as a more elegant approach. Despite this, the function now successfully converts a list into a clean, human-readable string.

---

## Conclusion

**Key takeaways from this lab:**

- A **function definition** uses the `def` keyword, followed by the function name, parentheses, and a colon. The indented lines below form the **function body**.
- A function does **not execute** until it is explicitly **called** by writing its name followed by parentheses (e.g., `alert()`).
- Functions can contain any Python structure — `print()` statements, `for` loops, conditionals, or other function calls — making them highly flexible.
- Wrapping reusable code in a function improves **readability**, **maintainability**, and **reusability** — changing the logic in one place updates all calls automatically.
- **String concatenation** using the `+` operator allows individual string values to be joined together into one larger string — useful for converting lists into formatted text.
- Starting with an **empty string variable** (`sum_variable = ""`) and appending to it inside a loop is a common pattern for building strings dynamically in Python.

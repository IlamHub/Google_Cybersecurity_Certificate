# Activity: Create Loops

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Create Loops
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

As a security analyst, some of the measures you take to protect a system will involve repetition. For example, you might need to investigate multiple IP addresses that have attempted to connect to the network. In Python, iterative statements help automate repetitive processes like these to make them more efficient.

In this lab, `for` loops and `while` loops are practiced in Python.

---

## Scenario

Programs are written in Python to automate the following security tasks:

- Displaying messages regarding network connection attempts
- Detecting IP addresses attempting to access restricted data
- Generating employee ID numbers for a Sales department

---

## Task 1 — `for` Loop with `range()`

**Code:**

```python
# Iterative statement using `for`, `range()`, and a loop variable of `i`
# Display "Connection could not be established." three times

for i in range(3):
    print("Connection could not be established.")
```

**Output:**

```
Connection could not be established.
Connection could not be established.
Connection could not be established.
```

---

## Task 2 — `for` Loop Using a Variable in `range()`

**Code:**

```python
# Create a variable called `connection_attempts` that stores the number of connection tries

connection_attempts = 3

# Iterative statement using `for`, `range()`, a loop variable of `i`, and `connection_attempts`
# Display "Connection could not be established." as many times as specified

for i in range(connection_attempts):
    print("Connection could not be established")
```

**Output:**

```
Connection could not be established
Connection could not be established
Connection could not be established
```

---

## Task 3 — `while` Loop Equivalent

**Code:**

```python
# Assign `connection_attempts` to an initial value of 0

connection_attempts = 0

# while loop that displays the message until connection_attempts reaches 3

while connection_attempts < 3:
    print("Connection could not be established")

    # Increment connection_attempts by 1 at the end of each iteration
    connection_attempts = connection_attempts + 1
```

**Output:**

```
Connection could not be established
Connection could not be established
Connection could not be established
```

**Question 1 — What do you observe about the differences between the `for` loop and the `while` loop?**

Both loops produce identical output, but the underlying logic differs:

- In the `for` loop, the loop variable `i` is automatically defined in the loop header and updated with each iteration — no manual tracking needed.
- In the `while` loop, the loop variable `connection_attempts` must be defined before the loop, and it must be manually incremented inside the loop body. If forgotten, the loop runs infinitely.

`for` loops are best when the number of iterations is known in advance. `while` loops are best when the loop should continue until a condition changes, regardless of how many iterations that takes.

---

## Task 4 — Iterating Over a List with a `for` Loop

**Code:**

```python
# Assign `ip_addresses` to a list of IP addresses from which users have tried to log in

ip_addresses = ["192.168.142.245", "192.168.109.50", "192.168.86.232", "192.168.131.147",
                "192.168.205.12", "192.168.200.48"]

# For loop that displays the elements of `ip_addresses` one at a time

for i in ip_addresses:
    print(i)
```

**Output:**

```
192.168.142.245
192.168.109.50
192.168.86.232
192.168.131.147
192.168.205.12
192.168.200.48
```

---

## Task 5 — Combining a `for` Loop with an `if`/`else` Statement

**Code:**

```python
# Assign `allow_list` to a list of IP addresses that are allowed to log in

allow_list = ["192.168.243.140", "192.168.205.12", "192.168.151.162", "192.168.178.71",
              "192.168.86.232", "192.168.3.24", "192.168.170.243", "192.168.119.173"]

# Assign `ip_addresses` to a list of IP addresses from which users have tried to log in

ip_addresses = ["192.168.142.245", "192.168.109.50", "192.168.86.232", "192.168.131.147",
                "192.168.205.12", "192.168.200.48"]

# For each IP address, check if it is in the allow list and display the result

for i in ip_addresses:
    if i in allow_list:
        print("IP address is allowed")
    else:
        print("IP address is not allowed")
```

**Output:**

```
IP address is not allowed
IP address is not allowed
IP address is allowed
IP address is not allowed
IP address is allowed
IP address is not allowed
```

---

## Task 6 — Using `break` to Stop the Loop on a Threat

**Code:**

```python
# Assign `allow_list` to a list of IP addresses that are allowed to log in

allow_list = ["192.168.243.140", "192.168.205.12", "192.168.151.162", "192.168.178.71",
              "192.168.86.232", "192.168.3.24", "192.168.170.243", "192.168.119.173"]

# Assign `ip_addresses` to a list of IP addresses from which users have tried to log in

ip_addresses = ["192.168.142.245", "192.168.109.50", "192.168.86.232", "192.168.131.147",
                "192.168.205.12", "192.168.200.48"]

# For each IP address, check if it is in the allow list
# If not allowed, display an alert and stop the loop immediately

for i in ip_addresses:
    if i in allow_list:
        print("IP address is allowed")
    else:
        print("IP address is not allowed. Further investigation of login activity required")
        break
```

**Output:**

```
IP address is not allowed. Further investigation of login activity required
```

The loop hits the first IP address (`192.168.142.245`), finds it is not in `allow_list`, prints the alert, and immediately exits via `break` — no further IPs are checked. This is appropriate when access to restricted data is involved and any unauthorized attempt warrants halting and escalating.

---

## Task 7 — `while` Loop to Generate Employee IDs

**Code:**

```python
# Assign the loop variable `i` to an initial value of 5000

i = 5000

# While loop that generates employee IDs divisible by 5, between 5000 and 5150 (inclusive)

while i <= 5150:
    print(i)
    i = i + 5
```

**Output:**

```
5000
5005
5010
5015
5020
5025
5030
5035
5040
5045
5050
5055
5060
5065
5070
5075
5080
5085
5090
5095
5100
5105
5110
5115
5120
5125
5130
5135
5140
5145
5150
```

---

## Task 8 — Adding an Alert Message Inside the Loop

**Code:**

```python
# Assign the loop variable `i` to an initial value of 5000

i = 5000

# While loop that generates employee IDs and displays an alert once i reaches 5100

while i <= 5150:
    print(i)
    if i == 5100:
        print("Only 10 valid employee ids remaining")
    i = i + 5
```

**Output:**

```
5000
5005
...
5095
5100
Only 10 valid employee ids remaining
5105
...
5150
```

**Question 2 — Why is `print(i)` written before the `if` statement rather than inside it?**

The goal is to display every employee ID generated across all iterations. If `print(i)` were placed inside the `if` block, it would only execute when `i == 5100`, meaning only one ID would ever be printed. By placing `print(i)` before the conditional, every ID is displayed regardless of whether the alert condition is met. The `if` block then independently checks if `i` has reached `5100` and appends the alert message at that specific point only.

---

## Conclusion

**Key takeaways from this lab:**

- **`for` loops** repeat a block of code a fixed number of times. They work with `range()` for numeric iteration or directly over a list to process each element.
- **`while` loops** repeat a block of code until a condition becomes `False`. They require manual initialization and updating of the loop variable — making them better suited for situations where the number of iterations is not known in advance.
- The **`in` operator** can be used inside a loop to check list membership on each iteration, enabling efficient allow-list checking across multiple IP addresses.
- The **`break` keyword** immediately exits a loop when triggered — useful in security contexts where a suspicious event should halt further processing and prompt investigation.
- **Nested conditionals inside loops** (`if`/`else` inside `for`/`while`) allow per-iteration decision-making, combining the power of iteration and logic in a single structure.
- Comparison operators used in `while` loop conditions include `<` (less than), `<=` (less than or equal to), and `==` (equal to).

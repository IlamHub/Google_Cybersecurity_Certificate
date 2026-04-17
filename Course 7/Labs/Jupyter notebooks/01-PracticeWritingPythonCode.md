# Activity: Practice Writing Python Code

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Practice Writing Python Code
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

Python is a programming language that helps in automating instructions to the computer in a variety of contexts, including security contexts. Writing code in Python is a valuable skill that helps security analysts thrive in their technical work.

In this lab, the basics of working inside a Jupyter notebook environment are explored, including writing code comments and displaying strings using the `print()` function.

---

## Task 1 — Editing a Markdown Cell

Notebook environments consist of two cell types:

- **Markdown cells** — for writing and formatting plain text
- **Code cells** — for writing and running Python code

**What was written in the markdown cell:**

> This is my first markdown cell. I am learning Python as part of the Google Cybersecurity Certificate. Markdown allows me to format text using plain-text syntax.

---

## Task 2 — Running a Pre-written Code Cell

**Code:**

```python
# This cell displays "Hello world!"

print("Hello world!")
```

**Output:**

```
Hello world!
```

**Question 1 — What do you observe about the output after running the code cell?**

The `print()` function outputs the string `"Hello world!"` to the screen. The comment above it (starting with `#`) does not appear in the output — only the result of the `print()` call is displayed.

---

## Task 3 — Observing That Comments Produce No Output

**Code:**

```python
# In Python, comments do not get displayed

# This code cell contains only comments
```

**Output:**

```
(no output)
```

**Question 2 — What do you observe about the output after running the cell?**

No output is produced. Python ignores lines that start with `#` — they are treated as comments and are not executed. Comments are purely for human readers to understand the code.

---

## Task 4 — Adding a Comment to a Code Cell

**Code:**

```python
# This cell displays "I am using Python."

print("I am using Python.")
```

**Output:**

```
I am using Python.
```

**Question 3 — What do you observe about the output after running the cell?**

The comment on the first line is ignored by Python and does not appear in the output. Only the `print()` statement executes, displaying the string `"I am using Python."` to the screen.

---

## Task 5 — Displaying a Custom Message with print()

**Code:**

```python
# This cell displays "I am a security analyst."

print("I am a security analyst.")
```

**Output:**

```
I am a security analyst.
```

**Question 4 — What do you observe about the output after running the cell?**

The `print()` function successfully displays the message `"I am a security analyst."`. The string passed inside the parentheses is what gets printed — the quotation marks define it as a string but are not shown in the output.

---

## Task 6 — Writing a print() Statement from Scratch

**Code:**

```python
# This cell displays "Python is useful for security!"

print("Python is useful for security!")
```

**Output:**

```
Python is useful for security!
```

**Question 5 — What do you observe about the output after running the cell?**

The custom `print()` statement works exactly as expected. The string `"Python is useful for security!"` is displayed. This demonstrates that `print()` can display any string passed to it.

---

## Task 7 — Combining All print() Statements

**Code:**

```python
# This cell displays all four messages from the lab

print("Hello world!")
print("I am using Python.")
print("I am a security analyst.")
print("Python is useful for security!")
```

**Output:**

```
Hello world!
I am using Python.
I am a security analyst.
Python is useful for security!
```

**Question 6 — What do you observe about the output after running the cell?**

All four `print()` statements execute in order from top to bottom, each printing its string on a new line. Python executes code sequentially, so the output appears in the same order the statements were written.

---

## Conclusion

**Key takeaways from this lab:**

- Jupyter notebooks support two cell types: **markdown cells** (for text/documentation) and **code cells** (for Python code).
- **Comments** in Python start with `#` and are ignored during execution — they exist only to explain the code to human readers.
- The **`print()` function** is used to display output to the screen. Any string passed inside the parentheses will be printed.
- Python executes code cells **line by line, top to bottom**.
- Writing clear comments alongside code is a professional standard that improves readability and collaboration.

---

## Lab Reference

**Coursera Lab :**
[Activity: Practice Writing Python Code]

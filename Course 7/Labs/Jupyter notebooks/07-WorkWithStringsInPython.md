# Activity: Work with Strings in Python

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Work with Strings in Python
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

Security analysts work with a lot of string data — employee IDs, device IDs, network activity logs, and URLs are all commonly represented as strings. Becoming comfortable working with strings in Python is essential for security analysis work.

In this lab, string creation, conversion, concatenation, indexing, slicing, and the `.index()` method are all practiced in the context of real security analyst tasks.

---

## Scenario

Three string-based tasks are automated in this lab:

1. Updating employee IDs to meet a new five-character standardized format.
2. Extracting specific characters from a device ID.
3. Parsing components from a URL string.

---

## Task 1 — Converting an Integer Employee ID to a String

**Code:**

```python
# Assign `employee_id` to a four digit number as an initial value

employee_id = 4186

# Display the data type of `employee_id`

print(type(employee_id))

# Reassign `employee_id` to the same value but in the form of a string

employee_id = str(employee_id)

# Display the data type of `employee_id` now

print(type(employee_id))
```

**Output:**

```
<class 'int'>
<class 'str'>
```

**Question 1 — What do you observe about the data type of `employee_id` the first time and second time it's displayed?**

The first time, `employee_id` is `4186` — an integer (`int`), since it was assigned as a plain number. After calling `str(employee_id)`, the variable is reassigned to the string `"4186"`. The second `type()` call confirms it is now a `str`. This conversion is necessary before string operations like concatenation or `len()` can be applied to the ID — neither works directly on integers.

---

## Task 2 — Checking ID Length with a Conditional

**Code:**

```python
# Assign `employee_id` to a four digit number as an initial value

employee_id = 4186

# Reassign `employee_id` to the same value but in the form of a string

employee_id = str(employee_id)

# Conditional statement that displays a message if the length of `employee_id` is less than five digits

if len(employee_id) < 5:
    print("This employee ID has less than five digits. It does not meet length requirements.")
```

**Output:**

```
This employee ID has less than five digits. It does not meet length requirements.
```

The `len()` function returns the number of characters in the string. Since `"4186"` has 4 characters, `len(employee_id) < 5` evaluates to `True` and the message is displayed.

---

## Task 3 — Padding the ID with Concatenation

**Code:**

```python
# Assign `employee_id` to a four digit number as an initial value

employee_id = 4186

# Reassign `employee_id` to the same value but in the form of a string

employee_id = str(employee_id)

# Display the `employee_id` as it currently stands

print(employee_id)

# Conditional statement that updates `employee_id` if its length is less than 5 digits

if len(employee_id) < 5:
    employee_id = "E" + employee_id

# Display the `employee_id` after the update

print(employee_id)
```

**Output:**

```
4186
E4186
```

When the condition is `True`, the string `"E"` is concatenated to the front of the existing employee ID using the `+` operator. The result is a five-character string `"E4186"` that now meets the new standardized format. Concatenation with `+` joins strings left to right, so `"E" + "4186"` produces `"E4186"`.

---

## Task 4 — Extracting the Fourth Character from a Device ID

**Code:**

```python
# Assign `device_id` to a string that contains alphanumeric characters

device_id = "r262c36"

# Extract the fourth character in `device_id` and display it

print(device_id[3])
```

**Output:**

```
2
```

Python uses **zero-based indexing**, meaning the first character is at index `0`. The fourth character is therefore at index `3`. In `"r262c36"`: index `0` = `r`, `1` = `2`, `2` = `6`, `3` = `2`. Bracket notation `device_id[3]` retrieves the character at that position.

---

## Task 5 — Slicing the First Three Characters

**Code:**

```python
# Assign `device_id` to a string that contains alphanumeric characters

device_id = "r262c36"

# Extract the first through the third characters in `device_id` and display the result

print(device_id[0:3])
```

**Output:**

```
r26
```

String slicing with `[start:stop]` extracts characters from `start` up to but **not including** `stop`. So `device_id[0:3]` returns characters at indices `0`, `1`, and `2` — which are `r`, `2`, and `6` — giving `"r26"`. This is a common pattern for extracting fixed-length prefixes from identifiers that encode structured information.

---

## Task 6 — Extracting the Protocol from a URL

**Code:**

```python
# Assign `url` to a specific URL

url = "https://exampleURL1.com"

# Extract the protocol of `url` along with the syntax following it, display the result

print(url[0:8])
```

**Output:**

```
https://
```

The protocol `"https"` occupies indices `0` through `4`, and `"://"` occupies indices `5` through `7`. The slice `[0:8]` captures all eight characters — `https://` — which is the full protocol prefix. Knowing these fixed positions allows analysts to reliably parse structured URL strings.

---

## Task 7 — Finding the Index of `.com` Using `.index()`

**Code:**

```python
# Assign `url` to a specific URL

url = "https://exampleURL1.com"

# Display the index where the domain extension ".com" is located in `url`

print(url.index(".com"))
```

**Output:**

```
19
```

The `.index()` method searches a string for a specified substring and returns the index of the **first character** of that substring. Here, `".com"` begins at index `19` in `"https://exampleURL1.com"`. This is useful when the exact position of a component is not known in advance and cannot be hardcoded.

---

## Task 8 — Storing the Index in a Variable

**Code:**

```python
# Assign `url` to a specific URL

url = "https://exampleURL1.com"

# Assign `ind` to the index where ".com" starts in `url`

ind = url.index(".com")
```

**Output:**

```
(no output — the value is stored in `ind` for later use)
```

Storing the index in a variable `ind` makes the code more flexible and readable. Instead of hardcoding `19` in every subsequent slice, `ind` is used — meaning the code will still work correctly if the URL changes and `.com` moves to a different position.

---

## Task 9 — Slicing the Domain Extension

**Code:**

```python
# Assign `url` to a specific URL

url = "https://exampleURL1.com"

# Assign `ind` to the index where ".com" starts in `url`

ind = url.index(".com")

# Extract the domain extension in `url` and display it

print(url[ind:ind+4])
```

**Output:**

```
.com
```

**Question 2 — What does this code output and why?**

The output is `".com"`. Since `ind = 19`, the slice `url[19:23]` is evaluated. This captures the four characters at indices `19`, `20`, `21`, and `22` — which are `.`, `c`, `o`, `m`. The ending index is expressed as `ind + 4` because `".com"` is exactly four characters long. This approach is more robust than hardcoding `url[19:23]` because it adapts automatically to different URLs where `.com` may appear at different positions.

---

## Task 10 — Extracting the Website Name

**Code:**

```python
# Assign `url` to a specific URL

url = "https://exampleURL1.com"

# Assign `ind` to the index where ".com" starts in `url`

ind = url.index(".com")

# Extract the website name in `url` and display it

print(url[8:ind])
```

**Output:**

```
exampleURL1
```

The website name `"exampleURL1"` sits between the `"https://"` prefix (which ends at index `8`) and the start of `".com"` (at index `ind = 19`). The slice `url[8:ind]` therefore extracts exactly the website name. Using `ind` as the endpoint instead of a hardcoded number ensures this works for any URL where the website name length varies.

---

## Conclusion

**Key takeaways from this lab:**

- The **`str()` function** converts other data types (like integers) into strings, enabling string operations such as `len()`, slicing, and concatenation.
- The **`len()` function** returns the number of characters in a string and is useful for enforcing format requirements like minimum ID length.
- **String concatenation** using `+` joins strings together — a clean way to prepend or append characters to build standardized identifiers.
- **String indexing** uses zero-based positions (e.g., `device_id[3]`) to retrieve a single character at a specific location.
- **String slicing** with `[start:stop]` extracts a substring from `start` up to but not including `stop` — useful for parsing fixed-format strings like device IDs and URLs.
- The **`.index()` method** locates the starting position of a substring within a string, enabling dynamic slicing when positions are not known in advance.
- Storing index values in variables (like `ind`) makes code more adaptable and readable, especially when the same position is referenced multiple times.

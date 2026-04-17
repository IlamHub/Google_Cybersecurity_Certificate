# Activity: Develop an Algorithm

**Course:** Google Cybersecurity Certificate — Automate Cybersecurity Tasks with Python
**Lab:** Develop an Algorithm
**Environment:** Jupyter Notebook (Google Coursera Lab)

---

## Introduction

An algorithm is a set of steps that can be used to solve a problem. Security analysts develop algorithms to automate decision-making processes — for example, verifying whether a user is approved to access a system and whether the device they've brought matches the one assigned to them.

In this lab, a complete login verification algorithm is built step by step in Python.

---

## Scenario

As a security analyst, an algorithm is developed that connects users to their assigned devices. The code checks whether a user is approved on the system and whether the device they present is the one assigned to them in the approved records.

---

## Task 1 — Exploring Synchronized Lists with Indices

**Code:**

```python
# Assign `approved_users` to a list of approved usernames

approved_users = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]

# Assign `approved_devices` to a list of device IDs that correspond to the usernames in `approved_users`

approved_devices = ["8rp2k75", "hl0s5o1", "2ye3lzg", "4n482ts", "a307vir"]

# Display the element at the specified index in `approved_users`

print(approved_users[0])

# Display the element at the specified index in `approved_devices`

print(approved_devices[0])
```

**Output:**

```
elarson
8rp2k75
```

**Question 1 — What did you observe about the output when index 0 is used? What happens when you replace 0 with another index?**

`approved_users[0]` returns `"elarson"` and `approved_devices[0]` returns `"8rp2k75"` — meaning `elarson` is the user and `8rp2k75` is their assigned device. The two lists are **synchronized**: the user at any index in `approved_users` corresponds to the device at the same index in `approved_devices`. Changing `0` to `2`, for example, returns `"tshah"` and `"2ye3lzg"` — the third user and their device. This synchronized structure is the foundation of the matching algorithm built in later tasks.

---

## Task 2 — Adding a New User with `.append()`

**Code:**

```python
approved_users = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
approved_devices = ["8rp2k75", "hl0s5o1", "2ye3lzg", "4n482ts", "a307vir"]

new_user = "gesparza"
new_device = "3rcv4w6"

# Add the new user's username and device ID to their respective lists

approved_users.append(new_user)
approved_devices.append(new_device)

# Display the contents of both lists

print(approved_users)
print(approved_devices)
```

**Output:**

```
['elarson', 'bmoreno', 'tshah', 'sgilmore', 'eraab', 'gesparza']
['8rp2k75', 'hl0s5o1', '2ye3lzg', '4n482ts', 'a307vir', '3rcv4w6']
```

**Question 2 — What did you observe after the new approved user was added?**

Both lists now have six elements. `"gesparza"` appears at the end of `approved_users` and `"3rcv4w6"` appears at the end of `approved_devices` — both at index `5`. The `.append()` method always adds the new element to the end of the list, preserving the synchronized relationship between both lists as long as both lists are updated together every time.

---

## Task 3 — Removing a Departed User with `.remove()`

**Code:**

```python
approved_users = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "2ye3lzg", "4n482ts", "a307vir", "3rcv4w6"]

removed_user = "tshah"
removed_device = "2ye3lzg"

# Remove the departed user's username and device ID from their respective lists

approved_users.remove(removed_user)
approved_devices.remove(removed_device)

# Display both updated lists

print(approved_users)
print(approved_devices)
```

**Output:**

```
['elarson', 'bmoreno', 'sgilmore', 'eraab', 'gesparza']
['8rp2k75', 'hl0s5o1', '4n482ts', 'a307vir', '3rcv4w6']
```

**Question 3 — What did you observe after the departed user was removed?**

`"tshah"` and `"2ye3lzg"` have been removed from their respective lists. Both lists now contain five elements, and the remaining users and devices remain synchronized at their correct indices. The `.remove()` method searches the list for the first occurrence of the specified value and deletes it. Just like with `.append()`, both lists must always be updated together to preserve synchronization.

---

## Task 4 — Checking if a Username is Approved

**Code:**

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "4n482ts", "a307vir", "3rcv4w6"]

username = "sgilmore"

# Conditional statement to check if the username is in the approved list

if username in approved_users:
    print("The username", username, "is approved to access the system.")
else:
    print("The username", username, "is not approved to access the system.")
```

**Output:**

```
The username sgilmore is approved to access the system.
```

**Question 4 — What message do you observe when `username` is `"sgilmore"`?**

Since `"sgilmore"` exists in `approved_users`, the `in` operator returns `True` and the approval message is displayed. If `username` were set to an unapproved name like `"tshah"`, the condition would be `False` and the `else` branch would execute instead, displaying the "not approved" message.

---

## Task 5 — Finding a Username's Index with `.index()`

**Code:**

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "4n482ts", "a307vir", "3rcv4w6"]

username = "sgilmore"

# Assign `ind` to the index of `username` in `approved_users`

ind = approved_users.index(username)

# Display the value of `ind`

print(ind)
```

**Output:**

```
2
```

**Question 5 — What do you observe when `username` is `"sgilmore"`?**

The `.index()` method returns `2`, meaning `"sgilmore"` is at position `2` in `approved_users` (zero-based indexing). Since the two lists are synchronized, index `2` in `approved_devices` will correspond to `"sgilmore"`'s assigned device — which will be used in the next task to verify the device match.

---

## Task 6 — Using the Index to Retrieve the Assigned Device

**Code:**

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "4n482ts", "a307vir", "3rcv4w6"]

username = "sgilmore"

# Assign `ind` to the index of `username` in `approved_users`

ind = approved_users.index(username)

# Display the device ID at the index that matches `ind` in `approved_devices`

print(approved_devices[ind])
```

**Output:**

```
4n482ts
```

**Question 6 — What do you observe when `username` is `"sgilmore"`?**

`approved_devices[2]` returns `"4n482ts"` — which is `sgilmore`'s assigned device. By using `ind` as a bridge between the two synchronized lists, the algorithm can look up any user's assigned device without needing a dictionary or any other data structure. This is the core lookup mechanism the full algorithm depends on.

---

## Task 7 — Verifying Both Username and Device ID Together

**Code:**

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "4n482ts", "a307vir", "3rcv4w6"]

username = "sgilmore"
device_id = "4n482ts"

ind = approved_users.index(username)

# Conditional: username must be approved AND device must match the assigned device

if username in approved_users and device_id == approved_devices[ind]:
    print("The username", username, "is approved to access the system.")
    print(device_id, "is the assigned device for", username)
```

**Output:**

```
The username sgilmore is approved to access the system.
4n482ts is the assigned device for sgilmore
```

**Question 7 — What do you observe when `username` is `"sgilmore"` and `device_id` is `"4n482ts"`?**

Both conditions are `True` — `"sgilmore"` is in `approved_users`, and `"4n482ts"` matches `approved_devices[2]`. The `and` operator requires both to be `True` for the block to execute. Both confirmation messages are displayed. If either condition were `False`, nothing would be printed (since no `else` branch exists yet at this stage).

---

## Task 8 — Handling a Device Mismatch with `elif`

**Code:**

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "4n482ts", "a307vir", "3rcv4w6"]

username = "sgilmore"
device_id = "4n482ts"

ind = approved_users.index(username)

# If approved and device matches

if username in approved_users and device_id == approved_devices[ind]:
    print("The user", username, "is approved to access the system.")
    print(device_id, "is the assigned device for", username)

# Elif: approved but wrong device

elif username in approved_users and device_id != approved_devices[ind]:
    print("The user", username, "is approved to access the system, but", device_id, "is not their assigned device.")
```

**Output (with correct device):**

```
The user sgilmore is approved to access the system.
4n482ts is the assigned device for sgilmore
```

**Output (with wrong device, e.g., `device_id = "8rp2k75"`):**

```
The user sgilmore is approved to access the system, but 8rp2k75 is not their assigned device.
```

**Question 8 — What do you observe when the device ID is correct vs. incorrect?**

With the correct device, the `if` block executes and both approval messages are displayed. With an incorrect device, the `elif` condition catches the case where the user is valid but the device doesn't match — and displays a tailored warning. This makes the system more informative, distinguishing between a completely unauthorized user and an authorized user who has presented the wrong device.

---

## Task 9 — Completing the Algorithm as a Function

**Code:**

```python
approved_users = ["elarson", "bmoreno", "sgilmore", "eraab", "gesparza"]
approved_devices = ["8rp2k75", "hl0s5o1", "4n482ts", "a307vir", "3rcv4w6"]

# Define the `login` function

def login(username, device_id):

    # Outer conditional: check if username is approved

    if username in approved_users:

        print("The user", username, "is approved to access the system.")

        # Find the index of the username in approved_users

        ind = approved_users.index(username)

        # Inner conditional: check if the device matches the assigned device

        if device_id == approved_devices[ind]:
            print(device_id, "is the assigned device for", username)
        else:
            print(device_id, "is not their assigned device.")

    # Outer else: username is not approved at all

    else:
        print("The username", username, "is not approved to access the system.")


# Test the function with different combinations

login("sgilmore", "4n482ts")
login("sgilmore", "8rp2k75")
login("tshah", "2ye3lzg")
```

**Output:**

```
The user sgilmore is approved to access the system.
4n482ts is the assigned device for sgilmore

The user sgilmore is approved to access the system.
8rp2k75 is not their assigned device.

The username tshah is not approved to access the system.
```

**Question 9 — After Python enters the inner conditional, what happens when the device ID is correct vs. incorrect?**

Once the outer `if` confirms the username is approved, Python enters the inner conditional to check the device:

- If `device_id == approved_devices[ind]`, the inner `if` is `True` and the "assigned device" confirmation is printed.
- If the device doesn't match, the inner `else` triggers and the "not their assigned device" warning is printed.

If the username is not approved at all, the outer `else` fires immediately and the inner conditional is never reached — Python does not check the device for an unapproved user. This nested structure efficiently separates the two verification layers.

---

## Conclusion

**Key takeaways from this lab:**

- **Synchronized lists** allow two lists to be used together as a lookup structure — the element at index `n` in one list corresponds to the element at index `n` in the other.
- **`.append()`** adds a new element to the end of a list — used to onboard new users while keeping both lists in sync.
- **`.remove()`** deletes the first matching element from a list — used to revoke access when a user leaves.
- **`.index()`** returns the position of a value in a list — the key tool for bridging two synchronized lists together.
- **Nested conditionals** allow multi-level decision logic: the outer conditional handles username approval, and the inner conditional handles device verification — making the logic clean and easy to follow.
- Wrapping the algorithm in a **function** (`login()`) makes it reusable, testable with different inputs, and easy to integrate into a larger security system.

# Lab: Filter a SQL Query

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47128741?parent=lti_session

## Environment

- Database: MariaDB
- Database Name: `organization`
- Shell: MariaDB shell
- Tables Used: `machines`, `employees`

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Unfiltered queries return everything — filtering lets you zero in on the specific machines, users, or events relevant to an investigation.
- `WHERE` clauses and pattern matching with `LIKE` are essential tools when triaging incidents, such as identifying which employees are affected by a compromised machine or which devices need an urgent patch.

---

## Task 1: List All Organization Machines

Retrieve the `device_id` and `operating_system` columns from the `machines` table.

```sql
SELECT device_id, operating_system
FROM machines;
```

**Expected Output (sample):**

```
+--------------+------------------+
| device_id    | operating_system |
+--------------+------------------+
| a184b775c707 | OS 1             |
| a192b174c940 | OS 2             |
| a305b818c708 | OS 3             |
...
200 rows in set
```

> **Q:** How many rows were returned?
> **A:** 200

---

## Task 2: Retrieve Machines with OS 2

Filter the results to return only machines running `OS 2`, which require an update.

```sql
SELECT device_id, operating_system
FROM machines
WHERE operating_system = 'OS 2';
```

> **Note:** The `WHERE` clause filters rows to only those that satisfy the specified condition. String values must be wrapped in single quotes.

**Expected Output (sample):**

```
+--------------+------------------+
| device_id    | operating_system |
+--------------+------------------+
| a192b174c940 | OS 2             |
| a320b137c219 | OS 2             |
...
80 rows in set
```

> **Q:** How many machines use OS 2?
> **A:** 80

---

## Task 3: List Employees in Specific Departments

### Filter by Finance Department

```sql
SELECT *
FROM employees
WHERE department = 'Finance';
```

> **Q:** What is the `employee_id` of the first row returned?
> **A:** 1003

---

### Filter by Sales Department

```sql
SELECT *
FROM employees
WHERE department = 'Sales';
```

> **Q:** How many employees work in the Sales department?
> **A:** 33

---

## Task 4: Identify Employee Machines

### Find the Employee in a Specific Office

A machine in `South-109` has an issue. Find out who uses it.

```sql
SELECT *
FROM employees
WHERE office = 'South-109';
```

> **Q:** Which employee uses the machine with the issue?
> **A:** `jlansky`

---

### Find All Employees in the South Building

Office names follow the format `Building-Number` (e.g., `South-109`). Use `LIKE` with the `%` wildcard to match all offices that start with `South`.

```sql
SELECT *
FROM employees
WHERE office LIKE 'South%';
```

> **Note:** The `LIKE` keyword enables pattern matching in SQL. The `%` wildcard represents any sequence of characters — placing it after `South` matches `South-109`, `South-203`, and so on. The `%` can be placed before, after, or on both sides of a substring.

> **Q:** Which department does the first employee in the South building belong to?
> **A:** Finance

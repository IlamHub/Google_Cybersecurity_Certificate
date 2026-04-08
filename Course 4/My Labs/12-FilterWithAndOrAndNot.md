# Lab: Filter with AND, OR, and NOT

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47128842?parent=lti_session

## Environment

- Database: MariaDB
- Database Name: `organization`
- Shell: MariaDB shell
- Tables Used: `log_in_attempts`, `employees`

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Security incidents rarely hinge on a single condition. You'll often need to combine filters — for example, failed logins AND after hours, or logins from a specific date OR the day before.
- Using `NOT` lets you quickly exclude known-safe categories (such as an already-patched department) and focus only on what still needs attention.

---

## Logical Operators Reference

| Operator | Behavior                                                     |
| -------- | ------------------------------------------------------------ |
| `AND`  | Returns rows where both conditions are true                  |
| `OR`   | Returns rows where at least one condition is true            |
| `NOT`  | Returns rows where the condition is false (excludes matches) |

---

## Task 1: Retrieve After-Hours Failed Login Attempts

Investigate failed logins that occurred after business hours (after 18:00).

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = FALSE;
```

> **Note:** Boolean values (`TRUE` / `FALSE`) are not wrapped in quotes — they are not strings. MySQL stores them as `1` (TRUE) and `0` (FALSE), so `success = 0` also works.

> **Q:** How many failed login attempts occurred after 18:00?
> **A:** 19

---

## Task 2: Retrieve Login Attempts on Specific Dates

Retrieve all login attempts from 2022-05-08 and 2022-05-09, the day of and the day before a suspicious event.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

> **Note:** Even though both conditions reference the same column, you must write the full condition each time — `login_date = '...'` cannot be shortened to a single expression with `OR`.

> **Q:** How many login attempts were made on these two days?
> **A:** 75

---

## Task 3: Retrieve Login Attempts Outside of Mexico

The `country` column contains both `MEX` and `MEXICO` as values. Use `NOT` with `LIKE` and the `MEX%` pattern to exclude all Mexican entries.

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

> **Note:** Combining `NOT` with `LIKE` excludes all rows that match the pattern, regardless of whether they say `MEX` or `MEXICO`.

> **Q:** How many login attempts were made outside of Mexico?
> **A:** 144

---

## Task 4: Retrieve Employees in Marketing (East Building)

Find Marketing department employees located in any East building office (e.g., `East-170`, `East-320`).

```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

> **Q:** What is the username of the first employee returned?
> **A:** `elarson`

---

## Task 5: Retrieve Employees in Finance or Sales

Locate employees in either the Finance or Sales department for a computer update.

```sql
SELECT *
FROM employees
WHERE department = 'Finance' OR department = 'Sales';
```

> **Note:** Both conditions must be written in full — you cannot write `WHERE department = 'Finance' OR 'Sales'`. The column name must be repeated for each condition.

> **Q:** What is the username of the first Sales department employee returned?
> **A:** `lrodriqu`

---

## Task 6: Retrieve All Employees Not in IT

The IT department has already been updated. Find all employees in other departments.

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

> **Q:** How many employees are not in the Information Technology department?
> **A:** 161

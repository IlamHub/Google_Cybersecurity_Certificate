# Lab: Complete a SQL Join

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47128878?parent=lti_session

## Environment

- Database: MariaDB
- Database Name: `organization`
- Shell: MariaDB shell
- Tables Used: `machines`, `employees`, `log_in_attempts`

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Security data is spread across multiple tables — user accounts, machines, and login activity are all separate.
- Joins let you cross-reference this data, for example: finding which employee owns a compromised machine, or listing every login attempt made by current staff.
- Understanding the difference between INNER, LEFT, and RIGHT joins prevents you from accidentally missing records that are critical to an investigation.

---

## SQL Joins Reference

| Join Type      | What It Returns                                                                   |
| -------------- | --------------------------------------------------------------------------------- |
| `INNER JOIN` | Only rows where the linking column has a match in both tables                     |
| `LEFT JOIN`  | All rows from the left table, plus matched rows from the right (NULL if no match) |
| `RIGHT JOIN` | All rows from the right table, plus matched rows from the left (NULL if no match) |

> When joining, always reference columns as `table.column` to avoid ambiguity when both tables share the same column name.

---

## Task 1: Match Employees to Their Machines

Both the `machines` and `employees` tables share a `device_id` column. Use an `INNER JOIN` to find only the machines that are assigned to an employee.

```sql
SELECT *
FROM machines
INNER JOIN employees ON machines.device_id = employees.device_id;
```

> **Note:** Only rows where `device_id` exists in both tables are returned. Machines with no assigned employee and employees with no assigned machine are excluded.

> **Q:** How many rows did the inner join return?
> **A:** 185

---

## Task 2: Return More Data

### Left Join — All Machines, With or Without an Employee

Returns every machine, including those not assigned to any employee. Unmatched employee columns show as `NULL`.

```sql
SELECT *
FROM machines
LEFT JOIN employees ON machines.device_id = employees.device_id;
```

> **Note:** The left table here is `machines` (referenced after `FROM`). All its rows are included regardless of whether a match exists in `employees`.

> **Q:** What is the username value in the last record returned?
> **A:** `NULL` — this machine has no assigned employee.

---

### Right Join — All Employees, With or Without a Machine

Returns every employee, including those not assigned to any machine. Unmatched machine columns show as `NULL`.

```sql
SELECT *
FROM machines
RIGHT JOIN employees ON machines.device_id = employees.device_id;
```

> **Note:** The right table here is `employees` (referenced after `RIGHT JOIN`). All its rows are included regardless of whether a match exists in `machines`.

> **Q:** What is the username value in the last record returned?
> **A:** `areyes`

---

## Task 3: Retrieve Login Attempt Data

Join the `employees` and `log_in_attempts` tables on the shared `username` column to retrieve all login attempts made by known employees.

```sql
SELECT *
FROM employees
INNER JOIN log_in_attempts ON employees.username = log_in_attempts.username;
```

> **Note:** Only employees who have at least one login attempt recorded are included in the result. Employees with no login attempts and log entries with unrecognized usernames are both excluded.

> **Q:** How many records are returned by this inner join?
> **A:** 200

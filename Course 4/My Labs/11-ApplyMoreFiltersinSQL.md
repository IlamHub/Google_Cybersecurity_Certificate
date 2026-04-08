# Lab: Apply More Filters in SQL

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47128789?parent=lti_session

## Environment

- Database: MariaDB
- Database Name: `organization`
- Shell: MariaDB shell
- Tables Used: `log_in_attempts`

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Filtering by date and time is critical when investigating security incidents — you need to isolate exactly when suspicious activity occurred.
- Filtering by event IDs helps you track specific log entries during forensic analysis.
- Using comparison operators precisely prevents pulling too much or too little data, which can slow down or mislead an investigation.

---

## Operators Reference

| Operator | Meaning                  |
| -------- | ------------------------ |
| `=`    | Equal to                 |
| `>`    | Greater than             |
| `<`    | Less than                |
| `<>`   | Not equal to             |
| `>=`   | Greater than or equal to |
| `<=`   | Less than or equal to    |

> **Note:** String and date/time values must be wrapped in single quotes. Numeric values must not be quoted.

---

## Task 1: Retrieve Login Attempts After a Certain Date

### Logins strictly after 2022-05-09

```sql
SELECT *
FROM log_in_attempts
WHERE login_date > '2022-05-09';
```

> **Q:** How many login attempts were made after 2022-05-09?
> **A:** 125

---

### Logins on or after 2022-05-09

```sql
SELECT *
FROM log_in_attempts
WHERE login_date >= '2022-05-09';
```

> **Q:** How many login attempts were made on or after 2022-05-09?
> **A:** 165

---

## Task 2: Retrieve Logins in a Date Range

Use `BETWEEN` and `AND` to filter within an inclusive date range.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date BETWEEN '2022-05-09' AND '2022-05-11';
```

> **Note:** `BETWEEN` is inclusive — it includes both the start and end values in the results.

> **Q:** How many login attempts were made between 2022-05-09 and 2022-05-11?
> **A:** 123

---

## Task 3: Investigate Logins at Certain Times

### Logins before 07:00:00

```sql
SELECT *
FROM log_in_attempts
WHERE login_time < '07:00:00';
```

> **Q:** What is the username of the fifth record returned?
> **A:** `eraab`

---

### Logins between 06:00:00 and 07:00:00

```sql
SELECT *
FROM log_in_attempts
WHERE login_time BETWEEN '06:00:00' AND '07:00:00';
```

> **Q:** What was the earliest login attempt in this time window?
> **A:** 06:01:31

---

## Task 4: Investigate Logins by Event ID

### Event IDs greater than or equal to 100

```sql
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id >= 100;
```

> **Note:** Numeric values do not use single quotes. Using quotes around numbers can cause unexpected behavior in comparisons.

> **Q:** What is the login date of the third result returned?
> **A:** 2022-05-09

---

### Event IDs between 100 and 150

```sql
SELECT event_id, username, login_date
FROM log_in_attempts
WHERE event_id BETWEEN 100 AND 150;
```

> **Q:** What is the username of the seventh result returned?
> **A:** `tmitchel`

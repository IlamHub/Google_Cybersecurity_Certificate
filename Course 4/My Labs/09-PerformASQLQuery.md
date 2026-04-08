# Lab: Perform a SQL Query

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47128701?parent=lti_session

## Environment

- Database: MariaDB
- Database Name: `organization`
- Shell: MariaDB shell
- Tables Used: `machines`, `log_in_attempts`

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- Security analysts regularly query databases to investigate login activity, identify compromised devices, and detect anomalies.
- Knowing how to retrieve and sort data efficiently helps you spot suspicious patterns quickly — such as logins from unexpected countries or outside working hours.

---

## Task 1: Retrieve Employee Device Data

### Select All Columns from the `machines` Table

```sql
SELECT *
FROM machines;
```

> **Note:** The `*` wildcard returns every column from the specified table. Table names in MySQL are case-sensitive.

**Expected Output (sample):**

```
+--------------+------------------+----------------+---------------+-------------+
| device_id    | operating_system | email_client   | OS_patch_date | employee_id |
+--------------+------------------+----------------+---------------+-------------+
| a184b775c707 | OS 1             | Email Client 1 | 2021-09-01    |        1156 |
| a192b174c940 | OS 2             | Email Client 1 | 2021-06-01    |        1052 |
| a305b818c708 | OS 3             | Email Client 2 | 2021-06-01    |        1182 |
...
200 rows in set
```

---

### Select Specific Columns: `device_id` and `email_client`

```sql
SELECT device_id, email_client
FROM machines;
```

> **Q:** What email client is returned in the third row?
> **A:** Email Client 2

---

### Select `device_id`, `operating_system`, and `OS_patch_date`

```sql
SELECT device_id, operating_system, OS_patch_date
FROM machines;
```

> **Q:** What is the patch date of the first entry?
> **A:** 2021-09-01

---

## Task 2: Investigate Login Activity

### Select `event_id` and `country` from `log_in_attempts`

```sql
SELECT event_id, country
FROM log_in_attempts;
```

> **Q:** Were any login attempts made from Australia?
> **A:** No

---

### Select `username`, `login_date`, and `login_time`

```sql
SELECT username, login_date, login_time
FROM log_in_attempts;
```

> **Q:** What username is returned in the fifth row?
> **A:** `jrafael`

---

### Select All Columns from `log_in_attempts`

```sql
SELECT *
FROM log_in_attempts;
```

---

## Task 3: Order Login Attempts Data

### Sort by `login_date`

```sql
SELECT *
FROM log_in_attempts
ORDER BY login_date;
```

> **Q:** What are the username and login date of the first record returned?
> **A:** `ivelasco` on `2022-05-08`

---

### Sort by `login_date`, then `login_time`

Multiple columns can be passed to `ORDER BY` — results are sorted by the first column, then ties are broken by the second.

```sql
SELECT *
FROM log_in_attempts
ORDER BY login_date, login_time;
```

> **Q:** What are the username and login time of the first record returned?
> **A:** `bsand` at `00:19:11`

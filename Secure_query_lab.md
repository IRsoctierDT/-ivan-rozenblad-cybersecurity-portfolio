# Secure Query Lab — Investigating Login Activity with SQL Filters

**Author:** Ivan Rozenblad
**Type:** SQL security lab / log investigation
**Environment:** Linux, MySQL/MariaDB
**Tables used:** `log_in_attempts`, `employees`

---

## Executive Summary

As a security analyst, I used SQL filters to investigate suspicious authentication
activity and to scope an upcoming security update. Working against the organization's
`log_in_attempts` and `employees` tables, I applied `WHERE` clauses with comparison
operators, pattern matching, and the logical operators `AND`, `OR`, and `NOT` to isolate
exactly the records relevant to each task. The result is a repeatable, least-effort
investigative workflow that returns only the rows an analyst needs — no manual scanning of
full tables.

---

## Objectives

- Retrieve failed login attempts that occurred **after business hours**.
- Retrieve all login attempts on a specific suspicious date.
- Retrieve login attempts that originated **outside an authorized country**.
- Scope a security update by selecting employees in specific departments or offices.

---

## Investigation & Queries

### 1. After-hours failed login attempts

Login attempts after 18:00 that failed are a strong indicator of unauthorized access
attempts. I filtered on both the timestamp and the success flag.

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = 0;
```

- `login_time > '18:00'` returns attempts after business hours.
- `success = 0` keeps only **failed** attempts.
- Both conditions are joined with `AND`, so a row must satisfy both.

### 2. All login attempts on a suspicious date

After a potential incident was flagged on a specific day, I needed every attempt on that
date plus the day before to establish context.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

- `OR` returns rows matching **either** date, widening the window around the event.

### 3. Login attempts outside an authorized country

The organization is based in a single country, so attempts from elsewhere warrant review.
Because the data stores the country both as `US` and `USA`, I excluded both spellings.

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country = 'US' AND NOT country = 'USA';
```

- `NOT` negates the condition, returning every attempt **not** from the United States.
- Combining two `NOT` conditions with `AND` accounts for the inconsistent country values.

### 4. Scoping a security update by department

To roll out a security update, I selected the employees in the affected departments.

```sql
-- Employees in the Marketing department, East offices only
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

- `LIKE 'East%'` matches any office whose name **starts with** "East" (the `%` wildcard
  matches the remaining characters).

```sql
-- Employees in either Sales or Finance
SELECT *
FROM employees
WHERE department = 'Sales' OR department = 'Finance';
```

```sql
-- All employees EXCEPT those in Information Technology
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

---

## Security Considerations

- **Least data exposure:** filters return only the rows needed for a task, limiting how
  much sensitive log data is pulled into an analyst's view.
- **Parameterize in production:** ad-hoc `WHERE` values here are for interactive
  investigation. Application code that builds these queries must use **parameterized
  queries / prepared statements** — never string concatenation — to prevent SQL injection.
- **Data normalization matters:** the `US` vs `USA` inconsistency shows why normalized,
  validated input improves both query accuracy and detection reliability.

---

## Results

| Task | Operator(s) used | Outcome |
|---|---|---|
| After-hours failed logins | `AND`, `>` | Isolated failed attempts after 18:00 |
| Suspicious-date attempts | `OR` | Returned all attempts across two dates |
| Out-of-country attempts | `NOT`, `AND` | Excluded both `US` and `USA` values |
| Department scoping | `AND`, `OR`, `NOT`, `LIKE` | Selected target employee sets for the update |

This workflow demonstrates using SQL filtering as a fast, precise first pass in log
investigation and in scoping security operations work.

---

*Performed in a controlled lab environment on a training dataset. No production or
personal data was used.*

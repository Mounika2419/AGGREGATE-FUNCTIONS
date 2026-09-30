# SQL Aggregate Functions and Grouping

## 📌 Description

This SQL program demonstrates the use of **aggregate functions** in MySQL.

Aggregate functions are used to perform calculations on a group of rows and return a **single result**.

The program demonstrates:

* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`
* `WHERE`
* `GROUP BY`
* `HAVING`
* Aggregate functions with conditions

---

# 🗄️ Database and Table Creation

```sql
SHOW DATABASES;

USE aids;

CREATE TABLE college(
    sid INT,
    sname VARCHAR(20),
    gpa DECIMAL(3,2),
    city VARCHAR(20)
);

DESC college;
```

### Explanation

### `SHOW DATABASES`

Displays all databases available in the MySQL server.

### `USE aids`

Selects the `aids` database.

> `USE college;` should not be used unless `college` is actually a **database**. In this program, `college` is the **table name**.

### `CREATE TABLE`

Creates a table named `college` with four columns:

| Column  | Data Type    | Description  |
| ------- | ------------ | ------------ |
| `sid`   | INT          | Student ID   |
| `sname` | VARCHAR(20)  | Student name |
| `gpa`   | DECIMAL(3,2) | Student GPA  |
| `city`  | VARCHAR(20)  | Student city |

### `DESC college`

Displays the structure of the `college` table.

---

# 📥 Inserting Records

```sql
INSERT INTO college VALUES(101,"ramu",9.2,"ong");
INSERT INTO college VALUES(102,"raju",9.2,"guntur");
INSERT INTO college VALUES(103,"ravi",8.4,"vijayawada");
INSERT INTO college VALUES(104,"meera",7.7,"kanigiri");
INSERT INTO college VALUES(106,"anil",8.7,"ongole");
INSERT INTO college VALUES(107,"rithu",7.5,"vijayawada");
INSERT INTO college VALUES(108,"harsha",7.8,"guntur");
```

These commands insert seven student records into the `college` table.

---

# 📋 Display All Records

```sql
SELECT * FROM college;
```

Displays all columns and all records from the table.

---

# 📊 What are Aggregate Functions?

**Aggregate functions** perform calculations on multiple rows and return a single value.

The main aggregate functions are:

| Function  | Purpose                   |
| --------- | ------------------------- |
| `COUNT()` | Counts the number of rows |
| `SUM()`   | Calculates the total      |
| `AVG()`   | Calculates the average    |
| `MIN()`   | Finds the minimum value   |
| `MAX()`   | Finds the maximum value   |

---

# 1. COUNT()

```sql
SELECT COUNT(*) FROM college;
```

`COUNT(*)` counts the total number of records in the table.

For the given data:

```text
7
```

So there are **7 students**.

---

# 2. SUM()

```sql
SELECT SUM(gpa) FROM college;
```

`SUM()` calculates the total of the GPA values.

It adds the GPA of all students.

---

# 3. AVG()

```sql
SELECT AVG(gpa) FROM college;
```

`AVG()` calculates the average GPA of all students.

Formula:

```text
Average = Sum of GPA / Number of students
```

---

# 4. MIN()

```sql
SELECT MIN(gpa) FROM college;
```

`MIN()` returns the smallest GPA.

For the given records:

```text
Minimum GPA = 7.5
```

---

# 5. MAX()

```sql
SELECT MAX(gpa) FROM college;
```

`MAX()` returns the highest GPA.

For the given records:

```text
Maximum GPA = 9.2
```

---

# ⚠️ Queries Using AGE

Your program contains:

```sql
SELECT MIN(age) FROM college;
SELECT MAX(age) FROM college;
SELECT SUM(age) FROM college;
SELECT AVG(age) FROM college;
```

These queries will produce an error because the `college` table contains:

```text
sid
sname
gpa
city
```

There is **no `age` column**.

You would get an error similar to:

```text
ERROR 1054 (42S22): Unknown column 'age' in 'field list'
```

### If you want to use AGE

Add the column first:

```sql
ALTER TABLE college ADD age INT;
```

Then you can use:

```sql
SELECT MIN(age) FROM college;
SELECT MAX(age) FROM college;
SELECT SUM(age) FROM college;
SELECT AVG(age) FROM college;
```

---

# 🔎 Aggregate Functions with WHERE

## Maximum GPA Greater Than 8

```sql
SELECT MAX(gpa)
FROM college
WHERE gpa > 8;
```

First, MySQL selects students whose GPA is greater than `8`.

Then `MAX()` finds the highest GPA among those students.

Result:

```text
9.2
```

---

## Maximum GPA Greater Than 10

```sql
SELECT MAX(gpa)
FROM college
WHERE gpa > 10;
```

There are no students with GPA greater than `10`.

Therefore, the result is:

```text
NULL
```

`NULL` means there is no matching value.

---

## Minimum GPA Greater Than 8

```sql
SELECT MIN(gpa)
FROM college
WHERE gpa > 8;
```

This finds the smallest GPA among students whose GPA is greater than `8`.

The matching GPAs are:

```text
9.2
9.2
8.4
8.7
```

Therefore:

```text
Minimum = 8.4
```

---

# 🏙️ GROUP BY

```sql
SELECT city, COUNT(*) AS address
FROM college
GROUP BY city;
```

`GROUP BY` groups rows having the same value.

Here, students are grouped according to their **city**.

The `COUNT(*)` function then counts students in each city.

### Example result

| City       | Address |
| ---------- | ------: |
| guntur     |       2 |
| kanigiri   |       1 |
| ong        |       1 |
| ongole     |       1 |
| vijayawada |       2 |

### What happens?

For example:

```text
guntur → raju, harsha → 2 students
vijayawada → ravi, rithu → 2 students
```

---

# 🔥 HAVING

```sql
SELECT city, COUNT(*) AS address
FROM college
GROUP BY city
HAVING COUNT(*) > 1;
```

`HAVING` is used to filter **groups** after `GROUP BY`.

This query displays only cities having **more than one student**.

### Result

| City       | Address |
| ---------- | ------: |
| guntur     |       2 |
| vijayawada |       2 |

---

# WHERE vs HAVING

This is an important SQL concept.

| WHERE                                | HAVING                                 |
| ------------------------------------ | -------------------------------------- |
| Filters individual rows              | Filters groups                         |
| Used before `GROUP BY`               | Used after `GROUP BY`                  |
| Commonly used with normal conditions | Commonly used with aggregate functions |

### Example of WHERE

```sql
SELECT *
FROM college
WHERE gpa > 8;
```

Filters individual students.

### Example of HAVING

```sql
SELECT city, COUNT(*)
FROM college
GROUP BY city
HAVING COUNT(*) > 1;
```

Filters groups of students based on their count.

---

# 🧠 Aggregate Function Summary

```text
COUNT() → Counts rows
SUM()   → Calculates total
AVG()   → Calculates average
MIN()   → Finds smallest value
MAX()   → Finds largest value
```

---

# 🎯 Objective

The objective of this program is to understand how SQL aggregate functions can be used to perform calculations on student data.

The program also demonstrates how `GROUP BY` can group records and how `HAVING` can filter those groups.

---

# 📚 Concepts Covered

* Database selection
* Table creation
* Data insertion
* `SELECT`
* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`
* `WHERE`
* `GROUP BY`
* `HAVING`
* `NULL`
* Aggregate functions with conditions

---

# ✅ Conclusion

This program demonstrates the basic use of **SQL aggregate functions** for analyzing student data. Functions such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()` make it easy to calculate statistics from multiple records.

`GROUP BY` is used to organize records into groups, while `HAVING` is used to filter those groups based on aggregate conditions.

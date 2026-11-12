# DBMS LAB RECORD - MySQL

**Scope:** SQL table creation, insertion, updation, filtering, aggregate functions, mathematical functions, logical operators, set operations and column aliases.

> This file contains GitHub-flavoured Markdown in plain text. It can be pasted directly into `lab.md` on GitHub.
>
> Run the SQL statements in order, using the same MySQL database. The examples use MySQL-compatible syntax. Statements such as `DROP TABLE IF EXISTS` are included where needed so that the exercises can be rerun without table-already-exists errors.

## Contents

1. [Creation, Insertion and Updation](#1-creation-insertion-and-updation)
2. [ALTER, RENAME and DROP](#2-alter-rename-and-drop)
3. [CHECK Constraint](#3-check-constraint)
4. [Query with a Literal String in the SELECT List](#4-query-with-a-literal-string-in-the-select-list)
5. [Filtering Clause](#5-filtering-clause)
6. [Aggregate Functions](#6-aggregate-functions)
7. [Mathematical Functions](#7-mathematical-functions)
8. [Logical Operators](#8-logical-operators)
9. [Set Operations](#9-set-operations)
10. [Aliases](#10-aliases)

---

## 1. Creation, Insertion and Updation

### A. Create a `supplier` table

**Question:** Create a table named `supplier` with the fields `supplier_id`, `name`, `address`, `city`, `country` and `ph_no`.

```sql
DROP TABLE IF EXISTS supplier;

CREATE TABLE supplier (
    supplier_id VARCHAR(5) PRIMARY KEY,
    name VARCHAR(10),
    address VARCHAR(100),
    city VARCHAR(30),
    country VARCHAR(30),
    ph_no VARCHAR(15)
);
```

### B. Display the table structure

**Question:** Display the description of the `supplier` table.

```sql
DESC supplier;
```

### C. Insert records into the table

```sql
INSERT INTO supplier
VALUES ('5001', 'David', 'Chennai', 'Chennai', 'India', '9496279381');

INSERT INTO supplier
VALUES ('5002', 'Antony', 'Kolkata', 'Kolkata', 'India', '7025589729');

INSERT INTO supplier
VALUES ('5003', 'Thomas', 'Pune', 'Pune', 'India', '80892710431');

INSERT INTO supplier
VALUES ('5004', 'Sam', 'Bangalore', 'Bangalore', 'India', '7025510332');
```

**Note:** `ph_no` is stored as `VARCHAR`, not `NUMERIC`, because a phone number is an identifier rather than a value used in calculations. This also allows different phone-number lengths and leading zeroes.

### D. Display all records

```sql
SELECT * FROM supplier;
```

### E. Update a record

**Question:** Change the phone number `7025589729` to `7025553142`.

```sql
UPDATE supplier
SET ph_no = '7025553142'
WHERE ph_no = '7025589729';
```

**Important:** Always use an appropriate `WHERE` condition with `UPDATE`. Without it, every row in the table will be updated.

---

## 2. ALTER, RENAME and DROP

### A. ALTER TABLE with ADD

**Question 1:** Add a `salary` column to the `supplier` table.

```sql
ALTER TABLE supplier
ADD COLUMN salary DECIMAL(10,2);
```

**Question 2:** Add an `email` column to the `supplier` table.

```sql
ALTER TABLE supplier
ADD COLUMN email VARCHAR(100);
```

### B. ALTER TABLE with DROP

**Question 1:** Remove the `salary` column from the `supplier` table.

```sql
ALTER TABLE supplier
DROP COLUMN salary;
```

**Question 2:** Remove the `email` column from the `supplier` table.

```sql
ALTER TABLE supplier
DROP COLUMN email;
```

### C. ALTER TABLE with MODIFY

**Question:** Change the size of the `name` column from `VARCHAR(10)` to `VARCHAR(15)` in the `supplier` table.

```sql
ALTER TABLE supplier
MODIFY COLUMN name VARCHAR(15);
```

### D. Rename a table

**Question:** Rename the table `supplier` to `supplier_details`.

```sql
RENAME TABLE supplier TO supplier_details;
```

### E. Drop a table

**Question:** Delete the table `supplier_details`.

```sql
DROP TABLE supplier_details;
```

> `DROP TABLE` permanently removes the table and its records. Run it only when you intend to delete the table.

---

## 3. CHECK Constraint

### A. Create a `customer` table with constraints

**Question:** Create a table named `customer` with the following fields and constraints.

| Field | Data type | Constraint |
|---|---|---|
| `cust_id` | `VARCHAR(5)` | Primary key; must start with `C` |
| `cust_name` | `VARCHAR(10)` | - |
| `revenue` | `DECIMAL(10,2)` | Cannot be `NULL` |
| `cust_type` | `VARCHAR(20)` | Must be `manufacturer`, `retailer`, `agent` or `wholesaler` |

```sql
DROP TABLE IF EXISTS customer;

CREATE TABLE customer (
    cust_id VARCHAR(5) PRIMARY KEY,
    cust_name VARCHAR(10),
    revenue DECIMAL(10,2) NOT NULL,
    cust_type VARCHAR(20) NOT NULL,
    CONSTRAINT chk_customer_id
        CHECK (cust_id LIKE 'C%'),
    CONSTRAINT chk_customer_type
        CHECK (cust_type IN ('manufacturer', 'retailer', 'agent', 'wholesaler'))
);
```

### B. Insert records into the `customer` table

```sql
INSERT INTO customer
VALUES ('C100', 'Roy', 100000, 'manufacturer');

INSERT INTO customer
VALUES ('C101', 'Richa', 180000, 'wholesaler');

INSERT INTO customer
VALUES ('C102', 'Rajesh', 120000, 'agent');

INSERT INTO customer
VALUES ('C103', 'Kalyani', 87000, 'wholesaler');

INSERT INTO customer
VALUES ('C104', 'Karthik', 55000, 'retailer');
```

### C. Display the table

```sql
SELECT * FROM customer;
```

**Constraint reminders:**

- `PRIMARY KEY` makes `cust_id` unique and not null.
- `NOT NULL` prevents `revenue` from being stored as `NULL`.
- `CHECK (cust_id LIKE 'C%')` requires the customer ID to begin with `C`.
- `CHECK (cust_type IN (...))` allows only the listed customer types.

**MySQL version note:** MySQL enforces `CHECK` constraints from MySQL 8.0.16 onwards. On older versions, a `CHECK` constraint may be parsed but not enforced. See the [MySQL Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/create-table-check-constraints.html).

---

## 4. Query with a Literal String in the SELECT List

### A. Create a `student` table

**Question:** Create a table named `student` with the fields `student_id`, `name` and `class`.

```sql
DROP TABLE IF EXISTS student;

CREATE TABLE student (
    student_id VARCHAR(5) PRIMARY KEY,
    name VARCHAR(10),
    class VARCHAR(5) NOT NULL
);
```

### B. Insert records into the table

```sql
INSERT INTO student VALUES ('S001', 'Achu', 'BSc');
INSERT INTO student VALUES ('S002', 'Soumya', 'BCA');
INSERT INTO student VALUES ('S003', 'Meera', 'BCA');
INSERT INTO student VALUES ('S004', 'Devu', 'BSc');
INSERT INTO student VALUES ('S005', 'Nandhu', 'BSc');
INSERT INTO student VALUES ('S006', 'Arunima', 'BCA');
INSERT INTO student VALUES ('S007', 'Anagha', 'BSc');
```

### C. Display a literal string in the SELECT list

**Question:** Display each student's ID, name and class, along with the same literal text for every row.

```sql
SELECT student_id, name, class, 'Student' AS category
FROM student;
```

**Explanation:** `'Student'` is a literal string. It is displayed as an additional column named `category` for every returned row. `AS category` gives that output column an alias.

---

## 5. Filtering Clause

### A. Filter student names using `LIKE`

The following queries use the `student` table created in Section 4.

**Question 1:** Display the details of students whose names start with `A`.

```sql
SELECT *
FROM student
WHERE name LIKE 'A%';
```

**Question 2:** Display the details of students whose names end with `a`.

```sql
SELECT *
FROM student
WHERE name LIKE '%a';
```

**Question 3:** Display the student ID and name of students whose names have the letter `u` in the third position.

```sql
SELECT student_id, name
FROM student
WHERE name LIKE '__u%';
```

**`LIKE` wildcards:**

- `%` matches zero or more characters.
- `_` matches exactly one character.
- In `'__u%'`, the first two underscores match any two characters, `u` must be the third character, and `%` matches the remaining characters.

### B. Create a student table for other filtering queries

The next exercise uses a different structure for the `student` table. The `DROP TABLE` statement avoids a table-already-exists error when running this file from top to bottom.

```sql
DROP TABLE IF EXISTS student;

CREATE TABLE student (
    roll_no INT PRIMARY KEY,
    name VARCHAR(30),
    gender CHAR(1),
    age INT,
    percentage DECIMAL(5,2)
);
```

### C. Insert records into the table

```sql
INSERT INTO student VALUES (1, 'George', 'M', 14, 85);
INSERT INTO student VALUES (2, 'Monica', 'F', 13, 85);
INSERT INTO student VALUES (3, 'Jessica', 'F', 14, 84);
INSERT INTO student VALUES (4, 'Tom', 'M', 13, 78);
```

### D. Display names without duplicates

**Question:** Display the student names without duplication.

```sql
SELECT DISTINCT name
FROM student;
```

### E. Display students whose percentage is between 80 and 90

```sql
SELECT *
FROM student
WHERE percentage BETWEEN 80 AND 90;
```

**Note:** `BETWEEN` includes both boundary values, 80 and 90.

### F. Display student details in ascending order of names

```sql
SELECT *
FROM student
ORDER BY name ASC;
```

### G. Display student details in descending order of names

```sql
SELECT *
FROM student
ORDER BY name DESC;
```

### H. Display students whose age is 14 or 15

```sql
SELECT *
FROM student
WHERE age IN (14, 15);
```

### I. Display the name and percentage of students whose names start with `M`

```sql
SELECT name, percentage
FROM student
WHERE name LIKE 'M%';
```

---

## 6. Aggregate Functions

### A. Create an `orders` table

**Question:** Create a table named `orders` with the fields `order_id`, `order_price` and `customer`.

```sql
DROP TABLE IF EXISTS orders;

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_price DECIMAL(10,2),
    customer VARCHAR(30)
);
```

> The table is named `orders` instead of `order` because `ORDER` is a MySQL keyword used in `ORDER BY`.

### B. Insert records into the table

```sql
INSERT INTO orders VALUES (1, 1000, 'Hanna');
INSERT INTO orders VALUES (2, 1600, 'Azad');
INSERT INTO orders VALUES (3, 2000, 'Ajin');
INSERT INTO orders VALUES (4, 700, 'Sreyas');
```

### C. Display the `orders` table

```sql
SELECT * FROM orders;
```

### D. Find the average order price

```sql
SELECT AVG(order_price) AS average_price
FROM orders;
```

### E. Find the total sum of order prices

```sql
SELECT SUM(order_price) AS total_order_price
FROM orders;
```

### F. Display the number of customers/orders

```sql
SELECT COUNT(customer) AS customer_count
FROM orders;
```

**Note:** `COUNT(column_name)` counts non-`NULL` values in that column. `COUNT(*)` counts all rows.

### G. Find the minimum order price

```sql
SELECT MIN(order_price) AS minimum_order_price
FROM orders;
```

### H. Find the customer name with the highest order price

```sql
SELECT customer
FROM orders
WHERE order_price = (
    SELECT MAX(order_price)
    FROM orders
);
```

### I. Find the order details with the minimum order price

```sql
SELECT *
FROM orders
WHERE order_price = (
    SELECT MIN(order_price)
    FROM orders
);
```

---

## 7. Mathematical Functions

### A. Find the absolute value of `-45`

```sql
SELECT ABS(-45) AS absolute_value;
```

**Result:** `45`

### B. Find the square root of `225`

```sql
SELECT SQRT(225) AS square_root;
```

**Result:** `15`

### C. Find the value of `10` raised to the power `2`

```sql
SELECT POWER(10, 2) AS power_value;
```

**Result:** `100`

### D. Find the remainder of `11 / 5`

```sql
SELECT MOD(11, 5) AS remainder;
```

**Result:** `1`

### E. Round `42.6` to the nearest integer

```sql
SELECT ROUND(42.6) AS rounded_value;
```

**Result:** `43`

### F. Round `98.2` up to the next integer

```sql
SELECT CEIL(98.2) AS ceiling_value;
```

**Result:** `99`

### G. Round `98.2` down to the integer below it

```sql
SELECT FLOOR(98.2) AS floor_value;
```

**Result:** `98`

---

## 8. Logical Operators

### A. Create a `student` table

**Question:** Create a table named `student` with the fields `roll_no`, `name`, `gender`, `age` and `percentage`.

> This exercise reuses the `student` table name with a different structure. The `DROP TABLE IF EXISTS` statement removes the table created in Section 5 before creating this version.

```sql
DROP TABLE IF EXISTS student;

CREATE TABLE student (
    roll_no INT PRIMARY KEY,
    name VARCHAR(30),
    gender CHAR(1),
    age INT,
    percentage DECIMAL(5,2)
);
```

### B. Insert records into the table

```sql
INSERT INTO student VALUES (1, 'George', 'M', 14, 85);
INSERT INTO student VALUES (2, 'Monica', 'F', 13, 85);
INSERT INTO student VALUES (3, 'Jessica', 'F', 14, 84);
INSERT INTO student VALUES (4, 'Tom', 'M', 13, 78);
```

### C. Display the `student` table

```sql
SELECT * FROM student;
```

### D. AND operator

**Question:** Display the name and percentage of students whose age is more than 12 and whose gender is female.

```sql
SELECT name, percentage
FROM student
WHERE age > 12 AND gender = 'F';
```

**Expected rows:** Monica and Jessica.

### E. Multiple AND operators

**Question:** Display the details of students whose age is more than 12, whose gender is female and whose percentage is more than 84.

```sql
SELECT *
FROM student
WHERE age > 12
  AND gender = 'F'
  AND percentage > 84;
```

**Expected row:** Monica.

### F. OR operator

**Question:** Display the name and percentage of students whose age is more than 12 or whose gender is male.

```sql
SELECT name, percentage
FROM student
WHERE age > 12 OR gender = 'M';
```

**Expected rows:** All four students, because every student in the sample data is older than 12.

### G. Multiple OR operators

**Question:** Display the details of students whose age is more than 13, whose gender is male or whose percentage is more than 80. Any one of these conditions is sufficient.

```sql
SELECT *
FROM student
WHERE age > 13
   OR gender = 'M'
   OR percentage > 80;
```

**Expected rows:** All four students.

### H. NOT operator

**Question 1:** Display the name and percentage of students whose gender is not female.

```sql
SELECT name, percentage
FROM student
WHERE NOT (gender = 'F');
```

**Expected rows:** George and Tom.

**Question 2:** Display the details of students whose gender is not male.

```sql
SELECT *
FROM student
WHERE NOT (gender = 'M');
```

**Expected rows:** Monica and Jessica.

**Logical operator reminders:**

- `AND` returns rows only when all specified conditions are true.
- `OR` returns rows when at least one specified condition is true.
- `NOT` reverses the result of a condition.

---

## 9. Set Operations

### A. Create the first table

**Question:** Create a table named `first_table` with the fields `roll_no` and `name`, and insert the given records.

```sql
DROP TABLE IF EXISTS first_table;
DROP TABLE IF EXISTS second_table;

CREATE TABLE first_table (
    roll_no INT PRIMARY KEY,
    name VARCHAR(30)
);

INSERT INTO first_table VALUES (1, 'Abhijith');
INSERT INTO first_table VALUES (2, 'Adam');
INSERT INTO first_table VALUES (3, 'Sheela');
```

### B. Display the first table

```sql
SELECT * FROM first_table;
```

### C. Create the second table

**Question:** Create a table named `second_table` with the fields `roll_no` and `name`, and insert the given records.

```sql
CREATE TABLE second_table (
    roll_no INT PRIMARY KEY,
    name VARCHAR(30)
);

INSERT INTO second_table VALUES (2, 'Adam');
INSERT INTO second_table VALUES (3, 'Sheela');
INSERT INTO second_table VALUES (4, 'Cletus');
```

### D. Display the second table

```sql
SELECT * FROM second_table;
```

### E. UNION operator

**Question:** Display the contents of both tables using the `UNION` operator.

```sql
SELECT roll_no, name FROM first_table
UNION
SELECT roll_no, name FROM second_table
ORDER BY roll_no;
```

**Explanation:** `UNION` combines the results and removes duplicate rows.

### F. UNION ALL operator

**Question:** Display the contents of both tables using the `UNION ALL` operator.

```sql
SELECT roll_no, name FROM first_table
UNION ALL
SELECT roll_no, name FROM second_table
ORDER BY roll_no;
```

**Explanation:** `UNION ALL` combines the results and keeps duplicate rows.

### G. INTERSECT operator

**Question:** Display the rows that are common to both tables using `INTERSECT`.

```sql
SELECT roll_no, name FROM first_table
INTERSECT
SELECT roll_no, name FROM second_table
ORDER BY roll_no;
```

**Expected rows:** `(2, 'Adam')` and `(3, 'Sheela')`.

### H. EXCEPT operator (MySQL equivalent of MINUS)

**Question:** Display the rows that are present in `first_table` but not in `second_table`.

```sql
SELECT roll_no, name FROM first_table
EXCEPT
SELECT roll_no, name FROM second_table
ORDER BY roll_no;
```

**Expected row:** `(1, 'Abhijith')`.

**MySQL version note:** MySQL supports `INTERSECT` and `EXCEPT` from MySQL 8.0.31 onwards. MySQL uses `EXCEPT`, not `MINUS`. On versions earlier than 8.0.31, use the following equivalent queries instead of the `INTERSECT` and `EXCEPT` statements above.

**Alternative for `INTERSECT` on older MySQL versions:**

```sql
SELECT f.roll_no, f.name
FROM first_table AS f
INNER JOIN second_table AS s
    ON f.roll_no = s.roll_no
   AND f.name = s.name
ORDER BY f.roll_no;
```

**Alternative for `EXCEPT` on older MySQL versions:**

```sql
SELECT f.roll_no, f.name
FROM first_table AS f
WHERE NOT EXISTS (
    SELECT 1
    FROM second_table AS s
    WHERE s.roll_no = f.roll_no
      AND s.name = f.name
)
ORDER BY f.roll_no;
```

**Set operation reminders:**

- The `SELECT` statements combined by a set operator must return the same number of columns, with compatible data types in corresponding positions.
- `UNION`, `INTERSECT` and `EXCEPT` remove duplicate rows by default.
- `UNION ALL` keeps duplicate rows.
- `EXCEPT` is directional: `A EXCEPT B` returns rows in `A` that are not in `B`.

See the [MySQL Reference Manual: Set Operations](https://dev.mysql.com/doc/refman/8.0/en/set-operations.html).

---

## 10. Aliases

### A. Create an `employee` table

**Question:** Create a table named `employee` with the fields `id`, `name` and `salary`, and display its contents.

```sql
DROP TABLE IF EXISTS employee;

CREATE TABLE employee (
    id INT PRIMARY KEY,
    name VARCHAR(30),
    salary DECIMAL(10,2)
);
```

### B. Insert records into the `employee` table

```sql
INSERT INTO employee VALUES (1, 'Athira', 2000);
INSERT INTO employee VALUES (2, 'Rajani', 10500);
INSERT INTO employee VALUES (3, 'Sheela', 18000);
INSERT INTO employee VALUES (4, 'Shamma', 9000);
```

### C. Display the contents of the `employee` table

```sql
SELECT * FROM employee;
```

### D. Display the average salary using the alias `AVERAGE`

```sql
SELECT AVG(salary) AS AVERAGE
FROM employee;
```

**Expected result:** `9875.00`

### E. Display the total salary using the alias `SUM`

```sql
SELECT SUM(salary) AS `SUM`
FROM employee;
```

**Expected result:** `39500.00`

### F. Increase each salary by 1500 and name the output column `NEW SALARY`

```sql
SELECT salary + 1500 AS `NEW SALARY`
FROM employee;
```

**Expected results:** `3500.00`, `12000.00`, `19500.00` and `10500.00`.

**Alias reminders:**

- An alias gives a temporary name to a column or expression in the query result.
- `AS` is optional in MySQL, but using it makes the alias easier to read.
- Use backticks around an alias that contains spaces, as in ``AS `NEW SALARY` ``.
- A column alias changes the displayed result heading; it does not rename the original table column.

---

## Quick Revision: Important SQL Commands and Functions

| Purpose | Syntax / Example |
|---|---|
| Create a table | `CREATE TABLE table_name (...);` |
| Insert a row | `INSERT INTO table_name VALUES (...);` |
| Display all rows | `SELECT * FROM table_name;` |
| Display table structure | `DESC table_name;` |
| Update records | `UPDATE table_name SET column = value WHERE condition;` |
| Add a column | `ALTER TABLE table_name ADD COLUMN column_name datatype;` |
| Modify a column | `ALTER TABLE table_name MODIFY COLUMN column_name datatype;` |
| Drop a column | `ALTER TABLE table_name DROP COLUMN column_name;` |
| Rename a table | `RENAME TABLE old_name TO new_name;` |
| Drop a table | `DROP TABLE table_name;` |
| Pattern matching | `WHERE column_name LIKE 'A%';` |
| Remove duplicate values | `SELECT DISTINCT column_name FROM table_name;` |
| Range filtering | `WHERE column_name BETWEEN value1 AND value2;` |
| Multiple-value filtering | `WHERE column_name IN (value1, value2);` |
| Ascending order | `ORDER BY column_name ASC;` |
| Descending order | `ORDER BY column_name DESC;` |
| AND condition | `WHERE condition1 AND condition2;` |
| OR condition | `WHERE condition1 OR condition2;` |
| NOT condition | `WHERE NOT (condition);` |
| UNION | `SELECT ... UNION SELECT ...;` |
| UNION ALL | `SELECT ... UNION ALL SELECT ...;` |
| INTERSECT | `SELECT ... INTERSECT SELECT ...;` |
| EXCEPT | `SELECT ... EXCEPT SELECT ...;` |
| Average | `AVG(column_name)` |
| Sum | `SUM(column_name)` |
| Count | `COUNT(*)` or `COUNT(column_name)` |
| Minimum | `MIN(column_name)` |
| Maximum | `MAX(column_name)` |
| Absolute value | `ABS(number)` |
| Square root | `SQRT(number)` |
| Power | `POWER(number, exponent)` |
| Remainder | `MOD(number, divisor)` |
| Round | `ROUND(number)` |
| Round up | `CEIL(number)` |
| Round down | `FLOOR(number)` |
| Column alias | `SELECT expression AS alias_name FROM table_name;` |

---

## Corrections Made to the Record

- Kept phone numbers as `VARCHAR` so they are treated as identifiers and can contain leading zeroes or different lengths.
- Used complete MySQL syntax for adding, modifying and dropping columns, renaming tables and updating records.
- Added `DROP TABLE IF EXISTS` before exercises that recreate a table, preventing table-already-exists errors during a top-to-bottom run.
- Kept the two different `student` table structures in separate exercises and explicitly dropped the earlier version before creating the next one.
- Used `DECIMAL(5,2)` for student percentages and `DECIMAL(10,2)` for salaries and prices so decimal values can be stored accurately.
- Corrected the logical-operator conditions to match the wording of the questions: “more than” is written with `>` rather than `>=`.
- Used distinct table names `first_table` and `second_table` for the set-operation exercise.
- Replaced the handwritten `MINUS` operator with MySQL's `EXCEPT` operator. MySQL supports `INTERSECT` and `EXCEPT` from version 8.0.31 onwards; alternatives for older versions are included.
- Corrected the salary increase result: `2000 + 1500 = 3500`, not `35000`.
- Used backticks for the alias `NEW SALARY` because the alias contains a space.
- Standardized SQL keywords, identifiers, capitalization, quotes, commas, parentheses and statement terminators.

**Scope note:** The uploaded PDF continues with later programs, but this file intentionally stops at Program 10 (Aliases), as requested.

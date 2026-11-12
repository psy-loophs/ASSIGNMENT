# DBMS LAB RECORD - MySQL

**Scope:** Creation, Insertion and Updation through Mathematical Functions.

> This file contains GitHub-flavoured Markdown in plain text. It can be pasted directly into `lab.md` on GitHub.
>
> Run the SQL statements in order, using the same database. The examples use MySQL-compatible syntax.

## Contents

1. [Creation, Insertion and Updation](#1-creation-insertion-and-updation)
2. [ALTER, RENAME and DROP](#2-alter-rename-and-drop)
3. [CHECK Constraint](#3-check-constraint)
4. [Query with a Literal String in the SELECT List](#4-query-with-a-literal-string-in-the-select-list)
5. [Filtering Clause](#5-filtering-clause)
6. [Aggregate Functions](#6-aggregate-functions)
7. [Mathematical Functions](#7-mathematical-functions)

---

## 1. Creation, Insertion and Updation

### A. Create a `supplier` table

**Question:** Create a table named `supplier` with the fields `supplier_id`, `name`, `address`, `city`, `country` and `ph_no`.

```sql
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
INSERT INTO student VALUES (2, 'Monica', 'F', 13, 88);
INSERT INTO student VALUES (3, 'Jessica', 'F', 14, 84);
INSERT INTO student VALUES (4, 'Tom', 'M', 13, 78);
INSERT INTO student VALUES (5, 'Tom', 'M', 14, 89);
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

---

## Corrections made to the handwritten record

- Changed the supplier phone-number column from `NUMERIC(10)` to `VARCHAR(15)`, because one supplied phone number has 11 digits and phone numbers should be stored as text.
- Corrected the `UPDATE` statement to compare and assign phone numbers as quoted strings.
- Made the initial supplier `name` column `VARCHAR(10)` so the later `MODIFY` example correctly changes it to `VARCHAR(15)`.
- Used complete MySQL syntax for dropping columns: `ALTER TABLE ... DROP COLUMN ...`.
- Corrected the table-renaming statement to `RENAME TABLE supplier TO supplier_details;`.
- Used `orders` instead of `order`, because `ORDER` is a MySQL keyword.
- Added `DROP TABLE IF EXISTS student;` before recreating `student` with a different structure, so the examples can be run in sequence.
- The handwritten section titled “Query with a Literal String in the SELECT List” did not contain a query demonstrating a literal string. Added a correct example using `'Student' AS category`.
- Standardized data types, column names, quoting, commas, parentheses and statement terminators.
- Corrected inconsistent supplier location entries so the city values are cities rather than state names.

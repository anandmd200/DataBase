# 🗄️ Complete Database Mastery: Beginner to Advanced Roadmap

## PHASE 1: FOUNDATION (Weeks 1-3)

---

### **Topic 1: What is a Database?**

A database is an organized collection of data stored electronically.

```
Real-life analogy:
📱 Phone Contact List = Simple Database

Name        | Phone        | Email
------------|------------- |------------------
John        | 123-456-7890 | john@email.com
Sarah       | 987-654-3210 | sarah@email.com
```

**Types of Databases:**
```
1. Relational Database (SQL)    → MySQL, PostgreSQL, Oracle, SQL Server
2. Non-Relational (NoSQL)       → MongoDB, Redis, Cassandra
3. In-Memory Database           → Redis, Memcached
4. Cloud Database               → Amazon RDS, Google Cloud SQL
```

---

### **Topic 2: RDBMS Concepts**

```
Key Terminologies:
┌─────────────────────────────────────────────┐
│  Table    → Collection of related data       │
│  Row      → A single record (tuple)          │
│  Column   → A field/attribute                │
│  Schema   → Structure/blueprint of database  │
│  Record   → Single entry in a table          │
└─────────────────────────────────────────────┘

Example Table: students
+----+--------+-----+-------+
| id | name   | age | grade |
+----+--------+-----+-------+
| 1  | Alice  | 20  | A     | ← Row (Record/Tuple)
| 2  | Bob    | 22  | B     |
| 3  | Charlie| 21  | A     |
+----+--------+-----+-------+
  ↑      ↑
Column  Column
```

---

### **Topic 3: Installing & Setting Up MySQL**

```bash
# Installation (Ubuntu)
sudo apt update
sudo apt install mysql-server

# Start MySQL
sudo service mysql start

# Login
mysql -u root -p

# For practice, you can also use:
# - db-fiddle.com (online)
# - sqliteonline.com (online)
# - XAMPP (local)
```

---

### **Topic 4: SQL Basics - DDL (Data Definition Language)**

```sql
-- ==========================================
-- CREATE DATABASE
-- ==========================================
CREATE DATABASE school;
USE school;

-- ==========================================
-- CREATE TABLE
-- ==========================================
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(150) UNIQUE,
    grade CHAR(1),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- ==========================================
-- SEE TABLE STRUCTURE
-- ==========================================
DESCRIBE students;
SHOW TABLES;

-- ==========================================
-- ALTER TABLE (Modify structure)
-- ==========================================
-- Add a column
ALTER TABLE students ADD COLUMN phone VARCHAR(15);

-- Modify a column
ALTER TABLE students MODIFY COLUMN name VARCHAR(200);

-- Drop a column
ALTER TABLE students DROP COLUMN phone;

-- Rename a column
ALTER TABLE students RENAME COLUMN grade TO letter_grade;

-- ==========================================
-- DROP & TRUNCATE
-- ==========================================
TRUNCATE TABLE students;  -- Deletes all rows, keeps structure
DROP TABLE students;      -- Deletes entire table
DROP DATABASE school;     -- Deletes entire database
```

---

### **Topic 5: Data Types**

```sql
-- ==========================================
-- NUMERIC TYPES
-- ==========================================
INT              -- Whole numbers: 1, 2, 100
BIGINT           -- Very large whole numbers
DECIMAL(10,2)    -- Exact decimal: 99999999.99
FLOAT            -- Approximate decimal

-- ==========================================
-- STRING TYPES
-- ==========================================
CHAR(10)         -- Fixed length string (always 10 chars)
VARCHAR(255)     -- Variable length string (up to 255)
TEXT             -- Long text (articles, descriptions)

-- ==========================================
-- DATE/TIME TYPES
-- ==========================================
DATE             -- '2024-01-15'
TIME             -- '14:30:00'
DATETIME         -- '2024-01-15 14:30:00'
TIMESTAMP        -- Auto-tracks time

-- ==========================================
-- OTHER
-- ==========================================
BOOLEAN          -- TRUE/FALSE
ENUM('A','B','C') -- Predefined set of values
BLOB             -- Binary data (images, files)

-- EXAMPLE TABLE WITH VARIOUS TYPES
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    salary DECIMAL(10, 2),
    hire_date DATE,
    is_active BOOLEAN DEFAULT TRUE,
    department ENUM('HR', 'IT', 'Sales', 'Marketing')
);
```

---

## PHASE 2: CRUD OPERATIONS (Weeks 3-5)

---

### **Topic 6: INSERT (Create Data)**

```sql
-- ==========================================
-- INSERT SINGLE ROW
-- ==========================================
INSERT INTO students (name, age, email, grade)
VALUES ('Alice', 20, 'alice@email.com', 'A');

-- ==========================================
-- INSERT MULTIPLE ROWS
-- ==========================================
INSERT INTO students (name, age, email, grade) VALUES
    ('Bob', 22, 'bob@email.com', 'B'),
    ('Charlie', 21, 'charlie@email.com', 'A'),
    ('Diana', 23, 'diana@email.com', 'C'),
    ('Eve', 20, 'eve@email.com', 'B'),
    ('Frank', 24, 'frank@email.com', 'A'),
    ('Grace', 22, 'grace@email.com', 'D'),
    ('Henry', 21, 'henry@email.com', 'B'),
    ('Ivy', 23, 'ivy@email.com', 'A'),
    ('Jack', 20, 'jack@email.com', 'C');

-- ==========================================
-- INSERT WITH ALL COLUMNS
-- ==========================================
INSERT INTO students
VALUES (11, 'Kate', 25, 'kate@email.com', 'A', NOW());
```

---

### **Topic 7: SELECT (Read Data)**

```sql
-- ==========================================
-- BASIC SELECT
-- ==========================================
SELECT * FROM students;                    -- All columns
SELECT name, age FROM students;            -- Specific columns
SELECT DISTINCT grade FROM students;       -- Unique values only

-- ==========================================
-- WHERE CLAUSE (Filtering)
-- ==========================================
SELECT * FROM students WHERE age = 20;
SELECT * FROM students WHERE age > 21;
SELECT * FROM students WHERE grade = 'A';
SELECT * FROM students WHERE name = 'Alice';

-- ==========================================
-- COMPARISON OPERATORS
-- ==========================================
SELECT * FROM students WHERE age >= 21;      -- Greater than or equal
SELECT * FROM students WHERE age != 22;      -- Not equal
SELECT * FROM students WHERE age <> 22;      -- Not equal (alternate)
SELECT * FROM students WHERE age BETWEEN 20 AND 22;  -- Range

-- ==========================================
-- LOGICAL OPERATORS
-- ==========================================
SELECT * FROM students WHERE age > 20 AND grade = 'A';
SELECT * FROM students WHERE age > 23 OR grade = 'A';
SELECT * FROM students WHERE NOT grade = 'D';

-- ==========================================
-- IN, LIKE, IS NULL
-- ==========================================
SELECT * FROM students WHERE grade IN ('A', 'B');
SELECT * FROM students WHERE name LIKE 'A%';     -- Starts with A
SELECT * FROM students WHERE name LIKE '%e';      -- Ends with e
SELECT * FROM students WHERE name LIKE '%ar%';    -- Contains 'ar'
SELECT * FROM students WHERE name LIKE '_o%';     -- Second char is 'o'
SELECT * FROM students WHERE email IS NULL;
SELECT * FROM students WHERE email IS NOT NULL;
```

---

### **Topic 8: UPDATE (Modify Data)**

```sql
-- ==========================================
-- UPDATE SINGLE RECORD
-- ==========================================
UPDATE students SET age = 25 WHERE id = 1;

-- ==========================================
-- UPDATE MULTIPLE COLUMNS
-- ==========================================
UPDATE students SET age = 26, grade = 'B' WHERE id = 1;

-- ==========================================
-- UPDATE MULTIPLE RECORDS
-- ==========================================
UPDATE students SET grade = 'A' WHERE age > 22;

-- ⚠️ WARNING: Without WHERE, ALL rows get updated!
UPDATE students SET grade = 'F';  -- DON'T DO THIS accidentally!
```

---

### **Topic 9: DELETE (Remove Data)**

```sql
-- ==========================================
-- DELETE SPECIFIC RECORDS
-- ==========================================
DELETE FROM students WHERE id = 5;
DELETE FROM students WHERE grade = 'D';
DELETE FROM students WHERE age > 23 AND grade = 'C';

-- ==========================================
-- DELETE ALL RECORDS
-- ==========================================
DELETE FROM students;        -- Removes all rows (can rollback)
TRUNCATE TABLE students;     -- Removes all rows (faster, no rollback)

-- ⚠️ Always use WHERE with DELETE!
```

---

## PHASE 3: INTERMEDIATE SQL (Weeks 5-8)

---

### **Topic 10: Sorting & Limiting Results**

```sql
-- ==========================================
-- ORDER BY (Sorting)
-- ==========================================
SELECT * FROM students ORDER BY name ASC;         -- A to Z
SELECT * FROM students ORDER BY age DESC;         -- Highest first
SELECT * FROM students ORDER BY grade ASC, age DESC;  -- Multiple sorts

-- ==========================================
-- LIMIT & OFFSET (Pagination)
-- ==========================================
SELECT * FROM students LIMIT 5;                   -- First 5 records
SELECT * FROM students LIMIT 5 OFFSET 5;          -- Records 6-10
SELECT * FROM students ORDER BY age DESC LIMIT 3;  -- Top 3 oldest
```

---

### **Topic 11: Aggregate Functions**

```sql
-- Setup: products table
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2),
    quantity INT
);

INSERT INTO products (name, category, price, quantity) VALUES
    ('Laptop', 'Electronics', 999.99, 50),
    ('Phone', 'Electronics', 699.99, 200),
    ('Tablet', 'Electronics', 499.99, 100),
    ('Desk', 'Furniture', 249.99, 30),
    ('Chair', 'Furniture', 199.99, 80),
    ('Headphones', 'Electronics', 149.99, 300),
    ('Bookshelf', 'Furniture', 179.99, 40),
    ('Mouse', 'Electronics', 29.99, 500),
    ('Keyboard', 'Electronics', 79.99, 400),
    ('Lamp', 'Furniture', 59.99, 150);

-- ==========================================
-- AGGREGATE FUNCTIONS
-- ==========================================
SELECT COUNT(*) FROM products;                    -- Total rows: 10
SELECT COUNT(*) FROM products WHERE category = 'Electronics'; -- 6

SELECT SUM(price) FROM products;                  -- Total of all prices
SELECT SUM(quantity) FROM products;               -- Total quantity

SELECT AVG(price) FROM products;                  -- Average price
SELECT MIN(price) FROM products;                  -- Cheapest: 29.99
SELECT MAX(price) FROM products;                  -- Most expensive: 999.99

-- Useful combination
SELECT
    COUNT(*) AS total_products,
    MIN(price) AS cheapest,
    MAX(price) AS most_expensive,
    AVG(price) AS average_price,
    SUM(quantity) AS total_stock
FROM products;
```

---

### **Topic 12: GROUP BY & HAVING**

```sql
-- ==========================================
-- GROUP BY
-- ==========================================
-- Count products per category
SELECT category, COUNT(*) AS total
FROM products
GROUP BY category;
-- Result:
-- Electronics | 6
-- Furniture   | 4

-- Average price per category
SELECT category, AVG(price) AS avg_price
FROM products
GROUP BY category;

-- Total stock per category
SELECT category, SUM(quantity) AS total_stock
FROM products
GROUP BY category;

-- ==========================================
-- HAVING (Filter AFTER grouping)
-- ==========================================
-- Categories with average price > 200
SELECT category, AVG(price) AS avg_price
FROM products
GROUP BY category
HAVING AVG(price) > 200;

-- ==========================================
-- WHERE vs HAVING
-- ==========================================
-- WHERE  → Filters BEFORE grouping
-- HAVING → Filters AFTER grouping

SELECT category, AVG(price) AS avg_price
FROM products
WHERE quantity > 50            -- Filter rows first
GROUP BY category
HAVING AVG(price) > 100;      -- Then filter groups

-- ==========================================
-- SQL EXECUTION ORDER
-- ==========================================
-- FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
```

---

### **Topic 13: Aliases & Concatenation**

```sql
-- ==========================================
-- COLUMN ALIASES
-- ==========================================
SELECT name AS product_name, price AS product_price FROM products;
SELECT name AS "Product Name", price AS "Unit Price" FROM products;

-- ==========================================
-- TABLE ALIASES
-- ==========================================
SELECT p.name, p.price FROM products AS p WHERE p.category = 'Electronics';

-- ==========================================
-- CONCAT
-- ==========================================
SELECT CONCAT(name, ' - $', price) AS product_info FROM products;
-- Output: "Laptop - $999.99"

SELECT CONCAT_WS(' | ', name, category, price) AS details FROM products;
-- Output: "Laptop | Electronics | 999.99"
```

---

## PHASE 4: CONSTRAINTS & KEYS (Weeks 8-10)

---

### **Topic 14: Constraints**

```sql
-- ==========================================
-- ALL CONSTRAINTS EXPLAINED
-- ==========================================
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,     -- PRIMARY KEY: Unique + Not Null
    email VARCHAR(150) UNIQUE,             -- UNIQUE: No duplicates allowed
    name VARCHAR(100) NOT NULL,            -- NOT NULL: Must have a value
    age INT CHECK (age >= 18),             -- CHECK: Must satisfy condition
    department VARCHAR(50) DEFAULT 'General', -- DEFAULT: Auto-fill value
    manager_id INT,
    FOREIGN KEY (manager_id) REFERENCES employees(id)  -- FOREIGN KEY
);

-- ==========================================
-- CONSTRAINT EXAMPLES
-- ==========================================
-- This will FAIL (NOT NULL violation):
INSERT INTO employees (name) VALUES (NULL);

-- This will FAIL (UNIQUE violation):
INSERT INTO employees (name, email) VALUES ('Alice', 'alice@mail.com');
INSERT INTO employees (name, email) VALUES ('Bob', 'alice@mail.com');  -- ERROR!

-- This will FAIL (CHECK violation):
INSERT INTO employees (name, age) VALUES ('Charlie', 15);  -- ERROR! age < 18

-- ==========================================
-- ADD/DROP CONSTRAINTS LATER
-- ==========================================
ALTER TABLE employees ADD CONSTRAINT chk_age CHECK (age >= 18);
ALTER TABLE employees DROP CONSTRAINT chk_age;

ALTER TABLE employees ADD UNIQUE (email);
ALTER TABLE employees MODIFY COLUMN name VARCHAR(100) NOT NULL;
```

---

### **Topic 15: Primary Key, Foreign Key & Relationships**

```sql
-- ==========================================
-- THREE TYPES OF RELATIONSHIPS
-- ==========================================

-- ┌────────────┐         ┌────────────┐
-- │ customers  │ 1 ── M  │  orders    │   ONE-TO-MANY
-- └────────────┘         └────────────┘
-- One customer can have many orders

-- ┌────────────┐         ┌────────────┐
-- │   users    │ 1 ── 1  │  profiles  │   ONE-TO-ONE
-- └────────────┘         └────────────┘
-- One user has one profile

-- ┌────────────┐         ┌────────────┐
-- │ students   │ M ── M  │  courses   │   MANY-TO-MANY
-- └────────────┘         └────────────┘
-- Students take multiple courses; courses have multiple students

-- ==========================================
-- ONE-TO-MANY EXAMPLE
-- ==========================================
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE
);

CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    amount DECIMAL(10, 2),
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Insert data
INSERT INTO customers (name, email) VALUES
    ('Alice', 'alice@mail.com'),
    ('Bob', 'bob@mail.com'),
    ('Charlie', 'charlie@mail.com');

INSERT INTO orders (order_date, amount, customer_id) VALUES
    ('2024-01-15', 250.00, 1),
    ('2024-01-20', 150.00, 1),
    ('2024-02-01', 300.00, 2),
    ('2024-02-10', 450.00, 3),
    ('2024-02-15', 200.00, 1);

-- ==========================================
-- MANY-TO-MANY EXAMPLE (Junction Table)
-- ==========================================
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100)
);

CREATE TABLE courses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(100)
);

-- Junction/Bridge table
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    PRIMARY KEY (student_id, course_id),  -- Composite Primary Key
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);

-- ==========================================
-- ON DELETE OPTIONS
-- ==========================================
-- CASCADE    → Delete child when parent is deleted
-- SET NULL   → Set foreign key to NULL
-- RESTRICT   → Prevent deletion of parent
-- NO ACTION  → Same as RESTRICT
-- SET DEFAULT → Set to default value
```

---

## PHASE 5: JOINS - The Most Important Topic! (Weeks 10-13)

---

### **Topic 16: JOINs**

```
Visual Reference:
┌─────────┐       ┌─────────┐
│ Table A │       │ Table B │
│  ┌───┐  │       │  ┌───┐  │
│  │   │──┼───────┼──│   │  │
│  │ A │  │       │  │ B │  │
│  │   │──┼───────┼──│   │  │
│  └───┘  │       │  └───┘  │
└─────────┘       └─────────┘

INNER JOIN:      Only matching records from BOTH tables
LEFT JOIN:       ALL from left + matching from right
RIGHT JOIN:      ALL from right + matching from left
FULL OUTER JOIN: ALL from both tables
CROSS JOIN:      Every combination (Cartesian product)
SELF JOIN:       Table joined with itself
```

```sql
-- ==========================================
-- SETUP DATA
-- ==========================================
CREATE TABLE departments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    dept_name VARCHAR(100)
);

CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    salary DECIMAL(10,2),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);

INSERT INTO departments VALUES
    (1, 'Engineering'),
    (2, 'Marketing'),
    (3, 'HR'),
    (4, 'Finance');     -- No employees in Finance

INSERT INTO employees VALUES
    (1, 'Alice', 80000, 1),
    (2, 'Bob', 75000, 1),
    (3, 'Charlie', 70000, 2),
    (4, 'Diana', 65000, 3),
    (5, 'Eve', 90000, 1),
    (6, 'Frank', 60000, NULL);  -- No department

-- ==========================================
-- INNER JOIN (Only matching records)
-- ==========================================
SELECT e.name, e.salary, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;

-- Result: (Frank is EXCLUDED - no dept, Finance EXCLUDED - no employees)
-- Alice   | 80000 | Engineering
-- Bob     | 75000 | Engineering
-- Charlie | 70000 | Marketing
-- Diana   | 65000 | HR
-- Eve     | 90000 | Engineering

-- ==========================================
-- LEFT JOIN (All employees, even without department)
-- ==========================================
SELECT e.name, e.salary, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;

-- Result: (Frank INCLUDED with NULL department)
-- Alice   | 80000 | Engineering
-- Bob     | 75000 | Engineering
-- Charlie | 70000 | Marketing
-- Diana   | 65000 | HR
-- Eve     | 90000 | Engineering
-- Frank   | 60000 | NULL         ← Included!

-- ==========================================
-- RIGHT JOIN (All departments, even without employees)
-- ==========================================
SELECT e.name, e.salary, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;

-- Result: (Finance INCLUDED with NULL employee)
-- Alice   | 80000 | Engineering
-- Bob     | 75000 | Engineering
-- Charlie | 70000 | Marketing
-- Diana   | 65000 | HR
-- Eve     | 90000 | Engineering
-- NULL    | NULL  | Finance      ← Included!

-- ==========================================
-- FULL OUTER JOIN (MySQL doesn't support directly)
-- ==========================================
SELECT e.name, e.salary, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id
UNION
SELECT e.name, e.salary, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;

-- ==========================================
-- CROSS JOIN (Every combination)
-- ==========================================
SELECT e.name, d.dept_name
FROM employees e
CROSS JOIN departments d;
-- 6 employees × 4 departments = 24 rows

-- ==========================================
-- SELF JOIN (Table joined with itself)
-- ==========================================
CREATE TABLE staff (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    manager_id INT
);

INSERT INTO staff VALUES
    (1, 'CEO', NULL),
    (2, 'CTO', 1),
    (3, 'Developer', 2),
    (4, 'Designer', 2),
    (5, 'Intern', 3);

SELECT
    s.name AS employee,
    m.name AS manager
FROM staff s
LEFT JOIN staff m ON s.manager_id = m.id;

-- Result:
-- CEO       | NULL
-- CTO       | CEO
-- Developer | CTO
-- Designer  | CTO
-- Intern    | Developer

-- ==========================================
-- MULTIPLE JOINS
-- ==========================================
CREATE TABLE projects (
    id INT PRIMARY KEY AUTO_INCREMENT,
    project_name VARCHAR(100),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);

INSERT INTO projects VALUES
    (1, 'Website Redesign', 1),
    (2, 'Marketing Campaign', 2),
    (3, 'Mobile App', 1);

-- Join 3 tables
SELECT
    e.name AS employee,
    d.dept_name AS department,
    p.project_name AS project
FROM employees e
JOIN departments d ON e.dept_id = d.id
JOIN projects p ON d.id = p.dept_id;
```

---

## PHASE 6: SUBQUERIES & ADVANCED SELECT (Weeks 13-16)

---

### **Topic 17: Subqueries (Nested Queries)**

```sql
-- ==========================================
-- SUBQUERY IN WHERE
-- ==========================================
-- Find employees earning above average
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Find employees in Engineering department
SELECT name FROM employees
WHERE dept_id = (SELECT id FROM departments WHERE dept_name = 'Engineering');

-- Find employees in departments that have projects
SELECT name FROM employees
WHERE dept_id IN (SELECT dept_id FROM projects);

-- ==========================================
-- SUBQUERY IN FROM (Derived Table)
-- ==========================================
SELECT dept_name, avg_salary
FROM (
    SELECT d.dept_name, AVG(e.salary) AS avg_salary
    FROM employees e
    JOIN departments d ON e.dept_id = d.id
    GROUP BY d.dept_name
) AS dept_averages
WHERE avg_salary > 70000;

-- ==========================================
-- SUBQUERY IN SELECT
-- ==========================================
SELECT
    name,
    salary,
    (SELECT AVG(salary) FROM employees) AS company_avg,
    salary - (SELECT AVG(salary) FROM employees) AS diff_from_avg
FROM employees;

-- ==========================================
-- EXISTS & NOT EXISTS
-- ==========================================
-- Departments that HAVE employees
SELECT dept_name FROM departments d
WHERE EXISTS (
    SELECT 1 FROM employees e WHERE e.dept_id = d.id
);

-- Departments with NO employees
SELECT dept_name FROM departments d
WHERE NOT EXISTS (
    SELECT 1 FROM employees e WHERE e.dept_id = d.id
);

-- ==========================================
-- CORRELATED SUBQUERY
-- ==========================================
-- Employees earning more than their department average
SELECT name, salary, dept_id
FROM employees e1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e2.dept_id = e1.dept_id
);
```

---

### **Topic 18: String Functions**

```sql
SELECT UPPER('hello');                     -- 'HELLO'
SELECT LOWER('HELLO');                     -- 'hello'
SELECT LENGTH('Hello');                    -- 5
SELECT TRIM('  Hello  ');                  -- 'Hello'
SELECT LTRIM('  Hello');                   -- 'Hello'
SELECT RTRIM('Hello  ');                   -- 'Hello'
SELECT SUBSTRING('Hello World', 1, 5);    -- 'Hello'
SELECT REPLACE('Hello World', 'World', 'SQL'); -- 'Hello SQL'
SELECT REVERSE('Hello');                   -- 'olleH'
SELECT LEFT('Hello', 3);                   -- 'Hel'
SELECT RIGHT('Hello', 3);                  -- 'llo'
SELECT LPAD('42', 5, '0');                -- '00042'
SELECT RPAD('Hi', 5, '!');                -- 'Hi!!!'
SELECT POSITION('World' IN 'Hello World'); -- 7
SELECT REPEAT('Ha', 3);                    -- 'HaHaHa'

-- Practical example
SELECT
    CONCAT(UPPER(LEFT(name, 1)), LOWER(SUBSTRING(name, 2))) AS proper_name
FROM employees;
```

---

### **Topic 19: Date & Time Functions**

```sql
SELECT NOW();                              -- 2024-07-15 14:30:00
SELECT CURDATE();                          -- 2024-07-15
SELECT CURTIME();                          -- 14:30:00
SELECT YEAR('2024-07-15');                 -- 2024
SELECT MONTH('2024-07-15');                -- 7
SELECT DAY('2024-07-15');                  -- 15
SELECT DAYNAME('2024-07-15');              -- Monday
SELECT MONTHNAME('2024-07-15');            -- July
SELECT DAYOFWEEK('2024-07-15');            -- 2 (1=Sunday)
SELECT DATEDIFF('2024-12-31', '2024-01-01'); -- 365
SELECT DATE_ADD('2024-01-01', INTERVAL 30 DAY);  -- 2024-01-31
SELECT DATE_SUB('2024-01-31', INTERVAL 1 MONTH); -- 2023-12-31
SELECT DATE_FORMAT('2024-07-15', '%d/%m/%Y');     -- 15/07/2024
SELECT DATE_FORMAT('2024-07-15', '%W, %M %d, %Y'); -- Monday, July 15, 2024

-- Practical: Orders from last 30 days
SELECT * FROM orders
WHERE order_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY);

-- Practical: Group orders by month
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS month,
    COUNT(*) AS total_orders,
    SUM(amount) AS total_revenue
FROM orders
GROUP BY DATE_FORMAT(order_date, '%Y-%m');
```

---

### **Topic 20: CASE Statement (Conditional Logic)**

```sql
-- ==========================================
-- SIMPLE CASE
-- ==========================================
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 85000 THEN 'Senior'
        WHEN salary >= 70000 THEN 'Mid-Level'
        WHEN salary >= 60000 THEN 'Junior'
        ELSE 'Intern'
    END AS level
FROM employees;

-- ==========================================
-- CASE IN UPDATE
-- ==========================================
UPDATE employees
SET salary = CASE
    WHEN dept_id = 1 THEN salary * 1.10   -- 10% raise for Engineering
    WHEN dept_id = 2 THEN salary * 1.05   -- 5% raise for Marketing
    ELSE salary * 1.03                     -- 3% raise for others
END;

-- ==========================================
-- CASE IN ORDER BY
-- ==========================================
SELECT * FROM employees
ORDER BY CASE dept_id
    WHEN 1 THEN 1
    WHEN 3 THEN 2
    WHEN 2 THEN 3
    ELSE 4
END;

-- ==========================================
-- CASE WITH AGGREGATE (Pivot-like)
-- ==========================================
SELECT
    SUM(CASE WHEN grade = 'A' THEN 1 ELSE 0 END) AS grade_a_count,
    SUM(CASE WHEN grade = 'B' THEN 1 ELSE 0 END) AS grade_b_count,
    SUM(CASE WHEN grade = 'C' THEN 1 ELSE 0 END) AS grade_c_count,
    SUM(CASE WHEN grade = 'D' THEN 1 ELSE 0 END) AS grade_d_count
FROM students;
```

---

### **Topic 21: UNION, INTERSECT, EXCEPT**

```sql
-- ==========================================
-- UNION (Combine results, remove duplicates)
-- ==========================================
SELECT name, 'Customer' AS type FROM customers
UNION
SELECT name, 'Employee' AS type FROM employees;

-- ==========================================
-- UNION ALL (Keep duplicates)
-- ==========================================
SELECT name FROM customers
UNION ALL
SELECT name FROM employees;

-- ==========================================
-- INTERSECT (Common records - MySQL workaround)
-- ==========================================
SELECT name FROM customers
WHERE name IN (SELECT name FROM employees);

-- ==========================================
-- EXCEPT (In A but not B - MySQL workaround)
-- ==========================================
SELECT name FROM customers
WHERE name NOT IN (SELECT name FROM employees);
```

---

## PHASE 7: ADVANCED SQL (Weeks 16-20)

---

### **Topic 22: Window Functions (VERY Important!)**

```sql
-- ==========================================
-- SETUP
-- ==========================================
CREATE TABLE sales (
    id INT PRIMARY KEY AUTO_INCREMENT,
    employee VARCHAR(50),
    department VARCHAR(50),
    sale_amount DECIMAL(10,2),
    sale_date DATE
);

INSERT INTO sales (employee, department, sale_amount, sale_date) VALUES
    ('Alice', 'Electronics', 5000, '2024-01-15'),
    ('Alice', 'Electronics', 3000, '2024-02-20'),
    ('Alice', 'Electronics', 7000, '2024-03-10'),
    ('Bob', 'Electronics', 4000, '2024-01-20'),
    ('Bob', 'Electronics', 6000, '2024-02-15'),
    ('Charlie', 'Clothing', 2000, '2024-01-10'),
    ('Charlie', 'Clothing', 3500, '2024-02-25'),
    ('Diana', 'Clothing', 4500, '2024-01-30'),
    ('Diana', 'Clothing', 2500, '2024-03-05'),
    ('Eve', 'Furniture', 8000, '2024-01-05'),
    ('Eve', 'Furniture', 6500, '2024-02-10');

-- ==========================================
-- ROW_NUMBER() - Sequential numbering
-- ==========================================
SELECT
    employee,
    department,
    sale_amount,
    ROW_NUMBER() OVER (ORDER BY sale_amount DESC) AS overall_rank,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY sale_amount DESC) AS dept_rank
FROM sales;

-- ==========================================
-- RANK() & DENSE_RANK()
-- ==========================================
-- RANK:       1, 2, 2, 4 (skips numbers)
-- DENSE_RANK: 1, 2, 2, 3 (no skip)

SELECT
    employee,
    sale_amount,
    RANK() OVER (ORDER BY sale_amount DESC) AS rank_val,
    DENSE_RANK() OVER (ORDER BY sale_amount DESC) AS dense_rank_val
FROM sales;

-- ==========================================
-- NTILE() - Divide into groups
-- ==========================================
SELECT
    employee,
    sale_amount,
    NTILE(4) OVER (ORDER BY sale_amount DESC) AS quartile
FROM sales;

-- ==========================================
-- SUM / AVG OVER - Running totals
-- ==========================================
SELECT
    employee,
    sale_date,
    sale_amount,
    SUM(sale_amount) OVER (ORDER BY sale_date) AS running_total,
    AVG(sale_amount) OVER (ORDER BY sale_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg_3
FROM sales;

-- ==========================================
-- LAG() & LEAD() - Previous/Next row values
-- ==========================================
SELECT
    employee,
    sale_date,
    sale_amount,
    LAG(sale_amount, 1) OVER (PARTITION BY employee ORDER BY sale_date) AS prev_sale,
    LEAD(sale_amount, 1) OVER (PARTITION BY employee ORDER BY sale_date) AS next_sale,
    sale_amount - LAG(sale_amount, 1) OVER (PARTITION BY employee ORDER BY sale_date) AS growth
FROM sales;

-- ==========================================
-- FIRST_VALUE() & LAST_VALUE()
-- ==========================================
SELECT
    employee,
    department,
    sale_amount,
    FIRST_VALUE(sale_amount) OVER (PARTITION BY department ORDER BY sale_amount DESC) AS highest_in_dept,
    sale_amount / FIRST_VALUE(sale_amount) OVER (PARTITION BY department ORDER BY sale_amount DESC) * 100 AS pct_of_highest
FROM sales;

-- ==========================================
-- PRACTICAL: Top 2 sales per department
-- ==========================================
SELECT * FROM (
    SELECT
        employee,
        department,
        sale_amount,
        ROW_NUMBER() OVER (PARTITION BY department ORDER BY sale_amount DESC) AS rn
    FROM sales
) ranked
WHERE rn <= 2;
```

---

### **Topic 23: Common Table Expressions (CTEs)**

```sql
-- ==========================================
-- BASIC CTE
-- ==========================================
WITH high_earners AS (
    SELECT name, salary, dept_id
    FROM employees
    WHERE salary > 70000
)
SELECT h.name, h.salary, d.dept_name
FROM high_earners h
JOIN departments d ON h.dept_id = d.id;

-- ==========================================
-- MULTIPLE CTEs
-- ==========================================
WITH dept_stats AS (
    SELECT
        dept_id,
        AVG(salary) AS avg_salary,
        COUNT(*) AS emp_count
    FROM employees
    GROUP BY dept_id
),
high_avg_depts AS (
    SELECT dept_id
    FROM dept_stats
    WHERE avg_salary > 70000
)
SELECT e.name, e.salary, d.dept_name
FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE e.dept_id IN (SELECT dept_id FROM high_avg_depts);

-- ==========================================
-- RECURSIVE CTE (Hierarchy)
-- ==========================================
WITH RECURSIVE org_chart AS (
    -- Base case: CEO (no manager)
    SELECT id, name, manager_id, 1 AS level,
           CAST(name AS CHAR(200)) AS path
    FROM staff
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive case: employees under managers
    SELECT s.id, s.name, s.manager_id, oc.level + 1,
           CONCAT(oc.path, ' → ', s.name)
    FROM staff s
    JOIN org_chart oc ON s.manager_id = oc.id
)
SELECT * FROM org_chart ORDER BY level;

-- Result:
-- 1 | CEO       | NULL | 1 | CEO
-- 2 | CTO       | 1    | 2 | CEO → CTO
-- 3 | Developer | 2    | 3 | CEO → CTO → Developer
-- 4 | Designer  | 2    | 3 | CEO → CTO → Designer
-- 5 | Intern    | 3    | 4 | CEO → CTO → Developer → Intern
```

---

### **Topic 24: Views**

```sql
-- ==========================================
-- CREATE VIEW
-- ==========================================
CREATE VIEW employee_details AS
SELECT
    e.id,
    e.name,
    e.salary,
    d.dept_name,
    CASE
        WHEN e.salary >= 80000 THEN 'Senior'
        WHEN e.salary >= 65000 THEN 'Mid'
        ELSE 'Junior'
    END AS level
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;

-- Use it like a table
SELECT * FROM employee_details;
SELECT * FROM employee_details WHERE level = 'Senior';

-- ==========================================
-- UPDATE VIEW
-- ==========================================
CREATE OR REPLACE VIEW employee_details AS
SELECT e.id, e.name, e.salary, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;

-- ==========================================
-- DROP VIEW
-- ==========================================
DROP VIEW IF EXISTS employee_details;

-- ==========================================
-- WITH CHECK OPTION
-- ==========================================
CREATE VIEW junior_employees AS
SELECT * FROM employees WHERE salary < 70000
WITH CHECK OPTION;

-- This prevents inserting/updating through the view
-- if the new data wouldn't be visible in the view
```

---

### **Topic 25: Indexes**

```sql
-- ==========================================
-- WHY INDEXES?
-- ==========================================
-- Without index: Full table scan (slow) → O(n)
-- With index:    Binary search (fast)   → O(log n)

-- Like a book's index page!

-- ==========================================
-- CREATE INDEX
-- ==========================================
CREATE INDEX idx_name ON employees(name);
CREATE INDEX idx_dept ON employees(dept_id);
CREATE UNIQUE INDEX idx_email ON employees(email);

-- Composite index (multiple columns)
CREATE INDEX idx_dept_salary ON employees(dept_id, salary);

-- ==========================================
-- VIEW INDEXES
-- ==========================================
SHOW INDEX FROM employees;

-- ==========================================
-- DROP INDEX
-- ==========================================
DROP INDEX idx_name ON employees;

-- ==========================================
-- WHEN TO USE INDEXES
-- ==========================================
-- ✅ Columns in WHERE clauses
-- ✅ Columns in JOIN conditions
-- ✅ Columns in ORDER BY
-- ✅ Columns with high selectivity (many unique values)
--
-- ❌ Small tables
-- ❌ Columns that change frequently
-- ❌ Columns with low selectivity (TRUE/FALSE)
-- ❌ Tables with heavy INSERT/UPDATE/DELETE

-- ==========================================
-- EXPLAIN - See query execution plan
-- ==========================================
EXPLAIN SELECT * FROM employees WHERE name = 'Alice';
EXPLAIN ANALYZE SELECT * FROM employees WHERE dept_id = 1;
```

---

## PHASE 8: DATABASE DESIGN (Weeks 20-23)

---

### **Topic 26: Normalization**

```
BEFORE NORMALIZATION (Messy Data):
┌────┬────────┬──────────────────────┬────────────────────────┐
│ id │ student│ courses              │ teachers               │
├────┼────────┼──────────────────────┼────────────────────────┤
│ 1  │ Alice  │ Math, Science        │ Mr. Smith, Mrs. Jones  │
│ 2  │ Bob    │ Math, English        │ Mr. Smith, Mr. Brown   │
└────┴────────┴──────────────────────┴────────────────────────┘
Problems: Repetition, hard to update, hard to search
```

```sql
-- ==========================================
-- 1NF: No repeating groups, atomic values
-- ==========================================
-- Each cell has ONE value, each row is unique
CREATE TABLE student_courses_1nf (
    id INT,
    student VARCHAR(50),
    course VARCHAR(50),
    teacher VARCHAR(50),
    PRIMARY KEY (id, course)
);
-- id | student | course  | teacher
-- 1  | Alice   | Math    | Mr. Smith
-- 1  | Alice   | Science | Mrs. Jones
-- 2  | Bob     | Math    | Mr. Smith
-- 2  | Bob     | English | Mr. Brown

-- ==========================================
-- 2NF: Remove partial dependencies
-- ==========================================
-- All non-key columns depend on FULL primary key
CREATE TABLE students_2nf (
    id INT PRIMARY KEY,
    student_name VARCHAR(50)
);

CREATE TABLE courses_2nf (
    id INT PRIMARY KEY,
    course_name VARCHAR(50),
    teacher VARCHAR(50)
);

CREATE TABLE enrollments_2nf (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES students_2nf(id),
    FOREIGN KEY (course_id) REFERENCES courses_2nf(id)
);

-- ==========================================
-- 3NF: Remove transitive dependencies
-- ==========================================
-- Non-key columns depend ONLY on primary key
CREATE TABLE courses_3nf (
    id INT PRIMARY KEY,
    course_name VARCHAR(50),
    teacher_id INT,
    FOREIGN KEY (teacher_id) REFERENCES teachers(id)
);

CREATE TABLE teachers (
    id INT PRIMARY KEY,
    teacher_name VARCHAR(50),
    department VARCHAR(50)
);

-- ==========================================
-- Summary:
-- 1NF → Atomic values, no repeating groups
-- 2NF → 1NF + No partial dependencies
-- 3NF → 2NF + No transitive dependencies
-- BCNF → 3NF + Every determinant is a candidate key
-- ==========================================
```

---

### **Topic 27: ER Diagrams (Entity-Relationship)**

```
E-Commerce Database Design:

┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   USERS      │     │   ORDERS     │     │ ORDER_ITEMS  │
├──────────────┤     ├──────────────┤     ├──────────────┤
│ PK id        │────<│ PK id        │────<│ PK id        │
│    name      │     │ FK user_id   │     │ FK order_id  │
│    email     │     │    total     │     │ FK product_id│
│    password  │     │    status    │     │    quantity   │
│    created_at│     │    order_date│     │    price     │
└──────────────┘     └──────────────┘     └──────────────┘
                                                │
                                                │
┌──────────────┐     ┌──────────────┐           │
│  CATEGORIES  │     │  PRODUCTS    │───────────┘
├──────────────┤     ├──────────────┤
│ PK id        │────<│ PK id        │
│    name      │     │ FK category_id│
│    description│     │    name      │
└──────────────┘     │    price     │
                     │    stock     │
                     │    description│
                     └──────────────┘
```

```sql
-- FULL E-COMMERCE DATABASE
CREATE DATABASE ecommerce;
USE ecommerce;

CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE categories (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    description TEXT
);

CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(200) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    stock INT DEFAULT 0,
    category_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);

CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    total DECIMAL(10,2),
    status ENUM('pending', 'processing', 'shipped', 'delivered', 'cancelled')
        DEFAULT 'pending',
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE order_items (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(id)
);

CREATE TABLE reviews (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    product_id INT NOT NULL,
    rating INT CHECK (rating BETWEEN 1 AND 5),
    comment TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (product_id) REFERENCES products(id),
    UNIQUE KEY unique_review (user_id, product_id)
);
```

---

## PHASE 9: TRANSACTIONS & STORED PROCEDURES (Weeks 23-26)

---

### **Topic 28: Transactions & ACID**

```sql
-- ==========================================
-- ACID PROPERTIES
-- ==========================================
-- A - Atomicity:    All or nothing
-- C - Consistency:  Data stays valid
-- I - Isolation:    Concurrent transactions don't interfere
-- D - Durability:   Committed data is permanent

-- ==========================================
-- TRANSACTION EXAMPLE: Bank Transfer
-- ==========================================
CREATE TABLE accounts (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    balance DECIMAL(10,2)
);

INSERT INTO accounts VALUES
    (1, 'Alice', 1000.00),
    (2, 'Bob', 500.00);

-- Transfer $200 from Alice to Bob
START TRANSACTION;

UPDATE accounts SET balance = balance - 200 WHERE id = 1;
UPDATE accounts SET balance = balance + 200 WHERE id = 2;

-- Check everything is correct
SELECT * FROM accounts;

-- If everything is fine:
COMMIT;

-- If something went wrong:
-- ROLLBACK;

-- ==========================================
-- SAVEPOINT
-- ==========================================
START TRANSACTION;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
SAVEPOINT after_debit;

UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- Oops, something wrong with the credit
ROLLBACK TO after_debit;

-- Fix and try again
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- ==========================================
-- ISOLATION LEVELS
-- ==========================================
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;  -- Dirty reads allowed
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;    -- No dirty reads
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;   -- Default in MySQL
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;      -- Strictest, slowest
```

---

### **Topic 29: Stored Procedures**

```sql
-- ==========================================
-- BASIC STORED PROCEDURE
-- ==========================================
DELIMITER //
CREATE PROCEDURE GetAllEmployees()
BEGIN
    SELECT * FROM employees;
END //
DELIMITER ;

-- Call it
CALL GetAllEmployees();

-- ==========================================
-- WITH PARAMETERS
-- ==========================================
DELIMITER //
CREATE PROCEDURE GetEmployeesByDept(IN dept_id_param INT)
BEGIN
    SELECT * FROM employees WHERE dept_id = dept_id_param;
END //
DELIMITER ;

CALL GetEmployeesByDept(1);

-- ==========================================
-- WITH OUTPUT PARAMETER
-- ==========================================
DELIMITER //
CREATE PROCEDURE GetDeptAvgSalary(
    IN dept_id_param INT,
    OUT avg_salary DECIMAL(10,2)
)
BEGIN
    SELECT AVG(salary) INTO avg_salary
    FROM employees
    WHERE dept_id = dept_id_param;
END //
DELIMITER ;

CALL GetDeptAvgSalary(1, @avg);
SELECT @avg;

-- ==========================================
-- COMPLEX PROCEDURE WITH LOGIC
-- ==========================================
DELIMITER //
CREATE PROCEDURE TransferMoney(
    IN from_account INT,
    IN to_account INT,
    IN amount DECIMAL(10,2),
    OUT result VARCHAR(50)
)
BEGIN
    DECLARE from_balance DECIMAL(10,2);

    -- Check balance
    SELECT balance INTO from_balance FROM accounts WHERE id = from_account;

    IF from_balance < amount THEN
        SET result = 'Insufficient funds';
    ELSE
        START TRANSACTION;
        UPDATE accounts SET balance = balance - amount WHERE id = from_account;
        UPDATE accounts SET balance = balance + amount WHERE id = to_account;
        COMMIT;
        SET result = 'Transfer successful';
    END IF;
END //
DELIMITER ;

CALL TransferMoney(1, 2, 200.00, @result);
SELECT @result;

-- ==========================================
-- DROP PROCEDURE
-- ==========================================
DROP PROCEDURE IF EXISTS GetAllEmployees;
```

---

### **Topic 30: Functions (User-Defined)**

```sql
-- ==========================================
-- CREATE FUNCTION
-- ==========================================
DELIMITER //
CREATE FUNCTION CalculateTax(salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    DECLARE tax DECIMAL(10,2);

    IF salary > 80000 THEN
        SET tax = salary * 0.30;
    ELSEIF salary > 60000 THEN
        SET tax = salary * 0.20;
    ELSE
        SET tax = salary * 0.10;
    END IF;

    RETURN tax;
END //
DELIMITER ;

-- Use it
SELECT name, salary, CalculateTax(salary) AS tax,
       salary - CalculateTax(salary) AS net_salary
FROM employees;

-- DROP
DROP FUNCTION IF EXISTS CalculateTax;
```

---

### **Topic 31: Triggers**

```sql
-- ==========================================
-- AUDIT LOG WITH TRIGGERS
-- ==========================================
CREATE TABLE salary_audit (
    id INT PRIMARY KEY AUTO_INCREMENT,
    employee_id INT,
    old_salary DECIMAL(10,2),
    new_salary DECIMAL(10,2),
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    action VARCHAR(20)
);

-- BEFORE UPDATE trigger
DELIMITER //
CREATE TRIGGER before_salary_update
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    IF OLD.salary != NEW.salary THEN
        INSERT INTO salary_audit (employee_id, old_salary, new_salary, action)
        VALUES (OLD.id, OLD.salary, NEW.salary, 'UPDATE');
    END IF;
END //
DELIMITER ;

-- Now any salary update is automatically logged
UPDATE employees SET salary = 95000 WHERE id = 1;
SELECT * FROM salary_audit;

-- ==========================================
-- AFTER INSERT trigger
-- ==========================================
DELIMITER //
CREATE TRIGGER after_order_insert
AFTER INSERT ON order_items
FOR EACH ROW
BEGIN
    -- Automatically reduce stock
    UPDATE products
    SET stock = stock - NEW.quantity
    WHERE id = NEW.product_id;
END //
DELIMITER ;

-- ==========================================
-- VIEW & DROP TRIGGERS
-- ==========================================
SHOW TRIGGERS;
DROP TRIGGER IF EXISTS before_salary_update;
```

---

## PHASE 10: PERFORMANCE & OPTIMIZATION (Weeks 26-28)

---

### **Topic 32: Query Optimization**

```sql
-- ==========================================
-- EXPLAIN ANALYZE
-- ==========================================
EXPLAIN SELECT * FROM employees WHERE name = 'Alice';
EXPLAIN ANALYZE SELECT * FROM employees WHERE dept_id = 1;

-- ==========================================
-- OPTIMIZATION TIPS
-- ==========================================

-- ❌ BAD: SELECT *
SELECT * FROM employees;

-- ✅ GOOD: Select only needed columns
SELECT name, salary FROM employees;

-- ❌ BAD: Function on indexed column
SELECT * FROM employees WHERE YEAR(hire_date) = 2024;

-- ✅ GOOD: Use range
SELECT * FROM employees
WHERE hire_date BETWEEN '2024-01-01' AND '2024-12-31';

-- ❌ BAD: Leading wildcard
SELECT * FROM employees WHERE name LIKE '%lice';

-- ✅ GOOD: Trailing wildcard (can use index)
SELECT * FROM employees WHERE name LIKE 'Ali%';

-- ❌ BAD: OR on different columns
SELECT * FROM employees WHERE name = 'Alice' OR dept_id = 2;

-- ✅ GOOD: Use UNION
SELECT * FROM employees WHERE name = 'Alice'
UNION
SELECT * FROM employees WHERE dept_id = 2;

-- ❌ BAD: NOT IN with subquery
SELECT * FROM employees WHERE dept_id NOT IN (SELECT id FROM departments);

-- ✅ GOOD: LEFT JOIN with NULL check
SELECT e.* FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id
WHERE d.id IS NULL;

-- ❌ BAD: COUNT(*)
SELECT COUNT(*) FROM employees;

-- ✅ GOOD (in some engines): COUNT on indexed column
SELECT COUNT(id) FROM employees;

-- ==========================================
-- ANALYZE TABLE
-- ==========================================
ANALYZE TABLE employees;
OPTIMIZE TABLE employees;
```

---

### **Topic 33: Partitioning**

```sql
-- ==========================================
-- RANGE PARTITIONING
-- ==========================================
CREATE TABLE sales_partitioned (
    id INT AUTO_INCREMENT,
    sale_date DATE,
    amount DECIMAL(10,2),
    PRIMARY KEY (id, sale_date)
)
PARTITION BY RANGE (YEAR(sale_date)) (
    PARTITION p2022 VALUES LESS THAN (2023),
    PARTITION p2023 VALUES LESS THAN (2024),
    PARTITION p2024 VALUES LESS THAN (2025),
    PARTITION pfuture VALUES LESS THAN MAXVALUE
);

-- Queries on specific year only scan relevant partition
SELECT * FROM sales_partitioned WHERE sale_date = '2024-06-15';

-- ==========================================
-- LIST PARTITIONING
-- ==========================================
CREATE TABLE employees_by_region (
    id INT AUTO_INCREMENT,
    name VARCHAR(100),
    region VARCHAR(20),
    PRIMARY KEY (id, region)
)
PARTITION BY LIST COLUMNS(region) (
    PARTITION peast VALUES IN ('New York', 'Boston'),
    PARTITION pwest VALUES IN ('LA', 'Seattle'),
    PARTITION pcentral VALUES IN ('Chicago', 'Dallas')
);
```

---

## PHASE 11: SECURITY & ADMINISTRATION (Weeks 28-30)

---

### **Topic 34: User Management & Permissions**

```sql
-- ==========================================
-- CREATE USER
-- ==========================================
CREATE USER 'john'@'localhost' IDENTIFIED BY 'StrongPass123!';
CREATE USER 'api_user'@'%' IDENTIFIED BY 'ApiPass456!';  -- From any host

-- ==========================================
-- GRANT PERMISSIONS
-- ==========================================
-- Full access to one database
GRANT ALL PRIVILEGES ON ecommerce.* TO 'john'@'localhost';

-- Read only
GRANT SELECT ON ecommerce.* TO 'report_user'@'localhost';

-- Specific permissions
GRANT SELECT, INSERT, UPDATE ON ecommerce.orders TO 'api_user'@'%';

-- Specific table & columns
GRANT SELECT (name, email) ON ecommerce.users TO 'limited_user'@'localhost';

-- ==========================================
-- REVOKE PERMISSIONS
-- ==========================================
REVOKE INSERT ON ecommerce.orders FROM 'api_user'@'%';
REVOKE ALL PRIVILEGES ON ecommerce.* FROM 'john'@'localhost';

-- ==========================================
-- VIEW & MANAGE
-- ==========================================
SHOW GRANTS FOR 'john'@'localhost';
ALTER USER 'john'@'localhost' IDENTIFIED BY 'NewPassword!';
DROP USER 'john'@'localhost';
FLUSH PRIVILEGES;

-- ==========================================
-- ROLES (MySQL 8+)
-- ==========================================
CREATE ROLE 'read_only', 'read_write', 'admin';

GRANT SELECT ON ecommerce.* TO 'read_only';
GRANT SELECT, INSERT, UPDATE, DELETE ON ecommerce.* TO 'read_write';
GRANT ALL PRIVILEGES ON ecommerce.* TO 'admin';

GRANT 'read_only' TO 'john'@'localhost';
SET DEFAULT ROLE 'read_only' TO 'john'@'localhost';
```

---

### **Topic 35: Backup & Recovery**

```bash
# ==========================================
# BACKUP (mysqldump)
# ==========================================
# Full database backup
mysqldump -u root -p ecommerce > ecommerce_backup.sql

# Specific tables
mysqldump -u root -p ecommerce users orders > tables_backup.sql

# All databases
mysqldump -u root -p --all-databases > full_backup.sql

# With compression
mysqldump -u root -p ecommerce | gzip > ecommerce_backup.sql.gz

# ==========================================
# RESTORE
# ==========================================
mysql -u root -p ecommerce < ecommerce_backup.sql

# From compressed
gunzip < ecommerce_backup.sql.gz | mysql -u root -p ecommerce
```

---

### **Topic 36: SQL Injection Prevention**

```sql
-- ==========================================
-- ❌ VULNERABLE CODE (Never do this!)
-- ==========================================
-- query = "SELECT * FROM users WHERE email = '" + userInput + "'"
-- If userInput = "' OR '1'='1" → Returns ALL users!
-- If userInput = "'; DROP TABLE users; --" → DELETES the table!

-- ==========================================
-- ✅ SAFE: Use Prepared Statements
-- ==========================================

-- MySQL Prepared Statement
PREPARE stmt FROM 'SELECT * FROM users WHERE email = ?';
SET @email = 'alice@mail.com';
EXECUTE stmt USING @email;
DEALLOCATE PREPARE stmt;
```

```python
# Python example (safe)
cursor.execute("SELECT * FROM users WHERE email = %s", (user_email,))

# Node.js example (safe)
# connection.query("SELECT * FROM users WHERE email = ?", [userEmail])

# Java example (safe)
# PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE email = ?");
# ps.setString(1, userEmail);
```

---

## PHASE 12: NoSQL BASICS (Weeks 30-32)

---

### **Topic 37: MongoDB (NoSQL Fundamentals)**

```javascript
// ==========================================
// SQL vs MongoDB Terminology
// ==========================================
// SQL          →  MongoDB
// Database     →  Database
// Table        →  Collection
// Row          →  Document
// Column       →  Field
// JOIN         →  Embedding / $lookup

// ==========================================
// BASIC OPERATIONS
// ==========================================

// Create / Insert
db.users.insertOne({
    name: "Alice",
    age: 25,
    email: "alice@mail.com",
    hobbies: ["reading", "coding"],
    address: {
        city: "New York",
        state: "NY"
    }
});

db.users.insertMany([
    { name: "Bob", age: 30, email: "bob@mail.com" },
    { name: "Charlie", age: 28, email: "charlie@mail.com" }
]);

// Read / Find
db.users.find();                              // SELECT * FROM users
db.users.find({ age: 25 });                   // WHERE age = 25
db.users.find({ age: { $gt: 25 } });          // WHERE age > 25
db.users.find({ age: { $gte: 25, $lte: 30 }}); // BETWEEN
db.users.find({ name: /^A/ });                // LIKE 'A%'
db.users.find({}, { name: 1, email: 1 });     // SELECT name, email

// Update
db.users.updateOne(
    { name: "Alice" },
    { $set: { age: 26 } }
);

// Delete
db.users.deleteOne({ name: "Charlie" });

// Aggregation (GROUP BY equivalent)
db.orders.aggregate([
    { $group: { _id: "$status", total: { $sum: "$amount" } } },
    { $sort: { total: -1 } }
]);
```

---

### **Topic 38: When to Use SQL vs NoSQL**

```
┌─────────────────────┬────────────────────────────┐
│     USE SQL WHEN    │   USE NoSQL WHEN           │
├─────────────────────┼────────────────────────────┤
│ Structured data     │ Unstructured/flexible data │
│ Complex queries     │ Simple queries             │
│ ACID compliance     │ High scalability needed    │
│ Financial systems   │ Real-time applications     │
│ Inventory systems   │ IoT / Sensor data          │
│ ERP / CRM          │ Social media feeds         │
│ Reporting/Analytics │ Caching (Redis)            │
│ Relationships matter│ Document storage           │
└─────────────────────┴────────────────────────────┘
```

---

## PHASE 13: REAL-WORLD PROJECTS (Weeks 32-36)

---

### **Topic 39: Complete Project - E-Commerce Analytics**

```sql
-- ==========================================
-- REAL BUSINESS QUERIES
-- ==========================================

-- 1. Monthly Revenue Report
SELECT
    DATE_FORMAT(o.order_date, '%Y-%m') AS month,
    COUNT(DISTINCT o.id) AS total_orders,
    SUM(oi.quantity * oi.price) AS revenue,
    AVG(o.total) AS avg_order_value
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
WHERE o.status != 'cancelled'
GROUP BY DATE_FORMAT(o.order_date, '%Y-%m')
ORDER BY month;

-- 2. Top 10 Customers by Lifetime Value
SELECT
    u.id,
    u.name,
    COUNT(o.id) AS total_orders,
    SUM(o.total) AS lifetime_value,
    AVG(o.total) AS avg_order_value,
    MAX(o.order_date) AS last_order
FROM users u
JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name
ORDER BY lifetime_value DESC
LIMIT 10;

-- 3. Product Performance with Ranking
WITH product_stats AS (
    SELECT
        p.id,
        p.name,
        c.name AS category,
        SUM(oi.quantity) AS units_sold,
        SUM(oi.quantity * oi.price) AS revenue,
        AVG(r.rating) AS avg_rating,
        COUNT(DISTINCT r.id) AS review_count
    FROM products p
    LEFT JOIN order_items oi ON p.id = oi.product_id
    LEFT JOIN categories c ON p.category_id = c.id
    LEFT JOIN reviews r ON p.id = r.product_id
    GROUP BY p.id, p.name, c.name
)
SELECT
    *,
    RANK() OVER (ORDER BY revenue DESC) AS revenue_rank,
    RANK() OVER (PARTITION BY category ORDER BY revenue DESC) AS category_rank
FROM product_stats;

-- 4. Customer Cohort Analysis (Retention)
WITH first_purchase AS (
    SELECT
        user_id,
        DATE_FORMAT(MIN(order_date), '%Y-%m') AS cohort_month
    FROM orders
    GROUP BY user_id
)
SELECT
    fp.cohort_month,
    DATE_FORMAT(o.order_date, '%Y-%m') AS order_month,
    COUNT(DISTINCT o.user_id) AS active_customers,
    TIMESTAMPDIFF(MONTH,
        STR_TO_DATE(CONCAT(fp.cohort_month, '-01'), '%Y-%m-%d'),
        STR_TO_DATE(CONCAT(DATE_FORMAT(o.order_date, '%Y-%m'), '-01'), '%Y-%m-%d')
    ) AS months_since_first
FROM orders o
JOIN first_purchase fp ON o.user_id = fp.user_id
GROUP BY fp.cohort_month, order_month
ORDER BY fp.cohort_month, order_month;

-- 5. Inventory Alert System
SELECT
    p.name,
    p.stock AS current_stock,
    COALESCE(SUM(oi.quantity), 0) AS total_sold_last_30_days,
    p.stock / NULLIF(COALESCE(SUM(oi.quantity), 0) / 30, 0) AS days_of_stock_left,
    CASE
        WHEN p.stock = 0 THEN '🔴 OUT OF STOCK'
        WHEN p.stock < 10 THEN '🟡 LOW STOCK'
        ELSE '🟢 IN STOCK'
    END AS status
FROM products p
LEFT JOIN order_items oi ON p.id = oi.product_id
LEFT JOIN orders o ON oi.order_id = o.id
    AND o.order_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)
GROUP BY p.id, p.name, p.stock
ORDER BY days_of_stock_left ASC;
```

---

## 📋 COMPLETE STUDY CHECKLIST

```
PHASE 1: Foundation ✅
  □ What is a Database
  □ RDBMS Concepts
  □ Installation & Setup
  □ DDL (CREATE, ALTER, DROP)
  □ Data Types

PHASE 2: CRUD ✅
  □ INSERT
  □ SELECT + WHERE + Operators
  □ UPDATE
  □ DELETE

PHASE 3: Intermediate ✅
  □ ORDER BY, LIMIT, OFFSET
  □ Aggregate Functions (COUNT, SUM, AVG, MIN, MAX)
  □ GROUP BY + HAVING
  □ Aliases + CONCAT

PHASE 4: Constraints & Keys ✅
  □ NOT NULL, UNIQUE, CHECK, DEFAULT
  □ PRIMARY KEY
  □ FOREIGN KEY + Relationships

PHASE 5: JOINs ✅
  □ INNER JOIN
  □ LEFT JOIN
  □ RIGHT JOIN
  □ FULL OUTER JOIN
  □ CROSS JOIN
  □ SELF JOIN
  □ Multiple JOINs

PHASE 6: Advanced SELECT ✅
  □ Subqueries (WHERE, FROM, SELECT)
  □ EXISTS / NOT EXISTS
  □ Correlated Subqueries
  □ String Functions
  □ Date Functions
  □ CASE Statements
  □ UNION / INTERSECT / EXCEPT

PHASE 7: Advanced SQL ✅
  □ Window Functions (ROW_NUMBER, RANK, LAG, LEAD, etc.)
  □ CTEs (WITH clause)
  □ Recursive CTEs
  □ Views
  □ Indexes + EXPLAIN

PHASE 8: Database Design ✅
  □ Normalization (1NF, 2NF, 3NF)
  □ ER Diagrams
  □ Schema Design

PHASE 9: Programming in SQL ✅
  □ Transactions + ACID
  □ Stored Procedures
  □ User-Defined Functions
  □ Triggers

PHASE 10: Performance ✅
  □ Query Optimization
  □ Partitioning
  □ Explain Plans

PHASE 11: Security ✅
  □ User Management
  □ Roles & Permissions
  □ Backup & Recovery
  □ SQL Injection Prevention

PHASE 12: NoSQL ✅
  □ MongoDB Basics
  □ SQL vs NoSQL

PHASE 13: Projects ✅
  □ E-Commerce Database
  □ Analytics Queries
  □ Real-world Scenarios
```

---

## 📚 Recommended Practice Resources

```
FREE PRACTICE:
1. LeetCode (SQL section)     - 50+ problems
2. HackerRank SQL             - Beginner to Advanced
3. SQLZoo.net                 - Interactive tutorials
4. Mode Analytics SQL Tutorial - Real datasets
5. W3Schools SQL              - Quick reference
6. db-fiddle.com              - Online SQL playground

BOOKS:
1. "Learning SQL" - Alan Beaulieu (Beginner)
2. "SQL Performance Explained" - Markus Winand (Advanced)
3. "Database Design for Mere Mortals" (Design)

YOUTUBE CHANNELS:
1. Bro Code - SQL Tutorial
2. Programming with Mosh - MySQL
3. freeCodeCamp - Full SQL Course
```

> **💡 Golden Rule**: Practice at least **2-3 SQL problems daily** on LeetCode/HackerRank. Reading alone won't make you master databases — **writing queries will!**

# 🗄️ The Absolute SQL Interview Guide

> *"SQL is the lingua franca of data. If you speak it fluently, every database in the world becomes your playground."*

Welcome. Whether you're preparing for your first data analyst role or a senior backend engineering position at a FAANG company, this guide is designed to be the **only SQL resource you need**. We go beyond surface-level definitions — you'll find **ASCII diagrams**, **real-world analogies**, **production-grade best practices**, and **115 battle-tested Q&As**.

**What Makes This Guide Different?**
- 🔍 **Visual Learning**: Every JOIN, index, and transaction is explained with ASCII art.
- 🏗️ **Analogies**: Complex concepts explained using everyday things (libraries, bank transfers, Venn diagrams).
- ⚡ **Advanced Topics**: Window functions, CTEs, execution plans, query optimization, and isolation levels with dirty-read examples.
- 🎯 **Interview-First**: Every question is something that has actually been asked in real interviews.

**Assumption**: Examples use **MySQL/PostgreSQL** syntax unless noted. Differences between MySQL, PostgreSQL, SQL Server, and Oracle are highlighted where relevant.

---

## Table of Contents

<!-- TOC start -->

- [Section 1: SQL Fundamentals](#section-1-sql-fundamentals)
  * [What is SQL?](#what-is-sql)
  * [The SQL Command Families (DDL, DML, DQL, DCL, TCL)](#the-sql-command-families)
  * [Data Types Deep Dive](#data-types-deep-dive)
  * [Q&A Bank (Questions 1-10)](#qa-bank-questions-1-10)
- [Section 2: Querying Data Like a Pro](#section-2-querying-data-like-a-pro)
  * [The SELECT Statement Lifecycle](#the-select-statement-lifecycle)
  * [Filtering & Pattern Matching](#filtering--pattern-matching)
  * [Sorting & Pagination](#sorting--pagination)
  * [Aggregation & The GROUP BY Engine](#aggregation--the-group-by-engine)
  * [Q&A Bank (Questions 11-42)](#qa-bank-questions-11-42)
- [Section 3: JOINs — The Heart of Relational Databases](#section-3-joins--the-heart-of-relational-databases)
  * [Visual JOIN Reference (ASCII Venn Diagrams)](#visual-join-reference)
  * [INNER, LEFT, RIGHT, FULL OUTER, CROSS, SELF](#all-join-types)
  * [Set Operations: UNION, INTERSECT, EXCEPT](#set-operations)
  * [Q&A Bank (Questions 43-54)](#qa-bank-questions-43-54)
- [Section 4: Subqueries, CTEs & Window Functions](#section-4-subqueries-ctes--window-functions)
  * [Subqueries: Scalar, Row, Correlated](#subqueries)
  * [CTEs: The WITH Clause](#ctes)
  * [Window Functions: The Game Changer](#window-functions)
  * [Q&A Bank (Questions 55-60)](#qa-bank-questions-55-60)
- [Section 5: Data Definition & Manipulation (DDL, DML, DCL)](#section-5-data-definition--manipulation)
  * [Creating & Modifying Tables](#creating--modifying-tables)
  * [INSERT, UPDATE, DELETE vs TRUNCATE](#insert-update-delete-vs-truncate)
  * [Constraints & Integrity](#constraints--integrity)
  * [Q&A Bank (Questions 61-91)](#qa-bank-questions-61-91)
- [Section 6: Indexes, Privileges & Security](#section-6-indexes-privileges--security)
  * [How Indexes Work (The Library Analogy)](#how-indexes-work)
  * [Clustered vs Non-Clustered Indexes](#clustered-vs-non-clustered)
  * [SQL Injection: The #1 Security Threat](#sql-injection)
  * [Q&A Bank (Questions 92-96, 115)](#qa-bank-questions-92-96-115)
- [Section 7: Transactions, ACID & Concurrency](#section-7-transactions-acid--concurrency)
  * [The Bank Transfer Analogy](#the-bank-transfer-analogy)
  * [ACID Properties Explained](#acid-properties-explained)
  * [Isolation Levels & The Three Read Phenomena](#isolation-levels)
  * [Locks & Deadlocks](#locks--deadlocks)
  * [Q&A Bank (Questions 97-104)](#qa-bank-questions-97-104)
- [Section 8: Views, Stored Procedures, Triggers & Cursors](#section-8-views-stored-procedures-triggers--cursors)
  * [Q&A Bank (Questions 105-114)](#qa-bank-questions-105-114)
- [Section 9: Query Optimization & Execution Plans](#section-9-query-optimization--execution-plans)
  * [Reading EXPLAIN Output](#reading-explain-output)
  * [The 10 Query Performance Killers](#the-10-query-performance-killers)
- [Section 10: Database Design & Normalization](#section-10-database-design--normalization)
  * [1NF, 2NF, 3NF, BCNF with Examples](#1nf-2nf-3nf-bcnf)
  * [Denormalization: When to Break the Rules](#denormalization)

<!-- TOC end -->

---

## Section 1: SQL Fundamentals

### What is SQL?

SQL (Structured Query Language) is a **declarative language** — you describe *what* you want, and the database engine figures out *how* to get it. Think of it like ordering at a restaurant: you say "Bring me a medium-rare steak," not "Go to the fridge, take out the meat, heat the pan to 200°C..."

```
┌─────────────────────────────────────────────────────────────┐
│  IMPERATIVE (C, Python)          DECLARATIVE (SQL)          │
│                                                             │
│  for each row:                  SELECT name, salary         │
│    if salary > 50000:           FROM employees              │
│      print(name)                WHERE salary > 50000;       │
└─────────────────────────────────────────────────────────────┘
```

SQL was born at IBM in the 1970s (originally called SEQUEL) and is now an ANSI/ISO standard. However, every database vendor adds their own spice:

| Feature | MySQL | PostgreSQL | SQL Server | Oracle |
|---------|-------|-----------|------------|--------|
| Limit rows | `LIMIT 10` | `LIMIT 10` | `TOP 10` | `FETCH FIRST 10` |
| Boolean | `TINYINT(1)` | `BOOLEAN` | `BIT` | `NUMBER(1)` |
| Current date | `CURDATE()` | `CURRENT_DATE` | `GETDATE()` | `SYSDATE` |
| String concat | `CONCAT()` | `\|\|` | `+` | `\|\|` |

### The SQL Command Families

Imagine a company. There are people who **build** the office (DDL), people who **work** in it (DML), people who **ask questions** (DQL), security guards who **control access** (DCL), and managers who **approve or cancel** decisions (TCL).

```
┌─────────────────────────────────────────────────────────────┐
│                    SQL COMMAND FAMILIES                     │
├──────────┬──────────────────────────────────────────────────┤
│ DDL      │ Data Definition Language                           │
│          │ CREATE, ALTER, DROP, TRUNCATE, RENAME              │
│          │ → "Builds the structure"                           │
├──────────┼──────────────────────────────────────────────────┤
│ DML      │ Data Manipulation Language                         │
│          │ INSERT, UPDATE, DELETE                             │
│          │ → "Changes the data"                               │
├──────────┼──────────────────────────────────────────────────┤
│ DQL      │ Data Query Language                                │
│          │ SELECT                                             │
│          │ → "Reads the data"                                 │
├──────────┼──────────────────────────────────────────────────┤
│ DCL      │ Data Control Language                              │
│          │ GRANT, REVOKE                                      │
│          │ → "Controls permissions"                           │
├──────────┼──────────────────────────────────────────────────┤
│ TCL      │ Transaction Control Language                       │
│          │ COMMIT, ROLLBACK, SAVEPOINT                        │
│          │ → "Manages transactions"                           │
└──────────┴──────────────────────────────────────────────────┘
```

### Data Types Deep Dive

Choosing the right data type is like choosing the right container — you don't store a sip of water in a swimming pool, and you don't store an ocean in a teacup.

| Category | Types | When to Use |
|----------|-------|-------------|
| **Integer** | `TINYINT`, `SMALLINT`, `MEDIUMINT`, `INT`, `BIGINT` | Whole numbers. Use the smallest that fits your range. |
| **Decimal** | `FLOAT`, `DOUBLE`, `DECIMAL(p,s)` | Money = always `DECIMAL`. Never use `FLOAT` for currency! |
| **String** | `CHAR(n)`, `VARCHAR(n)`, `TEXT` | `CHAR` for fixed length (e.g., country codes). `VARCHAR` for variable. `TEXT` for essays. |
| **Date/Time** | `DATE`, `TIME`, `DATETIME`, `TIMESTAMP` | `TIMESTAMP` is UTC-aware and smaller. `DATETIME` for historical dates. |
| **Binary** | `BLOB`, `BINARY`, `VARBINARY` | Images, files, encrypted data. |
| **JSON** | `JSON` (MySQL 5.7+), `JSONB` (PostgreSQL) | Semi-structured data, config, logs. PostgreSQL's `JSONB` is indexed & faster. |

**The Money Rule**: 
```sql
-- ❌ BAD: Float precision errors (0.1 + 0.2 ≠ 0.3)
CREATE TABLE bad_products (price FLOAT);

-- ✅ GOOD: Exact precision
CREATE TABLE good_products (price DECIMAL(10,2));  -- 99999999.99 max
```

### Best Practices
- 🎯 **Never use `SELECT *` in production.** It breaks when columns are added, transfers unnecessary data, and prevents covering indexes.
- 🎯 **Always specify columns in INSERT.** It makes your code robust against schema changes.
- 🎯 **Use `COALESCE()` instead of `IFNULL()`** — it's ANSI standard and works across databases.
- 🎯 **Be explicit about NULLs.** `NULL` is not `0`, not `""`, not `FALSE`. It is the "unknown."

---

### Q&A Bank (Questions 1-10)

**1. SQL was developed as an integral part of...**
> Relational Database Management Systems (RDBMS). SQL is the ANSI-standard language for creating, querying, updating, and managing relational databases. Major implementations include MySQL, PostgreSQL, SQL Server, Oracle, and SQLite.
>
> *Real-world context*: Every web application you use — Instagram, Netflix, Uber — stores its data in SQL databases (often sharded or replicated, but SQL at the core).

**2. What does SQL stand for?**
> **S**tructured **Q**uery **L**anguage. Originally called SEQUEL at IBM in the 1970s.

**3. What type of language is SQL?**
> **Declarative (non-procedural)**. You state *what* result you want, not *how* to compute it. The database's **query optimizer** decides the "how" — which indexes to use, which join order is fastest, etc.
>
> Compare with **PL/SQL** (Oracle) or **T-SQL** (SQL Server), which are procedural extensions that add loops, variables, and conditional logic.

**4. Which is NOT a valid SQL command: SELECT, REMOVE, UPDATE, INSERT?**
> **REMOVE** is not valid. To delete rows, use `DELETE`. `DROP` removes objects (tables, databases).
>
> | Command | Purpose |
> |---------|---------|
> | SELECT | Read data |
> | INSERT | Add new rows |
> | UPDATE | Modify existing rows |
> | DELETE | Remove rows |
> | CREATE/ALTER/DROP | Manage schema objects |

**5. What is MySQL, and how does it differ from SQL?**
> **SQL** is the *language* (like English). **MySQL** is a *database system* that *speaks* SQL (like a person who speaks English). 
>
> Analogy: SQL is the recipe; MySQL is the kitchen that follows it.

**6. What is PL/SQL, and how is it different from SQL?**
> **PL/SQL** = Procedural Language extensions to SQL (Oracle-specific). It adds variables, loops, IF-ELSE, and exception handling.
>
> | SQL | PL/SQL |
> |-----|--------|
> | Single statements | Blocks of code |
> | No variables | Variables & constants |
> | No loops | FOR, WHILE loops |
> | Data-oriented | Application-oriented |
> | Can embed in PL/SQL | Cannot embed SQL inside itself |

**7. What are the possible values for a BOOLEAN field in MySQL?**
> MySQL doesn't have a native `BOOLEAN` type. It uses `TINYINT(1)` where `0` = false, `1` = true, and any non-zero value is treated as true in conditions.
> ```sql
> CREATE TABLE users (is_active TINYINT(1) DEFAULT 1);
> ```
> PostgreSQL, however, has a true `BOOLEAN` type accepting `TRUE`, `FALSE`, and `NULL`.

**8. Which data type for distance rounded to the nearest mile?**
> `INTEGER` (or `INT`). If you need fractional miles later, use `DECIMAL(8,2)`.

**9. Which are valid SQL keywords?**
> `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `JOIN`, `INSERT`, `UPDATE`, `DELETE`, `CREATE`, `ALTER`, `DROP`, `INDEX`, `UNION`, `LIMIT`, `DISTINCT`, `AS`, `AND`, `OR`, `NOT`, `IN`, `BETWEEN`, `LIKE`, `IS NULL`, `EXISTS`, `CASE`, `WHEN`, `THEN`, `ELSE`, `END`.

**10. Which are valid SQL comments?**
> ```sql
> -- Single-line comment (standard)
> /* Multi-line
>    comment */
> # Hash comment (MySQL only)
> ```

---

## Section 2: Querying Data Like a Pro

### The SELECT Statement Lifecycle

When you run a `SELECT`, the database doesn't execute clauses in the order you write them. Understanding the **logical execution order** is crucial — it explains why you can't reference an alias in WHERE but can in ORDER BY.

```
┌──────────────────────────────────────────────────────────────────┐
│            LOGICAL EXECUTION ORDER OF SELECT                     │
├────────┬─────────────────────────────────────────────────────────┤
│ 1      │ FROM + JOINs → Determine source tables                  │
│ 2      │ WHERE → Filter rows                                     │
│ 3      │ GROUP BY → Aggregate into buckets                       │
│ 4      │ HAVING → Filter groups                                  │
│ 5      │ SELECT → Compute columns & aliases                      │
│ 6      │ DISTINCT → Remove duplicates                            │
│ 7      │ ORDER BY → Sort results                                 │
│ 8      │ LIMIT / OFFSET → Paginate                               │
└────────┴─────────────────────────────────────────────────────────┘
```

**This is why this fails:**
```sql
-- ❌ ERROR: alias "full_name" doesn't exist yet at step 2 (WHERE)
SELECT first_name || ' ' || last_name AS full_name
FROM employees
WHERE full_name = 'John Doe';

-- ✅ FIX: Repeat the expression or use a subquery/CTE
SELECT first_name || ' ' || last_name AS full_name
FROM employees
WHERE first_name || ' ' || last_name = 'John Doe';
```

### Filtering & Pattern Matching

```sql
-- Comparison operators
WHERE salary > 50000
WHERE age BETWEEN 18 AND 65          -- Inclusive on both ends
WHERE department IN ('Engineering', 'Product', 'Design')
WHERE name LIKE 'A%'                  -- Starts with A
WHERE name LIKE '%son'                -- Ends with son
WHERE name LIKE '_a%'                 -- Second letter is 'a'
WHERE name LIKE '%\_%' ESCAPE '\'     -- Contains literal underscore
WHERE email IS NULL                   -- Missing email (NOT = NULL!)
WHERE email IS NOT NULL
```

**The NULL Trap:**
```sql
-- 🚨 WRONG: This returns NOTHING, not even rows where manager_id IS NULL
SELECT * FROM employees WHERE manager_id = NULL;

-- ✅ CORRECT:
SELECT * FROM employees WHERE manager_id IS NULL;

-- COALESCE gives you a fallback value:
SELECT name, COALESCE(phone, 'No phone') AS contact FROM users;
-- IFNULL is MySQL-specific; COALESCE is standard and accepts multiple args:
SELECT COALESCE(mobile, home_phone, work_phone, 'No phone') FROM contacts;
```

### Sorting & Pagination

```sql
-- Multi-column sort
SELECT * FROM products
ORDER BY category ASC, price DESC;

-- Pagination (Page 3, 20 items per page)
-- MySQL / PostgreSQL
SELECT * FROM products ORDER BY id LIMIT 20 OFFSET 40;

-- SQL Server
SELECT * FROM products ORDER BY id OFFSET 40 ROWS FETCH NEXT 20 ROWS ONLY;

-- Offset gets slower as page number grows!
-- For large tables, use keyset pagination:
SELECT * FROM products WHERE id > 1000 ORDER BY id LIMIT 20;
```

### Aggregation & The GROUP BY Engine

Aggregate functions collapse multiple rows into one summary value:

| Function | Purpose | NULL Handling |
|----------|---------|---------------|
| `COUNT(*)` | Count all rows | Counts NULLs too |
| `COUNT(col)` | Count non-NULL values | Ignores NULLs |
| `SUM(col)` | Total | Ignores NULLs |
| `AVG(col)` | Average | Ignores NULLs |
| `MIN(col)` / `MAX(col)` | Smallest / Largest | Ignores NULLs |
| `GROUP_CONCAT()` / `STRING_AGG()` | Concatenate strings | Varies by DB |

```sql
-- Find departments with average salary > 60k, sorted
SELECT 
    department,
    COUNT(*) AS headcount,
    AVG(salary) AS avg_salary,
    MAX(salary) AS top_salary
FROM employees
WHERE hire_date >= '2020-01-01'    -- Filter ROWS first
GROUP BY department
HAVING AVG(salary) > 60000         -- Filter GROUPS after aggregation
ORDER BY avg_salary DESC;
```

**WHERE vs HAVING — The Critical Difference:**
```
┌─────────────────────────────────────────────────────────────────┐
│ WHERE filters ROWS (before grouping)                            │
│ HAVING filters GROUPS (after aggregation)                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Raw Rows → [WHERE] → Filtered Rows → [GROUP BY] → Groups      │
│                                                           ↓     │
│  Result ← [SELECT] ← [HAVING] ← Filtered Groups                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

### Q&A Bank (Questions 11-42)

**11. Which SQL statement extracts data?**
> `SELECT`. Optional clauses: `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`, `JOIN`.
> ```sql
> SELECT name AS full_name, salary * 12 AS annual_salary
> FROM employees
> WHERE department = 'Engineering'
> ORDER BY annual_salary DESC;
> ```

**12. How to select all records from table `Products`?**
> ```sql
> SELECT * FROM products;
> ```
> ⚠️ *Interview tip*: Always follow up with "But in production, I list explicit columns to reduce network overhead and prevent breaking if columns are reordered or added."

**13. Can we rename a column in output?**
> Yes, using `AS` (alias):
> ```sql
> SELECT first_name AS fname, last_name AS lname FROM customers;
> -- AS is optional but recommended for readability:
> SELECT first_name fname FROM customers;
> ```

**14. How to select `FirstName` from `Customers`?**
> ```sql
> SELECT FirstName FROM Customers;
> ```

**15. What does the FROM clause do?**
> Specifies the source table(s). Can include subqueries, JOINs, or even multiple tables (implicit cross join, but avoid this).

**16. Which statement returns only different values?**
> `SELECT DISTINCT`. It operates on the *entire selected row*.
> ```sql
> -- Returns unique city-state combinations
> SELECT DISTINCT city, state FROM addresses;
> ```

**17. Display distinct cities in ADDRESSES(id, street_name, number, city, state)?**
> ```sql
> SELECT DISTINCT city FROM addresses;
> ```

**18. Select all records where FirstName is "John"?**
> ```sql
> SELECT * FROM Customers WHERE FirstName = 'John';
> ```

**19. OR vs AND?**
> `AND` requires ALL conditions to be true. `OR` requires ANY to be true. Use parentheses to control precedence — `AND` binds tighter than `OR`.
> ```sql
> -- Without parentheses, this is parsed as:
> -- WHERE (age > 18 AND city = 'NY') OR status = 'active'
> SELECT * FROM customers 
> WHERE age > 18 AND (city = 'NY' OR city = 'LA');
> ```

**20. Which comparison operators exist?**
> `=`, `!=` or `<>`, `>`, `<`, `>=`, `<=`. Some DBs support `<=>` (NULL-safe equal in MySQL).

**21. Select records where FirstName="John" AND LastName="Jackson"?**
> ```sql
> SELECT * FROM Customers 
> WHERE FirstName = 'John' AND LastName = 'Jackson';
> ```

**22. How to select 10 random rows?**
> ```sql
> -- MySQL
> SELECT * FROM tbl ORDER BY RAND() LIMIT 10;
> -- PostgreSQL
> SELECT * FROM tbl ORDER BY RANDOM() LIMIT 10;
> -- SQL Server
> SELECT TOP 10 * FROM tbl ORDER BY NEWID();
> ```
> Performance note: This is O(n log n) and full table scan. For large tables, use a random ID approach.

**23. What does `ISNULL(price, 50)` return if price is NULL?**
> `50`. The first non-NULL value is returned.
> Cross-database version: `COALESCE(price, 50)`.

**24. Which operator searches text patterns?**
> `LIKE` with wildcards `%` (zero or more chars) and `_` (single char).
> ```sql
> WHERE name LIKE 'A%'      -- starts with A
> WHERE name LIKE '%a%'     -- contains a
> WHERE name LIKE '_a%'     -- second char is a
> WHERE name LIKE '___'     -- exactly 3 characters
> ```

**25. Details of students whose FirstName starts with 'K'?**
> ```sql
> SELECT * FROM Students WHERE FirstName LIKE 'K%';
> ```

**26. Which operator selects values in a range?**
> `BETWEEN` (inclusive):
> ```sql
> SELECT * FROM sales WHERE amount BETWEEN 100 AND 500;
> -- Equivalent to: amount >= 100 AND amount <= 500
> ```

**27. Correct syntax for date range?**
> ```sql
> SELECT * FROM Sales 
> WHERE Date BETWEEN '2017-12-01' AND '2018-01-01';
> ```
> Use ISO-8601 format (`YYYY-MM-DD`) to avoid locale issues.

**28. LastName alphabetically between "Brooks" and "Gray"?**
> ```sql
> SELECT * FROM Customers WHERE LastName BETWEEN 'Brooks' AND 'Gray';
> ```

**29. What does the IN keyword do?**
> Checks if a value matches any in a list. It's a shorthand for multiple ORs and often more readable.
> ```sql
> -- These are equivalent:
> WHERE state IN ('CA', 'NY', 'TX')
> WHERE state = 'CA' OR state = 'NY' OR state = 'TX'
> ```
> `IN` can also contain a subquery: `WHERE id IN (SELECT customer_id FROM orders)`.

**30. What does UPPER do?**
> Converts to uppercase. `LOWER` to lowercase. `INITCAP` (Oracle/PostgreSQL) capitalizes first letter of each word.
> ```sql
> SELECT UPPER('hello'); -- HELLO
> ```

**31. Round up to the nearest integer?**
> `CEILING()` or `CEIL()`:
> ```sql
> SELECT CEIL(25.01);   -- 26
> SELECT FLOOR(25.99);  -- 25
> SELECT ROUND(25.5);   -- 26
> ```

**32. Current date in MySQL without time?**
> ```sql
> SELECT CURDATE();        -- MySQL
> SELECT CURRENT_DATE;     -- Standard / PostgreSQL
> ```

**33. Keyword to retrieve maximum value?**
> `MAX()` aggregate function.
> ```sql
> SELECT MAX(salary) FROM employees;
> ```

**34. Function to count results?**
> `COUNT()`. `COUNT(*)` counts rows. `COUNT(column)` counts non-NULL values.
> ```sql
> SELECT COUNT(*) FROM orders;           -- Total orders
> SELECT COUNT(shipped_date) FROM orders; -- Only shipped orders
> ```

**35. Which are aggregate functions?**
> `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`. Some DBs also have `STDDEV`, `VARIANCE`, `GROUP_CONCAT`/`STRING_AGG`.

**36. Return number of records in Customers?**
> ```sql
> SELECT COUNT(*) FROM Customers;
> ```

**37. Sorting direction keywords?**
> `ASC` (ascending, default) and `DESC` (descending).
> ```sql
> ORDER BY price DESC, name ASC;
> ```

**38. Default sort order if not specified?**
> `ASC`.

**39. Top 3 students by mark?**
> ```sql
> -- MySQL / PostgreSQL
> SELECT name, mark FROM Students ORDER BY mark DESC LIMIT 3;
> -- SQL Server
> SELECT TOP 3 name, mark FROM Students ORDER BY mark DESC;
> -- Oracle
> SELECT name, mark FROM Students WHERE ROWNUM <= 3 ORDER BY mark DESC;
> ```

**40. Sort Customers descending by FirstName?**
> ```sql
> SELECT * FROM Customers ORDER BY FirstName DESC;
> ```

**41. Correct GROUP BY syntax?**
> ```sql
> SELECT name, COUNT(name) FROM customers GROUP BY name;
> ```
> In standard SQL (and MySQL 5.7+ with `ONLY_FULL_GROUP_BY`), any non-aggregated column in SELECT must appear in GROUP BY.

**42. WHERE vs HAVING?**
> | WHERE | HAVING |
> |-------|--------|
> | Filters **rows** | Filters **groups** |
> | Executes **before** GROUP BY | Executes **after** GROUP BY |
> | Cannot use aggregates | Can use `COUNT()`, `SUM()`, etc. |
> | Can reference any column | Can only reference grouped columns or aggregates |
>
> ```sql
> SELECT department, AVG(salary) AS avg_sal
> FROM employees
> WHERE hire_date > '2020-01-01'      -- Filter rows first
> GROUP BY department
> HAVING AVG(salary) > 60000;         -- Then filter groups
> ```

---

## Section 3: JOINs — The Heart of Relational Databases

Relational databases split data across tables to avoid duplication. JOINs are how you put Humpty Dumpty back together again.

### Visual JOIN Reference

Imagine two circles in a Venn diagram. The **left circle** is Table A, the **right circle** is Table B.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                         THE JOIN FAMILY TREE                                 │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   INNER JOIN                    LEFT JOIN                    RIGHT JOIN      │
│                                                                              │
│      A       B                    A       B                    A       B     │
│    ┌───┐   ┌───┐                ┌───┐   ┌───┐                ┌───┐   ┌───┐   │
│    │███│   │███│                │███│███│   │                │   │███│███│   │
│    │███│███│███│                │███│███│   │                │   │███│███│   │
│    │███│   │███│                │███│███│   │                │   │███│███│   │
│    └───┘   └───┘                └───┘   └───┘                └───┘   └───┘   │
│      ▓▓▓ Only matching           ▓▓▓ All from A              ▓▓▓ All from B  │
│                                                                              │
│   FULL OUTER JOIN              CROSS JOIN                   SELF JOIN        │
│                                                                              │
│      A       B                    A       B                    A ←→ A        │
│    ┌───┐   ┌───┐                ┌───┐   ┌───┐                                │
│    │███│███│   │                │███│███│███│                Employee        │
│    │███│███│███│                │███│███│███│                ├─ id           │
│    │   │███│███│                │███│███│███│                ├─ name         │
│    └───┘   └───┘                └───┘   └───┘                └─ manager_id   │
│      ▓▓▓ All from both           ▓▓▓ Every row x                             │
│                                  every row (Cartesian)       Join to itself  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### All JOIN Types Explained

```sql
-- Sample tables
CREATE TABLE customers (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);
CREATE TABLE orders (
    id INT PRIMARY KEY,
    customer_id INT,
    amount DECIMAL(10,2)
);
```

**INNER JOIN** — Only matching rows from both tables.
```sql
SELECT c.name, o.amount
FROM customers c
INNER JOIN orders o ON c.id = o.customer_id;
-- Only customers who HAVE placed orders
```

**LEFT JOIN** — All rows from the left table, NULLs for right-table misses.
```sql
SELECT c.name, COALESCE(o.amount, 0) AS amount
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id;
-- ALL customers, even those who never ordered (amount shows 0)
```

**RIGHT JOIN** — All rows from the right table. Rarely used; just swap table order and use LEFT JOIN.

**FULL OUTER JOIN** — All rows from both, NULLs where no match. Not supported in MySQL, but works in PostgreSQL/SQL Server/Oracle.
```sql
-- PostgreSQL
SELECT * FROM customers c
FULL OUTER JOIN orders o ON c.id = o.customer_id;

-- MySQL workaround with UNION
SELECT * FROM customers c LEFT JOIN orders o ON c.id = o.customer_id
UNION
SELECT * FROM customers c RIGHT JOIN orders o ON c.id = o.customer_id;
```

**CROSS JOIN** — Cartesian product. A × B rows.
```sql
-- Every color paired with every size
SELECT color, size FROM colors CROSS JOIN sizes;  -- 5 colors × 4 sizes = 20 rows
```

**SELF JOIN** — Table joined to itself.
```sql
-- Find employees and their managers
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

### Set Operations

```sql
-- UNION: Combine, remove duplicates
SELECT city FROM customers
UNION
SELECT city FROM suppliers;

-- UNION ALL: Combine, keep duplicates (FASTER — use when you know there are no dupes)
SELECT city FROM customers
UNION ALL
SELECT city FROM suppliers;

-- INTERSECT: Only rows present in BOTH (not in MySQL)
SELECT city FROM customers
INTERSECT
SELECT city FROM suppliers;

-- EXCEPT / MINUS: In first set but NOT in second
SELECT city FROM customers
EXCEPT           -- PostgreSQL / SQL Server
-- MINUS        -- Oracle
SELECT city FROM suppliers;
```

---

### Q&A Bank (Questions 43-54)

**43. What is JOIN used for?**
> Combines rows from two or more tables based on a related column (foreign key relationship).

**44. Most common type of join?**
> `INNER JOIN`. It's the default — if you write `FROM A JOIN B`, most databases interpret it as `INNER JOIN`.

**45. What are different JOINs in SQL?**
> 1. **INNER JOIN** — matching rows only
> 2. **LEFT (OUTER) JOIN** — all left + matched right
> 3. **RIGHT (OUTER) JOIN** — all right + matched left
> 4. **FULL OUTER JOIN** — all rows from both
> 5. **CROSS JOIN** — Cartesian product
> 6. **SELF JOIN** — table joined to itself

**46. Which is NOT TRUE about the ON clause?**
> The `ON` clause specifies the join condition. It improves readability over the old comma-syntax, supports multi-column joins (`ON a.id = b.id AND a.type = b.type`), and is required for outer joins. Any statement claiming otherwise is false.

**47. Inner join result?**
> Returns only rows where the join condition evaluates to true in **both** tables.

**48. Can you join 3 tables with INNER JOIN?**
> Yes. There's no practical limit (though performance degrades with many joins).
> ```sql
> SELECT f.name, d.name AS division, c.name AS country
> FROM faculty f
> INNER JOIN division d ON f.division_id = d.id
> INNER JOIN country c ON f.country_id = c.id;
> ```

**49. Can you join a table to itself?**
> Yes — **SELF JOIN**. You must use aliases to distinguish the two instances.
> ```sql
> SELECT a.name AS employee, b.name AS manager
> FROM employees a, employees b
> WHERE a.manager_id = b.id;
> ```

**50. What is true about Cartesian Products?**
> A Cartesian product occurs when tables are joined **without a condition**. Every row in Table A pairs with every row in Table B: `m × n` rows total. It's usually a bug, but `CROSS JOIN` is explicit and valid for combinatorial data.

**51. INTERSECTION in relational algebra?**
> Corresponds to rows present in **both** sets. SQL: `INTERSECT`.

**52. UNION in relational algebra?**
> Corresponds to rows in **either** set, duplicates removed. Think "A OR B" in set terms.

**53. UNION vs UNION ALL?**
> | UNION | UNION ALL |
> |-------|-----------|
> | Removes duplicates | Keeps duplicates |
> | Slower (sort + dedup) | Faster |
> | Use when uniqueness matters | Use when sets are already distinct or duplicates are meaningful |

**54. Which set operator for "searched but didn't buy"?**
> `MINUS` (Oracle) or `EXCEPT` (PostgreSQL/SQL Server):
> ```sql
> SELECT name FROM searchers WHERE product = 'X'
> EXCEPT
> SELECT name FROM buyers WHERE product = 'X';
> ```

---

## Section 4: Subqueries, CTEs & Window Functions

### Subqueries

A subquery is a query inside another query. It can return a **scalar** (one value), a **single row**, a **column** (multiple rows, one column), or a **table** (multiple rows, multiple columns).

```sql
-- Scalar subquery (returns one value)
SELECT name, salary,
    (SELECT AVG(salary) FROM employees) AS company_avg
FROM employees;

-- Correlated subquery (depends on outer query)
SELECT name, salary
FROM employees e
WHERE salary > (SELECT AVG(salary) FROM employees WHERE dept = e.dept);

-- Subquery with IN
SELECT name FROM customers
WHERE id IN (SELECT customer_id FROM orders WHERE amount > 1000);

-- Subquery with EXISTS (often faster than IN for large datasets)
SELECT name FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);
```

**`EXISTS` vs `IN`:**
- `EXISTS` stops at the first match (short-circuits).
- `IN` builds the entire subquery result set first.
- Use `EXISTS` for correlated subqueries, `IN` for small static lists.

### CTEs: The WITH Clause

CTEs (Common Table Expressions) make complex queries readable. They're like temporary views for a single query.

```sql
WITH high_earners AS (
    SELECT dept, AVG(salary) AS avg_sal
    FROM employees
    GROUP BY dept
    HAVING AVG(salary) > 80000
),
recent_hires AS (
    SELECT * FROM employees WHERE hire_date > '2023-01-01'
)
SELECT r.name, r.salary, h.avg_sal
FROM recent_hires r
JOIN high_earners h ON r.dept = h.dept;
```

**Recursive CTEs** (for hierarchical data):
```sql
-- PostgreSQL / SQL Server / MySQL 8.0+
WITH RECURSIVE org_tree AS (
    -- Anchor: top-level managers
    SELECT id, name, manager_id, 0 AS level
    FROM employees WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive: employees under each manager
    SELECT e.id, e.name, e.manager_id, ot.level + 1
    FROM employees e
    JOIN org_tree ot ON e.manager_id = ot.id
)
SELECT * FROM org_tree;
```

### Window Functions: The Game Changer

Window functions are the #1 topic that separates junior from senior SQL interviews. They compute across a "window" of rows related to the current row **without collapsing rows** like GROUP BY does.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    GROUP BY vs WINDOW FUNCTION                               │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Input:                              GROUP BY result:    Window result:      │
│  ┌──────┬────────┬────────┐          ┌──────┬────────┐   ┌──────┬────────┐   │
│  │ Dept │ Name   │ Salary │          │ Dept │ AVG    │   │ Name │ AVG    │   │
│  ├──────┼────────┼────────┤          ├──────┼────────┤   ├──────┼────────┤   │
│  │ A    │ Alice  │ 100    │    →     │ A    │ 150    │   │ Alice│ 150    │   │
│  │ A    │ Bob    │ 200    │          │ B    │ 400    │   │ Bob  │ 150    │   │
│  │ B    │ Carol  │ 400    │          └──────┴────────┘   │ Carol│ 400    │   │
│  └──────┴────────┴────────┘                              └──────┴────────┘   │
│                                                                              │
│  GROUP BY collapses rows            Window keeps all rows, adds calculation  │
│  (3 rows → 2 rows)                  (3 rows → 3 rows)                        │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

```sql
-- ROW_NUMBER(): Unique rank, no ties
SELECT name, salary,
    ROW_NUMBER() OVER (ORDER BY salary DESC) AS rank_num
FROM employees;
-- Alice: 50000 → 1, Bob: 50000 → 2, Carol: 40000 → 3

-- RANK(): Ties get same rank, next rank skips
SELECT name, salary,
    RANK() OVER (ORDER BY salary DESC) AS rank_num
FROM employees;
-- Alice: 50000 → 1, Bob: 50000 → 1, Carol: 40000 → 3

-- DENSE_RANK(): Ties get same rank, next rank doesn't skip
SELECT name, salary,
    DENSE_RANK() OVER (ORDER BY salary DESC) AS rank_num
FROM employees;
-- Alice: 50000 → 1, Bob: 50000 → 1, Carol: 40000 → 2

-- PARTITION BY: Reset window per group
SELECT dept, name, salary,
    RANK() OVER (PARTITION BY dept ORDER BY salary DESC) AS dept_rank
FROM employees;

-- LAG / LEAD: Previous / next row values
SELECT date, revenue,
    LAG(revenue, 1) OVER (ORDER BY date) AS prev_day,
    revenue - LAG(revenue, 1) OVER (ORDER BY date) AS daily_change
FROM daily_sales;

-- Running total
SELECT name, salary,
    SUM(salary) OVER (ORDER BY hire_date) AS running_total
FROM employees;

-- Moving average
SELECT date, temperature,
    AVG(temperature) OVER (ORDER BY date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
FROM weather;
```

---

### Q&A Bank (Questions 55-60)

**55. A SELECT statement whose results are used in filtering the main query is called?**
> A **subquery** (inner query or nested query).

**56. Subqueries can be nested in...**
> `SELECT`, `INSERT`, `UPDATE`, `DELETE`, or another subquery. They can appear in `WHERE`, `FROM`, `SELECT` (scalar), or `HAVING`.

**57. Row comparison operators with subqueries?**
> `IN`, `ANY`, `ALL`, `EXISTS`, `NOT EXISTS`, and standard comparison operators (`=`, `>`, `<`, `>=`, `<=`, `<>`).
> ```sql
> WHERE salary > ALL (SELECT salary FROM employees WHERE dept = 'Sales')
> WHERE salary > ANY (SELECT salary FROM employees WHERE dept = 'Sales')
> ```

**58. A subquery inside a subquery is called?**
> A **nested subquery**.

**59. A subquery that references the outer query?**
> A **correlated subquery**. It executes once for each row of the outer query.
> ```sql
> SELECT * FROM employees e
> WHERE salary > (SELECT AVG(salary) FROM employees WHERE dept = e.dept);
> ```

**60. What is the CASE function?**
> SQL's version of IF-THEN-ELSE. Two forms: simple and searched.
> ```sql
> -- Searched CASE (more flexible)
> SELECT name,
>     CASE 
>         WHEN salary >= 100000 THEN 'Executive'
>         WHEN salary >= 60000  THEN 'Senior'
>         WHEN salary >= 40000  THEN 'Mid'
>         ELSE 'Junior'
>     END AS level
> FROM employees;
> 
> -- Simple CASE
> SELECT name,
>     CASE dept
>         WHEN 'Engineering' THEN 'Tech'
>         WHEN 'Sales' THEN 'Revenue'
>         ELSE 'Other'
>     END AS dept_category
> FROM employees;
> ```

---

## Section 5: Data Definition & Manipulation (DDL, DML, DCL)

### Creating & Modifying Tables

```sql
-- Comprehensive CREATE TABLE
CREATE TABLE employees (
    id              INT AUTO_INCREMENT PRIMARY KEY COMMENT 'Surrogate key',
    email           VARCHAR(255) NOT NULL UNIQUE,
    first_name      VARCHAR(50) NOT NULL,
    last_name       VARCHAR(50) NOT NULL,
    salary          DECIMAL(10,2) CHECK (salary >= 0),
    department_id   INT,
    hire_date       DATE DEFAULT (CURRENT_DATE),
    is_active       TINYINT(1) DEFAULT 1,
    metadata        JSON,
    
    -- Foreign key with ON DELETE/UPDATE actions
    CONSTRAINT fk_dept 
        FOREIGN KEY (department_id) 
        REFERENCES departments(id)
        ON DELETE SET NULL      -- Keep employee if dept deleted
        ON UPDATE CASCADE,      -- Update dept_id if departments.id changes
    
    -- Table-level constraint
    CONSTRAINT chk_names CHECK (first_name <> last_name)
) ENGINE=InnoDB 
  DEFAULT CHARSET=utf8mb4 
  COMMENT='Company employees';
```

**ALTER TABLE operations:**
```sql
-- Add column
ALTER TABLE employees ADD phone VARCHAR(20);

-- Add column with position (MySQL)
ALTER TABLE employees ADD middle_name VARCHAR(50) AFTER first_name;

-- Modify column type
ALTER TABLE employees MODIFY phone VARCHAR(30);

-- Rename column (MySQL)
ALTER TABLE employees CHANGE phone mobile_phone VARCHAR(30);

-- Rename column (PostgreSQL / standard)
ALTER TABLE employees RENAME COLUMN phone TO mobile_phone;

-- Drop column
ALTER TABLE employees DROP COLUMN phone;

-- Add index
ALTER TABLE employees ADD INDEX idx_hire_date (hire_date);

-- Drop foreign key
ALTER TABLE employees DROP FOREIGN KEY fk_dept;
```

### INSERT, UPDATE, DELETE vs TRUNCATE

```sql
-- INSERT: Add data
INSERT INTO employees (email, first_name, last_name, salary)
VALUES ('alice@co.com', 'Alice', 'Smith', 75000);

-- Bulk insert
INSERT INTO employees (email, first_name, last_name, salary)
VALUES 
    ('bob@co.com', 'Bob', 'Jones', 80000),
    ('carol@co.com', 'Carol', 'White', 90000);

-- INSERT from SELECT
INSERT INTO employees_archive (id, email, name)
SELECT id, email, CONCAT(first_name, ' ', last_name)
FROM employees WHERE is_active = 0;

-- UPDATE: Modify data (ALWAYS use WHERE!)
UPDATE employees 
SET salary = salary * 1.1, last_raise = CURDATE()
WHERE performance_rating = 'Exceeds';

-- UPDATE with JOIN (MySQL)
UPDATE employees e
JOIN departments d ON e.department_id = d.id
SET e.salary = e.salary * 1.05
WHERE d.location = 'San Francisco';

-- DELETE: Remove rows (ALWAYS use WHERE!)
DELETE FROM employees WHERE id = 42;

-- DELETE with JOIN
DELETE e FROM employees e
JOIN departments d ON e.department_id = d.id
WHERE d.name = 'Dissolved Team';
```

**TRUNCATE vs DELETE vs DROP:**

```
┌──────────────────────────────────────────────────────────────────────────────┐
│              DELETE vs TRUNCATE vs DROP — THE SHOWDOWN                       │
├─────────────┬─────────────┬─────────────┬────────────────────────────────────┤
│ Aspect      │ DELETE      │ TRUNCATE    │ DROP                               │
├─────────────┼─────────────┼─────────────┼────────────────────────────────────┤
│ Type        │ DML         │ DDL         │ DDL                                │
│ WHERE       │ Yes         │ No          │ N/A (whole object)                 │
│ Speed       │ Slow (row)  │ Fast (page) │ Fast                               │
│ Logging     │ Row-level   │ Page-level  │ Minimal                            │
│ Rollback    │ Yes         │ Sometimes   │ No                                 │
│ Triggers    │ Fires       │ Doesn't fire│ N/A                                │
│ Identity    │ Preserved   │ Reset       │ N/A                                │
│ Structure   │ Kept        │ Kept        │ DESTROYED                          │
│ Use case    │ Remove some │ Empty table │ Remove table forever               │
└─────────────┴─────────────┴─────────────┴────────────────────────────────────┘
```

### Constraints & Integrity

| Constraint | Purpose | NULL Allowed? |
|------------|---------|---------------|
| `PRIMARY KEY` | Unique identifier | No |
| `UNIQUE` | No duplicates | Yes (one NULL usually) |
| `NOT NULL` | Must have value | — |
| `FOREIGN KEY` | Referential integrity | Yes (optional relationship) |
| `CHECK` | Value condition | Depends |
| `DEFAULT` | Auto-fill if omitted | — |

```sql
-- UNIQUE allows multiple NULLs (in most DBs)
CREATE TABLE users (
    email VARCHAR(255) UNIQUE  -- NULL ≠ NULL in SQL, so multiple NULLs OK
);

-- CHECK constraint
CREATE TABLE products (
    price DECIMAL(10,2) CHECK (price > 0),
    discount DECIMAL(3,2) CHECK (discount BETWEEN 0 AND 1)
);
```

---

### Q&A Bank (Questions 61-91)

**61. Different types of SQL statements?**
> DDL (CREATE, ALTER, DROP, TRUNCATE), DML (INSERT, UPDATE, DELETE, SELECT), DQL (SELECT — sometimes grouped with DML), DCL (GRANT, REVOKE), TCL (COMMIT, ROLLBACK, SAVEPOINT).

**62. Which statements are DDL?**
> `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`.

**63. DML includes?**
> `SELECT`, `INSERT`, `UPDATE`, `DELETE`.

**64. GRANT and REVOKE are under?**
> **DCL** (Data Control Language).

**65. Which is NOT a DML statement?**
> `COMMIT` — it's **TCL** (Transaction Control Language). Also `CREATE`, `GRANT`, `TRUNCATE` are not DML.

**66. Which statement inserts new data?**
> `INSERT INTO`.

**67. Must you specify columns when inserting?**
> No, if you provide values for ALL columns in the exact table order. But **best practice**: always specify columns. It prevents errors when schema changes and is self-documenting.
> ```sql
> -- Risky: breaks if columns are reordered
> INSERT INTO customers VALUES (1, 'John', 'Doe');
> 
> -- Safe: explicit and clear
> INSERT INTO customers (id, first_name, last_name) VALUES (1, 'John', 'Doe');
> ```

**68. Insert a new record into Customers?**
> ```sql
> INSERT INTO Customers (id, first_name, last_name) VALUES (1, 'John', 'Doe');
> ```

**69. Insert "Hawkins" as LastName in Customers?**
> ```sql
> INSERT INTO Customers (LastName) VALUES ('Hawkins');
> ```

**70. How to create a temporary table in MySQL?**
> ```sql
> CREATE TEMPORARY TABLE temp_top_customers
> SELECT * FROM customers WHERE total_spent > 10000;
> ```
> It exists only for the current session/connection and is automatically dropped when the session ends.

**71. Which statement updates data?**
> `UPDATE`.

**72. Keyword in UPDATE to change values?**
> `SET`.

**73. Change "Jackson" to "Hawkins" in LastName?**
> ```sql
> UPDATE Customers SET LastName = 'Hawkins' WHERE LastName = 'Jackson';
> ```
> ⚠️ *Without WHERE, every row becomes Hawkins!*

**74. Which statement deletes data?**
> `DELETE`.

**75. Delete records where FirstName is "John"?**
> ```sql
> DELETE FROM Customers WHERE FirstName = 'John';
> ```

**76. What is FROM used for?**
> Specifies the source table(s) for `SELECT`, `UPDATE`, `DELETE`, and `INSERT`.

**77. DELETE vs TRUNCATE?**
> See the comparison table above. Key differences: `DELETE` is DML (row-by-row, rollbackable, fires triggers, has WHERE). `TRUNCATE` is DDL (bulk page deallocation, faster, no WHERE, resets auto-increment, doesn't fire triggers).

**78. Which statement creates a table?**
> `CREATE TABLE`.

**79. What is Collation?**
> Collation defines the **rules for comparing and sorting** characters. It works with the character set.
> - `utf8mb4_general_ci`: Case-insensitive, faster
> - `utf8mb4_unicode_ci`: Case-insensitive, accurate for all Unicode
> - `utf8mb4_bin`: Binary comparison (case-sensitive)
> ```sql
> SELECT * FROM users WHERE name = 'john'; -- Matches 'John' with _ci collation
> ```

**80. What is AUTO_INCREMENT?**
> Automatically generates sequential unique integers for a column, typically the PRIMARY KEY.
> ```sql
> CREATE TABLE users (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50));
> INSERT INTO users (name) VALUES ('Alice');  -- id becomes 1 automatically
> ```
> In PostgreSQL, use `SERIAL` or `GENERATED ALWAYS AS IDENTITY`. In SQL Server, `IDENTITY(1,1)`.

**81. Valid constraints in MySQL?**
> `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, `CHECK`, `DEFAULT`, `AUTO_INCREMENT`.

**82. Which is NOT TRUE about constraints?**
> Any statement claiming constraints hurt data integrity or are optional in production is false. Constraints are essential for data quality.

**83. NOT NULL constraint?**
> Forces a column to reject NULL values. Every row must have a value.

**84. An unique (non-key) field?**
> Use the `UNIQUE` constraint. Unlike PRIMARY KEY, a table can have multiple UNIQUE constraints, and they typically allow one NULL.

**85. What is CHECK constraint?**
> Enforces a boolean condition on every row:
> ```sql
> CREATE TABLE persons (age INT CHECK (age >= 0 AND age <= 150));
> ```

**86. UNIQUE vs PRIMARY KEY?**
> | PRIMARY KEY | UNIQUE |
> |-------------|--------|
> | One per table | Multiple per table |
> | Cannot be NULL | Usually allows one NULL |
> | Implicitly indexed | Explicitly indexed |
> | Identifies the row | Alternate identifier |

**87. What does DROP TABLE do?**
> Permanently removes the table definition, all data, indexes, triggers, and constraints. **Cannot be undone** (unless in a transaction that rolls back, in some DBs).
> ```sql
> DROP TABLE IF EXISTS old_customers;
> ```

**88. DROP vs TRUNCATE?**
> `DROP` removes the table *structure*. `TRUNCATE` removes only the *data*, keeping the structure.

**89. Add `order_date` column to `order` table?**
> ```sql
> ALTER TABLE `order` ADD order_date DATE;
> ```
> Backticks escape reserved words. Better: rename the table to `orders`.

**90. Rename column Address to Addr in Customer?**
> ```sql
> -- MySQL
> ALTER TABLE Customer CHANGE Address Addr VARCHAR(50);
> -- PostgreSQL / Standard
> ALTER TABLE Customer RENAME COLUMN Address TO Addr;
> ```

**91. Delete column CITY from ADDRESSES?**
> ```sql
> ALTER TABLE addresses DROP COLUMN city;
> ```

---

## Section 6: Indexes, Privileges & Security

### How Indexes Work: The Library Analogy

Imagine a library with 1 million books. Finding a book without a catalog means checking every shelf — that's a **full table scan**. An index is the card catalog, organized alphabetically, letting you jump directly to the right shelf.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    TABLE SCAN vs INDEXED LOOKUP                              │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Without Index (Full Table Scan)              With Index (B-Tree)            │
│                                                                              │
│  📚 📚 📚 📚 📚 📚 📚 📚 📚 📚               [M]─────┐                      │
│  📚 📚 📚 📚 📚 📚 📚 📚 📚 📚              /         \                     │
│  📚 📚 📚 📚 📚 📚 📚 📚 📚 📚            [G]         [S]                   │
│  📚 📚 📚 📚 📚 📚 📚 📚 📚 📚           /   \       /   \                  │
│  📚 📚 📚 📚 📚 📚 📚 📚 📚 📚         [C]   [J]   [P]   [W]               │
│       ↑                                      |    |    |    |                │
│   Check EVERY book                        Look up 'Smith': go right to S     │
│   O(n) — slow for large n               O(log n) — scales to billions        │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

```sql
-- Create a basic index
CREATE INDEX idx_email ON users(email);

-- Create a UNIQUE index (also enforces uniqueness)
CREATE UNIQUE INDEX idx_username ON users(username);

-- Composite index (multi-column)
CREATE INDEX idx_name_age ON users(last_name, first_name, age);

-- Prefix index (for long text columns)
CREATE INDEX idx_bio_prefix ON users(bio(100));

-- Covering index (includes all columns needed for a query)
CREATE INDEX idx_covering ON orders(customer_id, status, total) 
INCLUDE (created_at);  -- PostgreSQL / SQL Server syntax
```

### Clustered vs Non-Clustered Indexes

```
┌──────────────────────────────────────────────────────────────────────────────┐
│              CLUSTERED vs NON-CLUSTERED INDEX                                │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  CLUSTERED INDEX                  NON-CLUSTERED INDEX                        │
│  (Only ONE per table)             (Many per table)                           │
│                                                                              │
│  The table IS the index.          The index is a SEPARATE structure.         │
│                                                                              │
│  ┌─────────────────┐              ┌──────────────┐     ┌─────────────────┐   │
│  │ ID │ Data       │              │ Index Key    │────→│ ID │ Data       │   │
│  ├────┼────────────┤              ├──────────────┤     ├────┼────────────┤   │
│  │ 1  │ Alice, ... │              │ Alice → 1    │     │ 1  │ Alice, ... │   │
│  │ 2  │ Bob, ...   │              │ Bob   → 2    │     │ 2  │ Bob, ...   │   │
│  │ 3  │ Carol, ... │              │ Carol → 3    │     │ 3  │ Carol, ... │   │
│  └────┴────────────┘              └──────────────┘     └─────────────────┘   │
│                                                                              │
│  Data stored IN ORDER.           Index contains pointers to actual rows.     │
│  Physically reorders table.      Index + lookup required.                    │
│  Range queries are blazing fast. Extra storage overhead.                     │
│                                                                              │
│  MySQL InnoDB: PK is clustered.  MySQL: Secondary indexes point to PK.       │
│  SQL Server: Can choose.         PostgreSQL: Only non-clustered (Heap).      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### SQL Injection: The #1 Security Threat

SQL injection happens when user input is concatenated directly into a query. It's the most dangerous and common database vulnerability.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    THE SQL INJECTION ATTACK                                  │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  VULNERABLE CODE:                                                            │
│  query = "SELECT * FROM users WHERE username = '" + input + "'";            │
│                                                                              │
│  ATTACKER INPUTS:              RESULTING QUERY:                              │
│  ' OR '1'='1                   SELECT * FROM users WHERE username = ''       │
│                                 OR '1'='1'  ← ALWAYS TRUE!                   │
│                                                                              │
│  RESULT: Returns ALL users. Attacker is now logged in as everyone.           │
│                                                                              │
│  WORSE INPUT:                                                                │
│  '; DROP TABLE users; --                                                      │
│                                                                              │
│  RESULTING QUERY:                                                            │
│  SELECT * FROM users WHERE username = ''; DROP TABLE users; --'              │
│                                                                              │
│  RESULT: Your users table is GONE.                                           │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

**The Fix: Always Use Parameterized Queries / Prepared Statements**

```python
# ❌ BAD — String concatenation (NEVER DO THIS)
cursor.execute(f"SELECT * FROM users WHERE id = {user_input}")

# ✅ GOOD — Parameterized query (database escapes input)
cursor.execute("SELECT * FROM users WHERE id = %s", (user_input,))

# ✅ GOOD — Prepared statement
stmt = db.prepare("SELECT * FROM users WHERE id = ?")
stmt.execute(user_input)
```

```sql
-- ❌ VULNERABLE
SELECT * FROM users WHERE email = '$email';

-- ✅ SAFE (Prepared statement)
SELECT * FROM users WHERE email = ?;
```

---

### Q&A Bank (Questions 92-96, 115)

**92. What are Indexes?**
> Data structures (typically B-Trees) that speed up data retrieval at the cost of slower writes and extra storage. Think of them as a book's table of contents.

**93. Clustered vs Non-Clustered?**
> - **Clustered**: Determines physical storage order. One per table. The data IS the index.
> - **Non-Clustered**: Separate structure with pointers to data. Multiple allowed per table.
> - Clustered indexes excel at range queries. Non-clustered are more flexible.

**94. Statement for assigning privileges?**
> `GRANT`. To remove: `REVOKE`.
> ```sql
> GRANT SELECT, INSERT ON database.orders TO 'app_user'@'%';
> REVOKE DELETE ON database.orders FROM 'app_user'@'%';
> ```

**95. Types of privileges?**
> 1. **System privileges**: CREATE, DROP, ALTER (database-level)
> 2. **Object privileges**: SELECT, INSERT, UPDATE, DELETE, EXECUTE (table/procedure-level)

**96. Privileges a user can grant?**
> `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `REFERENCES`, `EXECUTE`, `USAGE`, `ALL PRIVILEGES`.

**115. What is SQL Injection?**
> A code injection attack where malicious SQL is inserted via user input. Prevention:
> 1. **Parameterized queries** (prepared statements)
> 2. **Input validation**
> 3. **ORM frameworks** (most handle escaping automatically)
> 4. **Least privilege** (app user shouldn't have DROP permissions)
> 5. **Stored procedures** with parameters

---

## Section 7: Transactions, ACID & Concurrency

### The Bank Transfer Analogy

The classic example: Alice sends $100 to Bob. Two operations must happen:
1. Subtract $100 from Alice's account
2. Add $100 to Bob's account

If the system crashes after step 1, $100 vanishes into thin air. A **transaction** wraps both steps into an atomic unit.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    THE BANK TRANSFER TRANSACTION                             │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  BEGIN;                                                                      │
│                                                                              │
│  ┌─────────────────┐          ┌─────────────────┐                           │
│  │ Alice: $500     │          │ Bob:   $300     │                           │
│  │                 │          │                 │                           │
│  │  [- $100]       │────┐     │                 │                           │
│  │  $400           │    │     │  [+ $100]       │                           │
│  │                 │◄───┘     │  $400           │                           │
│  └─────────────────┘          └─────────────────┘                           │
│                                                                              │
│  ↓ If everything succeeds:          ↓ If anything fails:                     │
│  COMMIT;                            ROLLBACK;                                │
│  (Permanent)                        (Undo everything)                        │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### ACID Properties Explained

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                         ACID PROPERTIES                                      │
├──────────────┬───────────────────────────────────────────────────────────────┤
│ ATOMICITY    │ All operations complete, or none do.                        │
│              │ "All or nothing." No partial commits.                       │
│              │ Analogy: Wedding vows — both say "I do" or neither does.    │
├──────────────┼───────────────────────────────────────────────────────────────┤
│ CONSISTENCY  │ Database moves from one valid state to another.             │
│              │ Constraints, triggers, and cascades must all succeed.       │
│              │ Analogy: A legal contract — every clause must be valid.     │
├──────────────┼───────────────────────────────────────────────────────────────┤
│ ISOLATION    │ Concurrent transactions don't interfere with each other.    │
│              │ Each transaction sees a consistent snapshot.                │
│              │ Analogy: Private changing rooms — you don't see others.     │
├──────────────┼───────────────────────────────────────────────────────────────┤
│ DURABILITY   │ Once committed, data survives power loss/crashes.           │
│              │ Written to disk / WAL (Write-Ahead Log).                    │
│              │ Analogy: Etching in stone — permanent once done.            │
└──────────────┴───────────────────────────────────────────────────────────────┘
```

### Isolation Levels & The Three Read Phenomena

When multiple transactions run at the same time, without isolation, three weird things can happen:

```
┌──────────────────────────────────────────────────────────────────────────────┐
│               THE THREE READ PHENOMENA (Bad Things That Happen)              │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  1. DIRTY READ                    2. NON-REPEATABLE READ                     │
│                                                                              │
│  T1 reads uncommitted data.      T1 reads a row. T2 updates it. T1          │
│  T1: SELECT → 100                reads again → different value!              │
│  T2: UPDATE → 200 (not committed)                                            │
│  T1: SELECT → 200  ← DIRTY!                                                  │
│                                                                              │
│  3. PHANTOM READ                                                             │
│  T1: SELECT WHERE age > 30 → 5 rows                                          │
│  T2: INSERT new person age 35 (committed)                                    │
│  T1: SELECT WHERE age > 30 → 6 rows  ← PHANTOM!                              │
│  The "ghost" row appeared.                                                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

**Isolation Levels (from least to most strict):**

| Level | Dirty Read | Non-Repeatable | Phantom | Use Case |
|-------|-----------|----------------|---------|----------|
| **READ UNCOMMITTED** | ✅ Allowed | ✅ Allowed | ✅ Allowed | Rarely used; reporting on huge tables |
| **READ COMMITTED** | ❌ Blocked | ✅ Allowed | ✅ Allowed | Oracle / SQL Server default |
| **REPEATABLE READ** | ❌ Blocked | ❌ Blocked | ✅ Allowed | MySQL InnoDB default |
| **SERIALIZABLE** | ❌ Blocked | ❌ Blocked | ❌ Blocked | Financial transactions |

```sql
-- Check/set isolation level (MySQL)
SELECT @@transaction_isolation;
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- PostgreSQL
SHOW default_transaction_isolation;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

### Locks & Deadlocks

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                         DEADLOCK ILLUSTRATION                                │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Transaction A              Transaction B                                    │
│  ─────────────              ─────────────                                    │
│  LOCK row 1                 LOCK row 2                                       │
│       ↓                          ↓                                           │
│  WAIT for row 2 ←──── BLOCKED ─→ WAIT for row 1                              │
│       ↓                          ↓                                           │
│  💀 DEADLOCK 💀                                                              │
│                                                                              │
│  Database detects this and kills one transaction (ROLLBACK).                 │
│  Your app should catch deadlock errors and retry.                            │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

```sql
-- Explicit locking (PostgreSQL)
SELECT * FROM accounts WHERE id = 1 FOR UPDATE;

-- Optimistic locking with version column
UPDATE accounts 
SET balance = balance - 100, version = version + 1
WHERE id = 1 AND version = 5;  -- If version changed, 0 rows updated → retry
```

---

### Q&A Bank (Questions 97-104)

**97. What does "locking" refer to?**
> A mechanism to prevent concurrent transactions from interfering with each other. Locks can be **shared** (read locks, multiple allowed) or **exclusive** (write locks, only one allowed).

**98. Main transaction controls?**
> - `COMMIT` — Make changes permanent
> - `ROLLBACK` — Undo all changes in the transaction
> - `SAVEPOINT` — Set a partial rollback point
> ```sql
> START TRANSACTION;
> UPDATE accounts SET balance = balance - 100 WHERE id = 1;
> SAVEPOINT before_credit;
> UPDATE accounts SET balance = balance + 100 WHERE id = 2;
> -- Oops, wrong account!
> ROLLBACK TO SAVEPOINT before_credit;
> -- Now retry with correct account
> COMMIT;
> ```

**99. A transaction that completes execution is said to be?**
> **Committed**.

**100. What does ROLLBACK do after COMMIT?**
> **Nothing.** Once `COMMIT` is executed, changes are permanent. `ROLLBACK` only works on uncommitted changes.

**101. Valid properties of a transaction?**
> **ACID**: Atomicity, Consistency, Isolation, Durability.

**102. What if autocommit is enabled?**
> Every individual statement is automatically committed. In MySQL, autocommit is ON by default. Turn it off for multi-statement transactions:
> ```sql
> SET autocommit = 0;
> -- ... multiple statements ...
> COMMIT;
> SET autocommit = 1;
> ```

**103. Default isolation level in MySQL?**
> **REPEATABLE READ** (InnoDB engine). Prevents dirty reads and non-repeatable reads, but phantom reads are possible (though InnoDB uses MVCC + gap locking to mostly prevent them).

**104. Is autocommit enabled by default in MySQL?**
> **Yes**, for each new session.

---

## Section 8: Views, Stored Procedures, Triggers & Cursors

### Views

A **View** is a stored SELECT query — a virtual table. It doesn't store data (unless it's a **materialized view**), but provides a consistent interface.

```sql
-- Simple view
CREATE VIEW active_customers AS
SELECT id, name, email FROM customers WHERE status = 'active';

-- Complex view with joins
CREATE VIEW order_summary AS
SELECT 
    o.id AS order_id,
    c.name AS customer_name,
    SUM(oi.quantity * oi.price) AS total
FROM orders o
JOIN customers c ON o.customer_id = c.id
JOIN order_items oi ON o.id = oi.order_id
GROUP BY o.id, c.name;

-- Query it like a table
SELECT * FROM order_summary WHERE total > 1000;
```

**Updatable Views** (can use INSERT/UPDATE/DELETE):
- Must reference exactly one base table
- Cannot contain DISTINCT, GROUP BY, aggregates, or UNION
- Must include all NOT NULL columns without defaults

```sql
-- Materialized view (PostgreSQL) — stores actual data, needs refresh
CREATE MATERIALIZED VIEW monthly_sales AS
SELECT DATE_TRUNC('month', order_date) AS month, SUM(total) 
FROM orders GROUP BY 1;

REFRESH MATERIALIZED VIEW monthly_sales;
```

### Stored Procedures vs Functions

```sql
-- MySQL Stored Procedure
DELIMITER //
CREATE PROCEDURE TransferMoney(
    IN from_account INT,
    IN to_account INT,
    IN amount DECIMAL(10,2)
)
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        RESIGNAL;
    END;
    
    START TRANSACTION;
    UPDATE accounts SET balance = balance - amount WHERE id = from_account;
    UPDATE accounts SET balance = balance + amount WHERE id = to_account;
    COMMIT;
END //
DELIMITER ;

-- Call it
CALL TransferMoney(1, 2, 100.00);
```

| | Stored Procedure | Function |
|---|------------------|----------|
| Returns | Can return multiple result sets | Must return exactly one value |
| Called with | `CALL proc_name()` | Used in expressions: `SELECT func()` |
| Side effects | Yes (can modify data) | Usually no (deterministic) |
| Transactions | Can manage transactions | Cannot (in most DBs) |

### Triggers

Triggers auto-execute when an event occurs. Useful for auditing, but use sparingly — they hide logic.

```sql
-- Audit trigger: log all salary changes
CREATE TRIGGER trg_salary_audit
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    IF OLD.salary <> NEW.salary THEN
        INSERT INTO salary_audit (emp_id, old_salary, new_salary, changed_at)
        VALUES (NEW.id, OLD.salary, NEW.salary, NOW());
    END IF;
END;

-- Trigger types:
-- BEFORE INSERT/UPDATE/DELETE → Validate/modify data before it hits the table
-- AFTER  INSERT/UPDATE/DELETE → Log, cascade, notify
-- INSTEAD OF (views only)     → Redirect operations
```

### Cursors

Cursors iterate row-by-row. They're slow — avoid them if set-based operations work.

```sql
-- MySQL cursor example
DELIMITER //
CREATE PROCEDURE ProcessEmployees()
BEGIN
    DECLARE done INT DEFAULT FALSE;
    DECLARE emp_name VARCHAR(100);
    DECLARE emp_salary DECIMAL(10,2);
    
    DECLARE emp_cursor CURSOR FOR 
        SELECT name, salary FROM employees WHERE department = 'Sales';
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;
    
    OPEN emp_cursor;
    read_loop: LOOP
        FETCH emp_cursor INTO emp_name, emp_salary;
        IF done THEN LEAVE read_loop; END IF;
        -- Process each row here
    END LOOP;
    CLOSE emp_cursor;
END //
DELIMITER ;
```

---

### Q&A Bank (Questions 105-114)

**105. What is a virtual table in MySQL?**
> A **View**.

**106. Are views updatable?**
> Some are. Requirements: based on a single table, no aggregates/DISTINCT/GROUP BY/UNION, includes primary key, and all NOT NULL columns.

**107. Advantages of views?**
> 1. **Simplify complex queries** — hide JOINs and aggregations
> 2. **Security** — expose only specific columns/rows
> 3. **Logical independence** — shield apps from schema changes
> 4. **Consistency** — same calculation logic everywhere

**108. Does a view contain data?**
> Regular views: **No** (virtual, query executed on access). Materialized views: **Yes** (stored data, needs refresh).

**109. How to remove a view?**
> ```sql
> DROP VIEW IF EXISTS order_summary;
> ```

**110. Can a view be based on another view?**
> Yes — nested views. Be careful with deep nesting as it hurts performance and readability.

**111. Iterate over rows in a stored procedure?**
> Use a **CURSOR**. Lifecycle: `DECLARE` → `OPEN` → `FETCH` → `CLOSE`.

**112. Process of finding a good query execution strategy?**
> **Query optimization**. The database's query optimizer generates multiple execution plans and picks the cheapest one based on statistics, indexes, and cost models. You can inspect plans with `EXPLAIN`.

**113. What is a trigger?**
> A stored procedure that automatically executes in response to a DML event (INSERT, UPDATE, DELETE) or DDL event (CREATE, ALTER, DROP). Components: **Event** (when), **Condition** (optional), **Action** (what to do).

**114. A stored procedure auto-executing on INSERT/UPDATE/DELETE?**
> A **Trigger**.

---

## Section 9: Query Optimization & Execution Plans

### Reading EXPLAIN Output

The `EXPLAIN` command shows how the database plans to execute your query. It's the **X-ray** for SQL performance.

```sql
EXPLAIN SELECT * FROM employees WHERE email = 'alice@co.com';

-- PostgreSQL (more detailed)
EXPLAIN (ANALYZE, BUFFERS) SELECT * FROM employees WHERE email = 'alice@co.com';
```

**Key columns to watch (MySQL):**

| Column | Meaning | Red Flags |
|--------|---------|-----------|
| `type` | Join type | `ALL` = full table scan (bad). Aim for `const`, `eq_ref`, `ref`, `range`. |
| `possible_keys` | Indexes considered | Empty = no useful indexes exist |
| `key` | Index actually used | NULL = no index used |
| `rows` | Rows examined | Should be much smaller than table size |
| `Extra` | Additional info | `Using filesort` (bad), `Using temporary` (bad), `Using index` (great!) |

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    EXPLAIN OUTPUT CHEAT SHEET                                │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  TYPE column (best to worst):                                                │
│                                                                              │
│  const    → PK lookup on constant        [BEST]                              │
│  eq_ref   → PK/unique join              ★★★★★                                │
│  ref      → Non-unique index match      ★★★★☆                                │
│  range    → Index range scan            ★★★☆☆                                │
│  index    → Full index scan             ★★☆☆☆                                │
│  ALL      → Full TABLE scan (NO!)       ★☆☆☆☆                                │
│                                                                              │
│  EXTRA column:                                                               │
│  Using index        → COVERING INDEX (doesn't touch table!) [GREAT]          │
│  Using where        → Filtering after index lookup           [OK]            │
│  Using filesort     → Sorting without index                  [SLOW]          │
│  Using temporary    → Created temp table                     [SLOW]          │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### The 10 Query Performance Killers

1. **`SELECT *`** — Pulls unnecessary data; prevents covering indexes.
2. **Functions on indexed columns** — `WHERE YEAR(date_col) = 2023` can't use index. Use `WHERE date_col BETWEEN '2023-01-01' AND '2023-12-31'`.
3. **Leading wildcard LIKE** — `LIKE '%smith'` can't use B-Tree index. Use full-text search instead.
4. **Implicit conversions** — Comparing string column to number forces conversion; index ignored.
5. **Missing indexes on JOIN/FK columns** — Foreign keys should almost always be indexed.
6. **N+1 queries** — Fetching related data in a loop. Use JOINs or `IN (...)`.
7. **Large OFFSET** — `OFFSET 1000000` scans and discards 1M rows. Use keyset pagination.
8. **Sorting without index** — `ORDER BY` on unindexed columns triggers filesort.
9. **Subqueries in SELECT** — Correlated subqueries run once per row; use JOINs instead.
10. **Not analyzing tables** — Stale statistics lead to bad plans. Run `ANALYZE TABLE`.

---

## Section 10: Database Design & Normalization

### 1NF, 2NF, 3NF, BCNF

Normalization eliminates redundancy and prevents anomalies (insert, update, delete). Think of it as organizing a closet — each item has one specific place.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                    NORMALIZATION LEVELS VISUALIZED                           │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  BEFORE NORMALIZATION (A Mess)                                             │
│  ┌────────────┬───────────┬────────────────────────────┬──────────┐          │
│  │ Student    │ Course    │ Instructor                 │ Office   │          │
│  ├────────────┼───────────┼────────────────────────────┼──────────┤          │
│  │ Alice      │ Math,Phys │ Prof. Smith, Prof. Jones   │ 101, 205 │          │
│  │ Bob        │ Math      │ Prof. Smith                │ 101      │          │
│  └────────────┴───────────┴────────────────────────────┴──────────┘          │
│  Problems: Repeating groups, redundancy, update anomaly (move office 3x)     │
│                                                                              │
│  1NF → Atomic values, no repeating groups                                    │
│  2NF → No partial dependencies (all non-key columns depend on WHOLE key)     │
│  3NF → No transitive dependencies (no column depends on non-key column)      │
│  BCNF → Every determinant is a candidate key                                 │
│                                                                              │
│  AFTER 3NF (Clean & Organized)                                             │
│  Students(id, name)      Courses(id, name)     Instructors(id, name, office) │
│  Enrollments(student_id, course_id, instructor_id)                           │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

**The Rules in Detail:**

| Normal Form | Rule | Violation Example |
|-------------|------|-------------------|
| **1NF** | All columns atomic (no lists/arrays in a cell) | `courses: "Math, Physics"` |
| **2NF** | No partial dependency (only relevant for composite keys) | Price depends on `product_id` but not `order_id` in an `order_items` table |
| **3NF** | No transitive dependency | `employee` table has `dept_name` when it should just have `dept_id` |
| **BCNF** | Every determinant is a candidate key | A table with `(student, course) → instructor` and `instructor → course` |

### Denormalization: When to Break the Rules

Normalization optimizes for writes. Sometimes reads are so frequent you intentionally denormalize:

- **Counters**: Pre-computed `comment_count` on a blog post table
- **Derived columns**: Storing `total_price` when it's `qty * unit_price`
- **Materialized views**: Pre-aggregated reports
- **Star schemas**: Data warehouses intentionally use denormalized fact/dimension tables

**Trade-off**: Faster reads, but you must keep redundant data in sync (triggers, application logic, or batch jobs).

---

## 🎯 Final Interview Tips

### Before the Interview
- **Practice on paper** — Many interviews are whiteboard-based. Write queries without autocomplete.
- **Know your dialect** — If the job lists PostgreSQL, know `LIMIT/OFFSET`, `::cast`, `JSONB`, window functions.
- **Memorize execution order**: `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT`
- **Be ready to optimize** — "How would you make this faster?" → Indexes, query rewrite, partitioning.

### During the Interview
- **Clarify assumptions** — Ask about NULL handling, duplicates, tie-breaking.
- **Start simple, then refine** — Write a working query first, then optimize.
- **Talk through your logic** — Explain why you chose JOIN over subquery, or which index you'd add.
- **Mention edge cases** — What if two employees tie for highest salary? Use `RANK()` or `DENSE_RANK()`.

### Common Take-Home Patterns
| Pattern | Technique |
|---------|-----------|
| Running total / moving average | Window functions (`SUM() OVER`, `AVG() OVER`) |
| Top N per group | `ROW_NUMBER() OVER (PARTITION BY ...)` |
| Gaps in sequences | `LEAD()` / `LAG()` or self-join |
| Hierarchical data | Recursive CTEs |
| Pivot data | `CASE` aggregates or `PIVOT` (SQL Server/Oracle) |
| Duplicate detection | `GROUP BY ... HAVING COUNT(*) > 1` |
| Median calculation | `PERCENTILE_CONT()` or `NTILE()` |

---

## 📚 Resources & Further Reading

- **Practice**: [LeetCode Database](https://leetcode.com/problemset/database/), [HackerRank SQL](https://www.hackerrank.com/domains/sql), [SQLBolt](https://sqlbolt.com/)
- **Documentation**: [PostgreSQL Docs](https://www.postgresql.org/docs/), [MySQL Reference](https://dev.mysql.com/doc/)
- **Books**: *SQL Performance Explained* (Markus Winand), *Learning SQL* (Alan Beaulieu)
- **Visualization**: [Use The Index, Luke!](https://use-the-index-luke.com/) — Free online SQL indexing guide

---

> *"The most important SQL skill isn't memorizing syntax — it's knowing how to ask the right question of your data, and how the database will answer it."*
>
> Good luck with your interview! 🚀

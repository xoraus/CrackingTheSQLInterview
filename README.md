# Ultimate SQL Interview Guide

SQL (Structured Query Language) is the standard for managing and manipulating relational data. It includes commands for querying, updating, and defining database structures. This guide is divided into logical sections for easy navigation, with full theory explanations, code examples, diagrams (described in text for readability), and best practices. At the end of relevant sections, you'll find an enhanced Q&A bank (questions 1-114) drawn from common interview topics, expanded with clearer explanations, additional SQL snippets, and edge-case insights.

**Key Features of This Guide:**
- **Theory & Best Practices:** In-depth explanations with real-world applications.
- **Examples:** Runnable SQL code blocks for illustration.
- **Diagrams:** Text-based representations (e.g., ASCII art) where helpful for visualizing joins or transactions.
- **Q&A Bank:** 115 questions, polished and expanded for deeper understanding.
- **Assumptions:** Examples use MySQL syntax unless noted; adapt for other DBMS as needed.

**Tips for Interview Success:**
- Practice writing queries by hand—interviews often involve whiteboarding.
- Understand differences between DBMS (e.g., MySQL vs. Oracle).
- Focus on optimization: Indexes, query plans, and avoiding common pitfalls like SQL injection.
- Know ACID properties for transactions and normalization for schema design.

Let's dive in!

## Table of Contents

<!-- TOC start -->

- [Section 1: SQL Fundamentals](#section-1-sql-fundamentals)
    * [Theory](#theory)
    * [Examples](#examples)
    * [Q&A Bank (Questions 1-10)](#qa-bank-questions-1-10)
- [Section 2: Querying Data](#section-2-querying-data)
    * [Theory](#theory-1)
    * [Diagrams](#diagrams)
    * [Examples](#examples-1)
    * [Q&A Bank (Questions 11-42)](#qa-bank-questions-11-42)
- [Section 3: Joins and Set Operations](#section-3-joins-and-set-operations)
    * [Theory](#theory-2)
    * [Diagrams](#diagrams-1)
    * [Examples](#examples-2)
    * [Q&A Bank (Questions 43-54)](#qa-bank-questions-43-54)
- [Section 4: Subqueries and Advanced Queries](#section-4-subqueries-and-advanced-queries)
    * [Theory](#theory-3)
    * [Examples](#examples-3)
    * [Q&A Bank (Questions 55-60)](#qa-bank-questions-55-60)
- [Section 5: Data Definition and Manipulation (DDL, DML, DCL)](#section-5-data-definition-and-manipulation-ddl-dml-dcl)
    * [Theory](#theory-4)
    * [Examples](#examples-4)
    * [Q&A Bank (Questions 61-91)](#qa-bank-questions-61-91)
- [Section 6: Indexes, Privileges, and Security](#section-6-indexes-privileges-and-security)
    * [Theory](#theory-5)
    * [Examples](#examples-5)
    * [Q&A Bank (Questions 92-96, 115)](#qa-bank-questions-92-96-115)
- [Section 7: Transactions and Concurrency](#section-7-transactions-and-concurrency)
    * [Theory](#theory-6)
    * [Diagrams](#diagrams-2)
    * [Examples](#examples-6)
    * [Q&A Bank (Questions 97-104)](#qa-bank-questions-97-104)
- [Section 8: Views, Stored Procedures, Triggers, and Advanced Topics](#section-8-views-stored-procedures-triggers-and-advanced-topics)
    * [Theory](#theory-7)
    * [Examples](#examples-7)
    * [Q&A Bank (Questions 105-114)](#qa-bank-questions-105-114)

<!-- TOC end -->

## Section 1: SQL Fundamentals

### Theory
SQL is a declarative language for interacting with RDBMS. It was developed in the 1970s by IBM and standardized by ANSI. SQL handles data definition (DDL), manipulation (DML), control (DCL), and querying (DQL). Key commands include SELECT, INSERT, UPDATE, DELETE, CREATE, ALTER, and DROP.

Unlike procedural languages (e.g., PL/SQL), SQL focuses on *what* to do, not *how*. It supports standards but has vendor-specific extensions (e.g., MySQL's LIMIT vs. SQL Server's TOP).

**Best Practices:**
- Use consistent casing (e.g., uppercase keywords) for readability.
- Always quote string literals with single quotes.
- Avoid SELECT * in production; specify columns to reduce data transfer.
- Handle NULLs explicitly, as they represent unknown values and can affect comparisons.

### Examples
Basic SELECT:
```sql
-- Select all columns from a table
SELECT * FROM customers;
```

Handling NULLs:
```sql
-- Use IS NULL to check for missing values
SELECT * FROM products WHERE price IS NULL;
```

### Q&A Bank (Questions 1-10)
1. **SQL was developed as an integral part of**  
   SQL (Structured Query Language) is a domain-specific language for managing data in RDBMS or RDSMS. It's an ANSI standard with major commands like SELECT, UPDATE, DELETE, INSERT, and WHERE. SQL can query, insert/update/delete data, create databases/tables/views, and manage permissions. Vendor extensions (e.g., MySQL's proprietary functions) exist beyond the standard.  
   *Example:*  
   ```sql
   SELECT * FROM employees WHERE salary > 50000;
   ```

2. **What does SQL stand for?**  
   SQL stands for Structured Query Language. It accesses and manipulates databases and is an ANSI standard.

3. **SQL is (referring to it as a Programming Language)**  
   SQL is declarative: you specify the desired result without detailing steps (e.g., no need to manage indexes manually). It's non-procedural, unlike languages like C++ that require explicit operations. This abstraction makes SQL efficient for data tasks.

4. **Which of the following is NOT a SQL command? (SELECT, REMOVE, UPDATE, INSERT)**  
   REMOVE is not a valid SQL command. Use DELETE instead. Key commands: SELECT (extract), UPDATE (modify), DELETE (remove), INSERT INTO (add), CREATE/ALTER/DROP (for structures), and INDEX operations.

5. **What is MySQL?**  
   MySQL is an open-source RDBMS by Oracle, using SQL as its language. **Difference between SQL and MySQL:** SQL is the language; MySQL is the system implementing it.  
   *Best Practice:* Use MySQL for web apps due to its speed; consider PostgreSQL for complex transactions.

6. **What are some properties of PL/SQL?**  
   PL/SQL (Procedural Language/SQL) extends SQL with procedural features like loops and variables, developed by Oracle. It's embedded in Oracle Database alongside SQL and Java. **Difference between SQL and PL/SQL:** SQL is for single queries/DML; PL/SQL for full programs. SQL is data-oriented; PL/SQL is application-oriented. SQL executes statements individually; PL/SQL in blocks. SQL can embed in PL/SQL, but not vice versa.  
   *Example (PL/SQL block):*  
   ```sql
   BEGIN
     DBMS_OUTPUT.PUT_LINE('Hello, PL/SQL!');
   END;
   ```

7. **What are the possible values for the BOOLEAN data field in MySQL?**  
   MySQL uses TINYINT(1) for booleans: 0 is false, non-zero is true.  
   *Example:*  
   ```sql
   CREATE TABLE users (is_active TINYINT(1));
   INSERT INTO users VALUES (1);  -- True
   ```

8. **What data type would you choose if you wanted to store the distance (rounded to the nearest mile)?**  
   INTEGER (or INT) for whole numbers. Use DECIMAL for precision if needed.  
   *Best Practice:* Choose data types based on range and precision to optimize storage.

9. **Which are valid SQL keywords (statements & clauses)**  
   Valid: SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY, UPDATE, DELETE, INSERT INTO, CREATE/ALTER DATABASE/TABLE, DROP TABLE, CREATE/DROP INDEX.

10. **Which of the following are valid SQL comments?**  
    Single-line: `-- Comment`. Multi-line: `/* Comment */`. Comments explain code or prevent execution.  
    *Example:*  
    ```sql
    -- Single-line
    SELECT * FROM customers;  /* Multi-line comment */
    ```

## Section 2: Querying Data

### Theory
Querying uses SELECT to retrieve data, with clauses like FROM (source), WHERE (filter), ORDER BY (sort), LIMIT (paginate). Operators include =, >, LIKE (patterns), BETWEEN (ranges), IN (lists). Handle duplicates with DISTINCT; NULLs with IS NULL/IFNULL.

**Best Practices:**
- Use indexes on WHERE columns for speed.
- Avoid wildcard % at LIKE's start for performance.
- Combine conditions with AND/OR logically.
### Diagrams
Text-based JOIN visualization (later in Joins section).

### Examples
Pattern matching:
```sql
SELECT * FROM products WHERE name LIKE 'A%';  -- Starts with A
```

### Q&A Bank (Questions 11-42)
11. **Which SQL statement is used to extract data from a database?**  
    SELECT retrieves rows. Optional clauses: WHERE, GROUP BY, HAVING, ORDER BY, AS (aliases).  
    *Example:*  
    ```sql
    SELECT name AS full_name FROM customers WHERE age > 30 ORDER BY age DESC;
    ```

12. **How to select all records from the table 'Products'?**  
    ```sql
    SELECT * FROM products;
    ```  
    *Best Practice:* Avoid * in production; list columns explicitly.

13. **Can we rename a column in the output of SQL query?**  
    Yes, using AS for aliases.  
    *Example:*  
    ```sql
    SELECT first_name AS fname FROM customers;
    ```

14. **With SQL, how do you select a column named "FirstName" from a table named "Customers"?**  
    ```sql
    SELECT FirstName FROM Customers;
    ```

15. **What does the SQL FROM clause do?**  
    Specifies tables/joins for data extraction.

16. **Which SQL statement is used to return only different values?**  
    SELECT DISTINCT.  
    *Example:*  
    ```sql
    SELECT DISTINCT city FROM addresses;
    ```

17. **Consider the following schema ADDRESSES (id, street_name, number, city, state) Which of the following query would display the distinct cities in the ADDRESSES table?**  
    ```sql
    SELECT DISTINCT city FROM addresses;
    ```

18. **With SQL, how do you select all the records from a table named "Customers" where the value of the column "FirstName" is "John"?**  
    ```sql
    SELECT * FROM Customers WHERE FirstName = 'John';
    ```  
    Use single quotes for strings.

19. **The OR operator displays a record if ANY conditions listed are true. The AND operator displays a record if ALL of the conditions listed are true.**  
    True. Combine with NOT for negation.  
    *Example:*  
    ```sql
    SELECT * FROM customers WHERE age > 18 AND city = 'NY' OR status = 'active';
    ```

20. **Which of the following SQL statements has correct syntax?**  
    ```sql
    SELECT * FROM Table1 WHERE Column1 >= 100;
    ```  
    Comparison operators: =, >, <, >=, <=, !=.

21. **With SQL, how do you select all the records from a table named "Customers" where the "FirstName" is "John" and the "LastName" is "Jackson"?**  
    ```sql
    SELECT * FROM Customers WHERE FirstName = 'John' AND LastName = 'Jackson';
    ```

22. **How to select random 10 rows from a table?**  
    ```sql
    SELECT * FROM tbl ORDER BY RAND() LIMIT 10;
    ```  
    Performance note: Inefficient for large tables; consider alternatives like random IDs.

23. **Examine the following code. What will the value of price be if the statement finds a NULL value? SELECT name, ISNULL(price, 50) FROM PRODUCTS**  
    50 (default). NULL is not zero or empty. Use IFNULL (MySQL), COALESCE (standard), ISNULL (SQL Server), NVL (Oracle).  
    *Example:*  
    ```sql
    SELECT name, COALESCE(price, 50) FROM products;
    ```

24. **Which operator is used to search for a specified text pattern in a column?**  
    LIKE with % (multi-char wildcard) or _ (single-char).  
    *Examples:* 'a%' (starts with a), '%or%' (contains or).

25. **How to write a query to show the details of a student from Students table whose FirstName starts with 'K'?**  
    ```sql
    SELECT * FROM Students WHERE FirstName LIKE 'K%';
    ```

26. **Which operator is used to select values within a range?**  
    BETWEEN (inclusive).  
    *Example:*  
    ```sql
    SELECT * FROM sales WHERE date BETWEEN '2023-01-01' AND '2023-12-31';
    ```

27. **Which of the following SQL statements is correct?**  
    ```sql
    SELECT * FROM Sales WHERE Date BETWEEN '01/12/2017' AND '01/01/2018';
    ```

28. **With SQL, how do you select all the records from a table named "Customers" where the "LastName" is alphabetically between (and including) "Brooks" and "Gray"?**  
    ```sql
    SELECT * FROM Customers WHERE LastName BETWEEN 'Brooks' AND 'Gray';
    ```

29. **The 'IN' SQL keyword…**  
    Specifies multiple values or subqueries in WHERE. Shorthand for OR chains.  
    *Example:*  
    ```sql
    SELECT * FROM products WHERE category IN ('Electronics', 'Books');
    ```

30. **What does UPPER function do?**  
    Converts string to uppercase. Similar: LOWER, INITCAP.  
    *Example:*  
    ```sql
    SELECT UPPER(name) FROM customers;
    ```

31. **What function to use to round a number to the smallest integer value that is greater than or equal to a number?**  
    CEILING() or CEIL().  
    *Example:*  
    ```sql
    SELECT CEILING(25.3);  -- 26
    ```

32. **How to get current date in MySQL (without time)?**  
    CURDATE() or CURRENT_DATE(). Returns YYYY-MM-DD.  
    *Example:*  
    ```sql
    SELECT CURDATE();  -- e.g., 2025-08-20
    ```

33. **Which SQL keyword is used to retrieve a maximum value?**  
    MAX() aggregate.  
    *Example:*  
    ```sql
    SELECT MAX(salary) FROM employees;
    ```

34. **Which SQL functions is used to count the number of results?**  
    COUNT(). Ignores NULLs unless COUNT(*).  
    *Example:*  
    ```sql
    SELECT COUNT(id) FROM orders WHERE status = 'shipped';
    ```

35. **Which of the following are Aggregate Functions?**  
    COUNT, SUM, MIN, MAX, AVG. Used for summaries.

36. **With SQL, how can you return the number of records in the "Customers" table?**  
    ```sql
    SELECT COUNT(*) FROM Customers;
    ```

37. **Which 2 SQL keywords specify the sorting direction of the result set retrieved with ORDER BY clause?**  
    ASC (ascending, default), DESC (descending).  
    *Example:*  
    ```sql
    SELECT * FROM products ORDER BY price DESC, name ASC;
    ```

38. **If you don't specify ASC or DESC for an ORDER BY clause, the following is used by default:**  
    ASC.

39. **Suppose a Students table has two columns, name and mark. How to get name and mark of top three students?**  
    ```sql
    SELECT name, mark FROM Students ORDER BY mark DESC LIMIT 3;
    ```  
    Use TOP in SQL Server, ROWNUM in Oracle.

40. **With SQL, how can you return all the records from a table named "Customers" sorted descending by "FirstName"?**  
    ```sql
    SELECT * FROM Customers ORDER BY FirstName DESC;
    ```

41. **Which of the following SQL statements is correct?**  
    ```sql
    SELECT name, COUNT(name) FROM customers GROUP BY name;
    ```  
    GROUP BY aggregates subsets.

42. **What is the difference between HAVING clause and WHERE clause?**  
    WHERE filters rows before grouping; HAVING after (with aggregates). HAVING requires GROUP BY if used with aggregates.  
    *Example:*  
    ```sql
    SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 60000;
    ```  
    *Best Practice:* Use WHERE for individual row filters to reduce data early.

## Section 3: Joins and Set Operations

### Theory
Joins combine tables based on related columns. Types: INNER (matching), LEFT (all left + matching right), RIGHT (all right + matching left), FULL OUTER (all from both), SELF (table with itself), CROSS (Cartesian product). Set operations: UNION (combine, distinct), UNION ALL (with duplicates), INTERSECT (common), MINUS (first minus second).

**Best Practices:**
- Use aliases for readability in multi-table queries.
- Prefer INNER JOIN for efficiency unless outer matches are needed.
- Index join columns.

### Diagrams
Simple JOIN diagram (ASCII):
```
Table A: ID | Name
Table B: ID | City

INNER JOIN: Matching IDs only
LEFT JOIN: All A + matching B (NULL for non-matches)
```

### Examples
INNER JOIN:
```sql
SELECT customers.name, orders.amount 
FROM customers 
INNER JOIN orders ON customers.id = orders.customer_id;
```

### Q&A Bank (Questions 43-54)
43. **What is JOIN used for?**  
    Combines rows from multiple tables on related columns.

44. **What is the most common type of join?**  
    INNER JOIN (returns matching rows).

45. **What are different JOINS used in SQL?**  
    INNER, LEFT, RIGHT, FULL OUTER, SELF, CROSS. CROSS produces Cartesian if no WHERE.  
    *Example (LEFT JOIN):*  
    ```sql
    SELECT * FROM table1 LEFT JOIN table2 ON table1.id = table2.id;
    ```

46. **Which of the following is NOT TRUE about the ON clause?**  
    ON specifies join conditions/columns, eases readability, supports multi-way joins. All are true except if the question implies something false—clarify in interview.

47. **Assume that Table A is joined to Table B. An inner join:**  
    Displays rows where keys match.

48. **Can you join 3 tables together with inner join:**  
    Yes.  
    *Example:*  
    ```sql
    SELECT * FROM faculty f 
    INNER JOIN division d ON f.division_id = d.id 
    INNER JOIN country c ON f.country_id = c.id;
    ```

49. **Can you join a table to itself?**  
    Yes, SELF JOIN.  
    *Example:*  
    ```sql
    SELECT a.name, b.name FROM employees a, employees b WHERE a.manager_id = b.id;
    ```

50. **Which of the following is true about Cartesian Products?**  
    Formed without join condition (CROSS JOIN). Results in m*n rows.  
    *Example:*  
    ```sql
    SELECT * FROM table1 CROSS JOIN table2;
    ```

51. **In relational algebra the INTERSECTION of two sets (set A and Set B) corresponds to**  
    A AND B (common rows). Use INTERSECT.  
    *Example:*  
    ```sql
    SELECT * FROM set1 INTERSECT SELECT * FROM set2;
    ```

52. **In relational algebra the UNION of two sets (set A and Set B) corresponds to**  
    A OR B (combined, distinct). SELECTs must match columns/types/order.

53. **What is the difference between UNION and UNION ALL?**  
    UNION: distinct rows; UNION ALL: all rows (duplicates included). UNION ALL is faster.

54. **Having a list of Customer Names that searched for product 'X' and a list of customer Names that bought the product 'X'. What set operator would you use to get only those who are interested but did not bought product 'X' yet?**  
    MINUS (or EXCEPT in some DBMS).  
    *Example:*  
    ```sql
    SELECT name FROM searchers MINUS SELECT name FROM buyers;
    ```

## Section 4: Subqueries and Advanced Queries

### Theory
Subqueries are nested queries in SELECT/FROM/WHERE. Types: scalar (single value), row (multiple), correlated (depends on outer). Use for filtering, calculations. CASE for conditional logic. Functions like UPPER, CEILING for data transformation.

**Best Practices:**
- Use subqueries sparingly; joins often perform better.
- Correlated subqueries can be slow—optimize with EXISTS.
- Nest carefully to avoid performance hits.

### Examples
Subquery in WHERE:
```sql
SELECT * FROM products WHERE price > (SELECT AVG(price) FROM products);
```

CASE:
```sql
SELECT name, 
CASE WHEN age < 18 THEN 'Minor' ELSE 'Adult' END AS status 
FROM users;
```

### Q&A Bank (Questions 55-60)
55. **One (or more) select statement whose return values are used in filtering conditions of the main query is called**  
    Subquery (inner/nested query).

56. **Subqueries can be nested in...**  
    SELECT, INSERT, UPDATE, DELETE, or another subquery.

57. **What row comparison operators can be used with a subquery?**  
    IN, ANY, ALL, >, <, =.

58. **A subquery that is used inside a subquery is called a**  
    Nested subquery.

59. **A subquery that uses a correlation name from the outer query is called a**  
    Correlated subquery (depends on outer row).  
    *Example:*  
    ```sql
    SELECT * FROM employees e WHERE salary > (SELECT AVG(salary) FROM employees WHERE department = e.department);
    ```

60. **What is Case Function?**  
    Conditional logic like IF-THEN-ELSE.  
    *Example above.*

## Section 5: Data Definition and Manipulation (DDL, DML, DCL)

### Theory
DDL: Defines structures (CREATE, ALTER, DROP). DML: Manipulates data (INSERT, UPDATE, DELETE, SELECT—sometimes DQL). DCL: Controls access (GRANT, REVOKE). TRUNCATE (DDL) removes all rows without logging.

**Best Practices:**
- Use transactions with DML for rollback.
- Specify columns in INSERT for robustness.
- TRUNCATE for fast bulk deletes (no WHERE).

### Examples
CREATE TABLE:
```sql
CREATE TABLE customers (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL
);
```

INSERT:
```sql
INSERT INTO customers (name) VALUES ('John Doe');
```

### Q&A Bank (Questions 61-91)
61. **What are different types of statements supported by SQL?**  
    DDL (CREATE/ALTER/DROP), DML (INSERT/UPDATE/DELETE/SELECT), DCL (GRANT/REVOKE). SELECT sometimes in DQL.

62. **Which of the following SQL statements are DDL**  
    ALTER, CREATE, DROP, TRUNCATE TABLE.

63. **DML includes the following SQL statements**  
    SELECT, INSERT, UPDATE, DELETE.

64. **Grant and Revoke commands are under**  
    DCL.

65. **Which of the following is not a DML statement?**  
    COMMIT (transaction control, TCL).

66. **Which SQL statement is used to insert new data in a database?**  
    INSERT INTO.

67. **When inserting data in a table do you have to specify the list of columns you are inserting values for?**  
    No, if providing values for all columns in order. But best to specify for clarity.

68. **With SQL, how can you insert a new record into the "Customers" table?**  
    ```sql
    INSERT INTO Customers VALUES (1, 'John', 'Doe');
    ```

69. **With SQL, how can you insert "Hawkins" as the "LastName" in the "Customers" table?**  
    ```sql
    INSERT INTO Customers (LastName) VALUES ('Hawkins');
    ```

70. **How do you create a temporary table in MySQL?**  
    ```sql
    CREATE TEMPORARY TABLE temp_customers SELECT * FROM customers LIMIT 10;
    ```  
    Drops at session end.

71. **Which SQL statement is used to update data in a database?**  
    UPDATE.

72. **What is the keyword is used in an UPDATE query to modify the existing value?**  
    SET.

73. **How can you change "Jackson" into "Hawkins" in the "LastName" column in the Customer table?**  
    ```sql
    UPDATE Customers SET LastName = 'Hawkins' WHERE LastName = 'Jackson';
    ```

74. **Which SQL statement is used to delete data from a database?**  
    DELETE.

75. **With SQL, how can you delete the records where the "FirstName" is "John" in the Customers Table?**  
    ```sql
    DELETE FROM Customers WHERE FirstName = 'John';
    ```

76. **The FROM SQL keyword is used to**  
    Specify source table(s) in SELECT/UPDATE/DELETE/INSERT.

77. **What is the difference between DELETE and TRUNCATE?**  
    DELETE (DML): Row-by-row, loggable, WHERE clause, rollback possible. TRUNCATE (DDL): Bulk remove all rows, faster, no WHERE, resets auto-increment.

78. **Which SQL statement is used to create a table in a database?**  
    CREATE TABLE.

79. **What is Collation in SQL?**  
    Rules for comparing/sorting strings (e.g., case-sensitive). Character sets define symbols; collations define comparisons.  
    *Example:* Binary (simple encoding), case-insensitive.

80. **What is true about an AUTO_INCREMENT column in SQL?**  
    Generates unique numbers automatically on INSERT. Often PRIMARY KEY.  
    *MySQL Example:*  
    ```sql
    CREATE TABLE persons (id INT AUTO_INCREMENT PRIMARY KEY);
    ```

81. **What are valid constraints in MySQL?**  
    NOT NULL, UNIQUE, PRIMARY KEY (UNIQUE + NOT NULL), FOREIGN KEY, CHECK, DEFAULT, INDEX.

82. **Which of the following is NOT TRUE about constraints?**  
    All are true: Constraints enforce data integrity.

83. **The NOT NULL constraint enforces a column to not accept null values.**  
    True.

84. **An unique (non-key) field**  
    UNIQUE constraint (allows multiples per table, unlike PRIMARY KEY).

85. **What is CHECK Constraint?**  
    Limits values (e.g., age >= 18).  
    *Example:*  
    ```sql
    CREATE TABLE persons (age INT CHECK (age >= 18));
    ```

86. **What is the difference between UNIQUE and PRIMARY KEY constraints?**  
    PRIMARY KEY: UNIQUE + NOT NULL, one per table. UNIQUE: Multiple per table, allows NULLs (in some DBMS).

87. **What does SQL DROP TABLE clause do?**  
    Removes table and data.  
    ```sql
    DROP TABLE table_name;
    ```

88. **What is the difference between DROP and TRUNCATE?**  
    DROP removes table structure; TRUNCATE removes data only.

89. **How do you add a 'order_date' column to a table called 'order'?**  
    ```sql
    ALTER TABLE `order` ADD order_date DATE;
    ```

90. **What the correct syntax to rename column 'Address' to 'Addr' in 'Customer' table?**  
    ```sql
    ALTER TABLE Customer CHANGE Address Addr VARCHAR(50);
    ```

91. **Consider the following schema ADDRESSES (id, street_name, number, city, state) Which code snippet will alter the table ADDRESSES and delete the column named CITY?**  
    ```sql
    ALTER TABLE addresses DROP COLUMN city;
    ```

## Section 6: Indexes, Privileges, and Security

### Theory
Indexes speed queries like a book index. Clustered (reorders table), non-clustered (separate). Privileges: GRANT/REVOKE for access. SQL Injection: Malicious input exploiting queries.

**Best Practices:**
- Index frequently queried columns, but not all—updates slow them.
- Use prepared statements to prevent injection.
- Least privilege principle for users.

### Examples
Index:
```sql
CREATE INDEX idx_name ON customers (name);
```

GRANT:
```sql
GRANT SELECT ON database.* TO 'user'@'localhost';
```

### Q&A Bank (Questions 92-96, 115)
92. **What are Indexes in SQL?**  
    Speed retrieval. Duplicate allowed unless UNIQUE.  
    *Best Practice:* Update sparingly on insert-heavy tables.

93. **What is the difference between clustered and non-clustered indexes? Which of the following statements are true?**  
    Clustered: One per table, reorders data. Non-clustered: Multiple, separate structure. Clustered faster for reads; both true statements apply.

94. **The statement for assigning access privileges is**  
    GRANT/REVOKE.

95. **How many types of Privileges are available in SQL?**  
    System (e.g., CREATE TABLE), Object (e.g., SELECT on specific table).

96. **List the various privileges that a user can grant to another user?**  
    SELECT, INSERT, UPDATE, DELETE, EXECUTE, etc.

97. **What is SQL Injection?**  
    Code injection via input. Prevent with parameterized queries.  
    *Example Vulnerability:*  
    ```sql
    -- Bad: SELECT * FROM users WHERE id = '$input';  -- Input: ' OR '1'='1
    ```  
    *Safe:* Use placeholders.

## Section 7: Transactions and Concurrency

### Theory
Transactions ensure ACID: Atomicity (all or nothing), Consistency (valid states), Isolation (concurrent independence), Durability (persists after commit). Controls: COMMIT, ROLLBACK, SAVEPOINT. Locking prevents conflicts. Isolation levels: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ (MySQL default), SERIALIZABLE.

**Best Practices:**
- Keep transactions short to reduce locking.
- Use explicit BEGIN TRANSACTION in multi-statement ops.
- Handle deadlocks with retries.

### Diagrams
ACID Properties (Text):
- Atomicity: Commit or Rollback entire tx.
- Isolation: Tx1 | Tx2 (no interference).

### Examples
Transaction:
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### Q&A Bank (Questions 97-104)
97. **What does the term 'locking' refer to?**  
    Prevents concurrent changes/reads on data.

98. **What are a transaction's main controls?**  
    COMMIT (save), ROLLBACK (undo), SAVEPOINT (partial rollback).  
    *Example:*  
    ```sql
    SAVEPOINT sp1;
    -- Operations
    ROLLBACK TO sp1;
    ```

99. **A transaction completes its execution is said to be**  
    Committed.

100. **Consider the following code: START TRANSACTION /transaction body/ COMMIT; ROLLBACK; What does Rollback do?**  
     Nothing—post-COMMIT changes are permanent.

101. **What are valid properties of the transaction?**  
     ACID.

102. **What happens if autocommit is enabled?**  
     Each statement auto-commits (default in MySQL).

103. **What is the default isolation level used in MySQL?**  
     REPEATABLE READ (prevents non-repeatable reads).

104. **In MySQL autocommit is enabled by default for each session.**  
     True.

## Section 8: Views, Stored Procedures, Triggers, and Advanced Topics

### Theory
Views: Virtual tables from queries. Updatable if simple. Cursors: Row-by-row processing in procedures. Triggers: Auto-execute on events (INSERT/UPDATE/DELETE). Optimization: Efficient plans via indexes, stats.

**Best Practices:**
- Use views for security (limit columns).
- Materialized views for performance (if supported).
- Triggers for audits, but avoid complex logic.

### Examples
View:
```sql
CREATE VIEW active_customers AS SELECT * FROM customers WHERE status = 'active';
```

Trigger:
```sql
CREATE TRIGGER after_insert AFTER INSERT ON orders FOR EACH ROW 
INSERT INTO audit_log VALUES (NEW.id, 'Inserted');
```

### Q&A Bank (Questions 105-114)
105. **Which of these is also known as a virtual table in MySQL?**  
     View.

106. **Are views updatable using INSERT, DELETE or UPDATE?**  
     Some are (simple, no aggregates/DISTINCT/GROUP BY). Conditions: One base table, includes PK, no subqueries.

107. **What are the advantages of Views?**  
     Simplify queries, limit access, hide complexity. Changes commit only after base table ops.

108. **Does a View contain data?**  
     No (normal view: query only). Yes for materialized (stored data, needs refresh).

109. **What SQL statement do you have to use to remove a view?**  
     ```sql
     DROP VIEW view_name;
     ```

110. **Can a View based on another View?**  
     Yes.

111. **Inside a stored procedure you to iterate over a set of rows returned by a query using a**  
     CURSOR. Steps: DECLARE, OPEN, FETCH, CLOSE, DEALLOCATE.

112. **How do you call the process of finding a good strategy for processing a query?**  
     Query optimization (considers plans, stats).

113. **What is a trigger? or There are triggers for… or A trigger is applied to**  
     Stored procedure auto-executing on DML/DDL events (INSERT/UPDATE/DELETE/CREATE/etc.). Components: Event, Action.  
     *Example above.*

114. **A special kind of a stored procedure that executes in response to certain action on the table like insertion, deletion or updation of data is called**  
     Trigger.

---

Resources

- www.wikipedia.org
- www.w3schools.com
- www.freefeast.info

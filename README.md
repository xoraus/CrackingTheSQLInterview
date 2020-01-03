
# **Cracking the SQL Interview**
## A comprehensive guide before your next interview
  


**1. SQL was developed as an integral part of**

SQL - Structured Query Language is a domain-specific language used in programming and designed for managing data held in a relational database management system (RDBMS), or for stream processing in a relational data stream management system (RDSMS).

Although SQL is an ANSI (American National Standards Institute) standard, there are different versions of the SQL language.

However, to be compliant with the ANSI standard, they all support at least the major commands (such as SELECT, UPDATE, DELETE, INSERT, WHERE) in a similar manner.

Note: Most of the SQL database programs also have their own proprietary extensions in addition to the SQL standard!

What Can SQL do?

-   SQL can execute queries against a database
-   SQL can retrieve data from a database
-   SQL can insert records in a database
-   SQL can update records in a database
-   SQL can delete records from a database
-   SQL can create new databases
-   SQL can create new tables in a database
-   SQL can create stored procedures in a database
-   SQL can create views in a database
-   SQL can set permissions on tables, procedures, and views

  

  

  

  

**2. What does SQL stand for?**

SQL stands for Structured Query Language.

SQL lets you access and manipulate databases.

SQL is an ANSI (American National Standards Institute) standard.

  

**3. SQL is (referring to it as a Programming Language)**

**SQL is a declarative language in which the expected result or operation is given without the specific details about how to accomplish the task.** The steps required to execute SQL statements are handled transparently by the SQL database. Sometimes **SQL is characterized as non-procedural** because procedural languages generally require the details of the operations to be specified, such as opening and closing tables, loading and searching indexes, or flushing buffers and writing data to filesystems. Therefore, SQL is considered to be designed at a higher conceptual level of operation than procedural languages because the lower level logical and physical operations aren't specified and are determined by the SQL engine or server process that executes it.

  

**4. Which of the following is NOT a SQL command? (SELECT, REMOVE, UPDATE, INSERT)**

REMOVE is not a valid SQL command.  

Some of The Most Important SQL Commands

SELECT - extracts data from a database

UPDATE - updates data in a database

DELETE - deletes data from a database

INSERT INTO - inserts new data into a database

CREATE DATABASE - creates a new database

ALTER DATABASE - modifies a database

CREATE TABLE - creates a new table

ALTER TABLE - modifies a table

DROP TABLE - deletes a table

CREATE INDEX - creates an index (search key)

DROP INDEX - deletes an index

  

  

  

**5. What is MySQL?**

MySQL is the most popular Open Source SQL database management system developed, distributed, and supported by Oracle Corporation.

Another common SQL interview question regarding MySQL may come in a different form: “**What is the difference between SQL and MySQL?**”  
  
**Difference between SQL and MySQL:**

SQL is a structured query language that is used for manipulating and accessing the relational database, on the other hand, MySQL itself is a relational database that uses SQL as the standard database language.

  

  

**6. What are some properties of PL/SQL?**

PL/SQL is a combination of SQL along with the procedural features of programming languages. It was developed by Oracle Corporation in the early 90's to enhance the capabilities of SQL. PL/SQL is one of three key programming languages embedded in the Oracle Database, along with SQL itself and Java.

Another common SQL interview question regarding PL/SQL may come in a different form:

“What is the difference between SQL and PL/SQL?”  
Difference between SQL and PL/SQL:

SQL is a Structured Query Language used to issue a single query or execute a single insert/update/delete.

PL-SQL is a programming language SQL, used to write full programs using variables, loops,operators etc. to carry out multiple selects/inserts/updates/deletes.

SQL may be considered as the source of data for our reports, web pages and screens.

PL/SQL can be considered as the application language similar to Java or PHP. It might be the language used to build, format and display those reports, web pages and screens.

SQL is a data oriented language used to select and manipulate sets of data.

PL/SQL is a procedural language used to create applications.

SQL vs. PL-SQL

SQL is used to write queries, DDL and DML statements.

PL/SQL is used to write program blocks, functions, procedures triggers,and packages.

SQL is executed one statement at a time.

PL/SQL is executed as a block of code.

SQL is declarative, i.e., it tells the database what to do but not how to do it.

Whereas, PL/SQL is procedural, i.e., it tells the database how to do things.

SQL can be embedded within a PL/SQL program.

But PL/SQL can’t be embedded within a SQL statement.

**7. What are the possible values for the BOOLEAN data field in MySQL?**

MySQL uses TINYINT(1) data type to represent boolean values. A value of zero is considered false . Non-zero values are considered true .

  

**8. What data type would you choose if you wanted to store the distance (rounded to the nearest mile)?**

INTEGER (or INT )  

**9. Which are valid SQL keywords (statements & clauses)**

SELECT - extracts data from a database

FROM - clause is used to specify the tables to extract data from

WHERE - clause is used to extract only those records that fulfill a specified condition.

GROUP BY - is often used with aggregate functions (COUNT , MAX , MIN , SUM , AVG ) to group the result-set by one or more columns.

HAVING - clause was added to SQL because the WHERE keyword could not be used with aggregate functions.

ORDER BY - keyword is used to sort the result-set in ascending or descending order.

UPDATE - updates data in a database

DELETE - deletes data from a database

INSERT INTO - inserts new data into a database

CREATE DATABASE - creates a new database

ALTER DATABASE - modifies a database

CREATE TABLE - creates a new table

ALTER TABLE - modifies a table

DROP TABLE - deletes a table

CREATE INDEX - creates an index (search key)

DROP INDEX - deletes an index

  

  

  

  

  

**10. Which of the following are valid SQL comments?**

Comments are used to explain sections of SQL statements, or to prevent execution of SQL statements.

Single line comments start with -- .

Any text between -- and the end of the line will be ignored (will not be executed).

The following example uses a single-line comment as an explanation:
```
-   --Select all:
-   SELECT * FROM Customers;
```	
Multi-line comments start with /* and end with */ .

Any text between /* and */ will be ignored.

The following example uses a multi-line comment as an explanation:
```
-   /*Select all the columns
-   of all the records
-   in the Customers table:*/
-   SELECT * FROM Customers;
```
The following example uses a multi-line comment to ignore many statements:
```
-   /*SELECT * FROM Customers;
-   SELECT * FROM Products;*/
-   SELECT * FROM Suppliers;
```

**11. Which SQL statement is used to extract data from a database?**

A SELECT statement retrieves zero or more rows from one or more database tables or database views.

As SQL is a declarative programming language, SELECT queries specify a result set, but do not specify how to calculate it.

The SELECT statement has many optional clauses:

WHERE specifies which rows to retrieve.

GROUP BY groups rows sharing a property so that an aggregate function can be applied to each group.

HAVING selects among the groups defined by the GROUP BY clause.

ORDER BY specifies an order in which to return the rows.

AS provides an alias which can be used to temporarily rename tables or columns.

  

  

**12. How to select all records from the table 'Products'?**

SELECT * FROM Products;

If you want to select all the fields available in the table, use the * syntax as this:

SELECT * FROM Products;

  

  

**13. Can we rename a column in the output of SQL query?**

Yes, using AS .

SQL aliases are used to give a column in a table, a temporary name.

Aliases are often used to make column names more readable.

An alias only exists for the duration of the query.

Alias Column Syntax:

-   SELECT column_name AS alias_name
-   FROM table_name;

  

**14. With SQL, how do you select a column named "FirstName" from a table named "Customers"?**

SELECT FirstName FROM Customers;

The SELECT statement is used to select data from a database.

The data returned is stored in a result table, called the result-set.

**SELECT Syntax**
```
-   SELECT column1, column2, ...
-   FROM table_name;
```
Here, column1, column2, ... are the field names of the table you want to select data from. If you want to select all the fields available in the table, use the following syntax:

SELECT * FROM table_name;

  

  

**15. What does the SQL FROM clause do?**

The SQL FROM clause is used to list the tables and any joins required for the SQL statement.

**16. Which SQL statement is used to return only different values?**

The SELECT DISTINCT statement is used to return only distinct (different) values.

Inside a table, a column often contains many duplicate values; and sometimes you only want to list the different (distinct) values.

**SELECT DISTINCT Syntax**  
```
-   SELECT DISTINCT column1, column2, ...
-   FROM table_name;
```
  

**17. Consider the following schema ADDRESSES (id, street_name, number, city, state) Which of the following query would display the distinct cities in the ADDRESSES table?**

SELECT DISTINCT city FROM addresses;

(same theory applies as for the previous question)

**18. With SQL, how do you select all the records from a table named "Customers" where the value of the column "FirstName" is "John"?**

SELECT * FROM Customers WHERE FirstName='John';

The WHERE clause is used to filter records.

The WHERE clause is used to extract only those records that fulfill a specified condition.

SQL requires single quotes around text values (most database systems will also allow double quotes).

  

**19. The OR operator displays a record if ANY conditions listed are true. The AND operator displays a record if ALL of the conditions listed are true.**

The WHERE clause can be combined with AND , OR , and NOT operators.

The AND and OR operators are used to filter records based on more than one condition:

The AND operator displays a record if all the conditions separated by AND are TRUE .

The OR operator displays a record if any of the conditions separated by OR are TRUE .

The NOT operator displays a record if the condition(s) is NOT TRUE .

**AND Syntax**
```
-   SELECT column1, column2, ...
-   FROM table_name
-   WHERE condition1 AND condition2 AND condition3 …;
```
**OR Syntax**
```
-   SELECT column1, column2, ...
-   FROM table_name
-   WHERE condition1 OR condition2 OR condition3 ...;
```
**NOT Syntax**
```
-   SELECT column1, column2, ...
-   FROM table_name
-   WHERE NOT condition;
```
  

  

  

**20. Which of the following SQL statements has correct syntax?**

SELECT * FROM Table1 WHERE Column1 >= 100

SQL Comparison Operators

= Equal to

> Greater than

< Less than

>= Greater than or equal to

<= Less than or equal to

<> Not equal to

**21. With SQL, how do you select all the records from a table named "Customers" where the "FirstName" is "John" and the "LastName" is "Jackson"?**
```
SELECT * FROM Customers WHERE FirstName='John' AND LastName='Jackson'
```
Same answers as for the previous 2 questions.

You must use the AND operator that displays a record if all the conditions separated by AND are TRUE and the = (‘equal’) comparison operator.

  

  

  

  

**22. How to select random 10 rows from a table?**

The easiest way to generate random rows in MySQL is to use the ORDER BY RAND() clause.
```
SELECT * FROM tbl ORDER BY RAND() LIMIT 10;
```
This can work fine for small tables. However, for big table, it will have a serious performance problem as in order to generate the list of random rows, MySQL need to assign random number to each row and then sort them.

Even if you want only 10 random rows from a set of 100k rows, MySQL need to sort all the 100k rows and then, extract only 10 of them.

**23. Examine the following code. What will the value of price be if the statement finds a NULL value? SELECT name, ISNULL(price, 50) FROM PRODUCTS**

What is a NULL Value?

A field with a NULL value is a field with no value.

If a field in a table is optional, it is possible to insert a new record or update a record without adding a value to this field. Then, the field will be saved with a NULL value.

Note: It is very important to understand that a NULL value is different from a zero value or a field that contains spaces. A field with a NULL value is one that has been left blank during record creation!

  

  

  

  

  

  

**How can you return a default value for a NULL?**

**MySQL**

The MySQL IFNULL() function lets you return an alternative value if an expression is NULL:
```
-   SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
-   FROM Products
```
or we can use the COALESCE() function, like this:
```
-   SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
-   FROM Products
```
**SQL Server**

The **SQL Server** ISNULL() function lets you return an alternative value when an expression is NULL :

-   SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))
-   FROM Products

**MS Access**

The MS Access IsNull() function returns TRUE (-1) if the expression is a null value, otherwise FALSE (0) :

-   SELECT ProductName, UnitPrice * (UnitsInStock + IIF(IsNull(UnitsOnOrder), 0, UnitsOnOrder))
-   FROM Products

**Oracle**

The Oracle NVL() function achieves the same result:

-   SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))
-   FROM Products  
    

**24. Which operator is used to search for a specified text pattern in a column?**

The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

There are two wildcards used in conjunction with the LIKE operator:

% - The percent sign represents zero, one, or multiple characters

_ - The underscore represents a single character

Examples:

-   WHERE CustomerName LIKE 'a%' -- Finds any values that starts with  "a"
-   WHERE CustomerName LIKE '%a' -- Finds any values that ends with  "a"
-   WHERE CustomerName LIKE '%or%' -- Finds any values that have "or"  in any position
-   WHERE CustomerName LIKE '_r%' -- Finds any values that have "r"  in the second position
-   WHERE CustomerName LIKE 'a_%_%' -- Finds any values that starts with  "a"  and are at least 3 characters in length
-   WHERE ContactName LIKE 'a%o' -- Finds any values that starts with  "a"  and ends with  "o"

**25. How to write a query to show the details of a student from Students table whose FirstName starts with 'K'?**

SELECT * FROM Students WHERE FirstName LIKE 'K%'.

Explanation from previous question applies.

  

**26. Which operator is used to select values within a range?**

The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates.

The BETWEEN operator is inclusive: begin and end values are included.

**BETWEEN Syntax**
```
-   SELECT column_name(s)
-   FROM table_name
-   WHERE column_name BETWEEN value1 AND value2;
```
**27. Which of the following SQL statements is correct?**

SELECT * FROM Sales WHERE Date BETWEEN '01/12/2017' AND '01/01/2018'  

Explanation from previous question applies.

**28. With SQL, how do you select all the records from a table named "Customers" where the "LastName" is alphabetically between (and including) "Brooks" and "Gray"?**
```
SELECT * FROM Customers WHERE LastName BETWEEN 'Brooks' AND 'Gray'  
```
Explanation from previous question applies.

  

  

  

  

  

**29. The 'IN' SQL keyword…**

The IN operator allows you to specify multiple values in a WHERE clause.

The IN operator is a shorthand for multiple OR conditions.

**IN Syntax**
```
-   SELECT column_name(s)
-   FROM table_name
-   WHERE column_name IN (value1, value2, ...);
```
or:
```
-   SELECT column_name(s)
-   FROM table_name
-   WHERE column_name IN (SELECT STATEMENT); --subquery
```
**30. What does UPPER function do?**

The UPPER() function converts a string to upper-case.

**31. What function to use to round a number to the smallest integer value that is greater than or equal to a number?**

The CEILING() function returns the smallest integer value that is greater than or equal to the specified number.

The CEIL() function is a synonym for the CEILING() function and also returns the smallest integer value that is greater than or equal to a number.

Example:

SELECT CEILING(25.50); -- returns 26

  

  

**32. How to get current date in MySQL (without time)?**

The CURDATE() function returns the current date. This function returns the current date as a YYYY-MM-DD format if used in a string context, and as a YYYYMMDD format if used in a numeric context.

The CURRENT_DATE() function is a synonym for the CURDATE() function.

**33. Which SQL keyword is used to retrieve a maximum value?**

The MAX() function returns the largest value of the selected column.

**MAX() Syntax**
```
-   SELECT MAX(column_name)
-   FROM table_name
-   WHERE condition;
```
**34. Which SQL functions is used to count the number of results?**

The COUNT() function returns the number of rows that matches a specified criteria.

**COUNT() Syntax**
```
-   SELECT COUNT(column_name)
-   FROM table_name
-   WHERE condition;
```
  

  

  

**35. Which of the following are Aggregate Functions?**

SQL Aggregate functions are:

**COUNT** counts how many rows are in a particular column.

**SUM** adds together all the values in a particular column.

**MIN** and **MAX** return the lowest and highest values in a particular column, respectively.

**AVG** calculates the average of a group of selected values.

**36. With SQL, how can you return the number of records in the "Customers" table?**

**SELECT COUNT(*) FROM Customers**

Same answer as for the previous question.

**37. Which 2 SQL keywords specify the sorting direction of the result set retrieved with ORDER BY clause?**

**ASC | DESC**

The ORDER BY keyword is used to sort the result-set in ascending or descending order.

**ORDER BY Syntax**
```
-   SELECT column1, column2, ...
-   FROM table_name
-   ORDER BY column1, column2, ... ASC|DESC;
```
  

**38. If you don't specify ASC or DESC for an ORDER BY clause, the following is used by default:**

The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.

**39. Suppose a Students table has two columns, name and mark. How to get name and mark of top three students?**

SELECT name, mark FROM Students ORDER BY mark DESC LIMIT 3;  

You have to use ORDER BY to order students by their marks and then select just the first 3 records.

The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.

**The SQL SELECT TOP Clause**

The **SELECT TOP** clause is used to specify the number of records to return.

The SELECT TOP clause is useful on large tables with thousands of records. Returning a large number of records can impact on performance.

Not all database systems support the SELECT TOP clause.**MySQL supports the** LIMIT clause to select a limited number of records, while **Oracle uses** ROWNUM .

**40. With SQL, how can you return all the records from a table named "Customers" sorted descending by "FirstName"?**
```
_SELECT * FROM Customers ORDER BY FirstName DESC;_
```
Same answers as for the previous 2 questions apply.

  

  

**41. Which of the following SQL statements is correct?**

_SELECT name, COUNT(name) FROM customers GROUP BY name_

SQL aggregate functions like COUNT , AVG , and SUM have something in common: they all aggregate across the entire table. But what if you want to aggregate only part of a table? For example, you might want to count the customers having the same name. In situations like this, you’d need to use the GROUP BY clause. GROUP BY allows you to separate data into groups, which can be aggregated independently of one another.

**42. What is the difference between HAVING clause and WHERE clause?**

Both specify a search condition but HAVING clause is used only with the SELECT statement and typically used with GROUP BY clause.

If GROUP BY clause is not used then HAVING behaves like WHERE clause only.

Here are some other differences:

HAVING filters records that work on summarized GROUP BY results.

HAVING applies to summarized group records, whereas WHERE applies to individual records.

Only the groups that meet the HAVING criteria will be returned.

HAVING requires that a GROUP BY clause is present.

WHERE and HAVING can be in the same query.

  

**43. What is JOIN used for?**

A JOIN clause is used to combine rows from two or more tables, based on a related column between them.

**44. What is the most common type of join?**

The most common type of join used in day to day queries is INNER JOIN .

**45. What are different JOINS used in SQL?**

There are several types of joins:

**SQL INNER JOIN Keyword**

The INNER JOIN keyword selects records that have matching values in both tables.

**SQL LEFT JOIN Keyword**

The LEFT JOIN keyword returns all records from the left table (table1), and the matched records from the right table (table2). The result is NULL from the right side, if there is no match.

**SQL RIGHT JOIN Keyword**

The RIGHT JOIN keyword returns all records from the right table (table2), and the matched records from the left table (table1). The result is NULL from the left side, when there is no match.

**SQL FULL OUTER JOIN Keyword**

The FULL OUTER JOIN keyword return all records when there is a match in either left (table1) or right (table2) table records.

Note: FULL OUTER JOIN can potentially return very large result-sets!

**SQL Self JOIN**

A self JOIN is a regular join, but the table is joined with itself.

**SQL CROSS JOIN**

The SQL CROSS JOIN produces a result set which is the number of rows in the first table multiplied by the number of rows in the second table if no WHERE clause is used along with CROSS JOIN .This kind of result is called as Cartesian Product.

If WHERE clause is used with CROSS JOIN , it functions like an INNER JOIN .

**46. Which of the following is NOT TRUE about the ON clause?**

ON clause is used to specify conditions or specify columns to JOIN . ON clause makes the query easy to understand. ON clause allows 3 way (or more) joins.

**47. Assume that Table A is joined to Table B. An inner join:**

**Displays rows (records) only when the values of the Key in table A and the foreign key in table B are equal.**

The INNER JOIN keyword selects records that have matching values in both tables.

**48. Can you join 3 tables together with inner join:**

Yes. You can join multiple tables with inner join.

For example, for a Faculty table the lookup tables might be Division, with DivisionID as the PK, Country, with CountryID as the PK, and Nationality, with NationalityID as the PK. To join Faculty to the Division, Country, and Nationality tables, the fields DivisionID, CountryID and NationalityID would need to be foreign keys in the Faculty table.  

The SQL to join them would then be:
```
-   SELECT <fieldlist> FROM Faculty AS f
-   INNER JOIN Division AS d ON d.FacultyID = f.FacultyID
-   INNER JOIN Country AS c ON c.FacultyID = f.FacultyID
-   INNER JOIN Nationality AS n ON n.FacultyID = f.FacultyID
```
  

  

  

  

**49. Can you join a table to itself?**

Yes. The operation is called self join.

**Self JOIN Syntax**
```
-   SELECT column_name(s)
-   FROM table1 T1, table1 T2
-   WHERE condition;
```
**50. Which of the following is true about Cartesian Products?**

**A Cartesian product is formed when a join condition is omitted.**

The SQL CROSS JOIN produces a result set which is the number of rows in the first table multiplied by the number of rows in the second table if no WHERE clause is used along with CROSS JOIN .This kind of result is called as Cartesian Product.

If WHERE clause is used with CROSS JOIN , it functions like an INNER JOIN .

**CROSS JOIN Syntax**  
```
-   SELECT *
-   FROM table1
-   CROSS JOIN table2;
```
  

  

  

  

**51. In relational algebra the INTERSECTION of two sets (set A and Set B) corresponds to**

**A AND B**

The SQL INTERSECT clause/operator is used to combine two SELECT statements, but returns rows only from the first SELECT statement that are identical to a row in the second SELECT statement. This means INTERSECT returns only common rows returned by the two SELECT statements.

**INTERSECT Syntax**
```
-   SELECT column1 [, column2 ]
-   FROM table1 [, table2 ]
-   [WHERE condition]
-   INTERSECT
-   SELECT column1 [, column2 ]
-   FROM table1 [, table2 ]
-   [WHERE condition]
```
  

  

  

  

  

  

  

  

**52. In relational algebra the UNION of two sets (set A and Set B) corresponds to**

**A OR B**

The SQL UNION clause/operator is used to combine the results of two or more SELECT statements without returning any duplicate rows.

To use this UNION clause, each SELECT statement must have

The same number of columns selected

The same number of column expressions

The same data type and

Have them in the same order

But they need not have to be in the same length.

**Union Syntax**
```
-   SELECT column1 [, column2 ]
-   FROM table1 [, table2 ]
-   [WHERE condition]
-   UNION
-   SELECT column1 [, column2 ]
-   FROM table1 [, table2 ]
-   [WHERE condition]
```
  

**53. What is the difference between UNION and UNION ALL?**

UNION – returns all distinct rows selected by either query

UNION ALL – returns all rows selected by either query, including all duplicates.

**54. Having a list of Customer Names that searched for product 'X' and a list of customer Names that bought the product 'X'. What set operator would you use to get only those who are interested but did not bought product 'X' yet?**

**MINUS**

The **SQL** MINUS operator is used to return all rows in the first SELECT statement that are not returned by the second SELECT statement. Each SELECT statement will define a dataset. The MINUS operator will retrieve all records from the first dataset and then remove from the results all records from the second dataset.

**MINUS Syntax**
```
-   SELECT expression1, expression2, ... expression_n
-   FROM tables
-   [WHERE conditions]
-   MINUS
-   SELECT expression1, expression2, ... expression_n
-   FROM tables
-   [WHERE conditions];
```
  

  

  

  

  

  

  

**55. One (or more) select statement whose return values are used in filtering conditions of the main query is called**

**Subquery.**

A subquery is a SQL query nested inside a main query.

A subquery may occur in :
```
-   A SELECT clause
-   A FROM clause
-   A WHERE clause
```
A subquery is usually added within the WHERE clause of another SQL SELECT statement.

You can use the comparison operators, such as > , < , or = . The comparison operator can also be a multiple-row operator, such as IN , ANY , or ALL .

A subquery is also called an inner query or inner select, while the statement containing a subquery is also called an outer query or outer select.

The inner query executes first before its parent query so that the results of an inner query can be passed to the outer query.

**56. Subqueries can be nested in...**

The subquery can be nested inside a SELECT , INSERT , UPDATE , or DELETE statement or inside another subquery.  

**57. What row comparison operators can be used with a subquery?**

You can use the comparison operators, such as > , < , or = . The comparison operator can also be a multiple-row operator, such as IN , ANY , or ALL .

**58. A subquery that is used inside a subquery is called a**

Subquery within another subquery is called as **Nested Subquery**.

  

**59. A subquery that uses a correlation name from the outer query is called a**

If the output of a subquery is depending on column values of the parent query table then the query is called **Correlated Subquery**.

**60. What is Case Function?**

The CASE function lets you evaluate conditions and return a value when the first condition is met (like an IF-THEN-ELSE statement).

**CASE Syntax**
```
-   CASE expression
-   WHEN condition1 THEN result1
-   WHEN condition2 THEN result2
-   ...
-   WHEN conditionN THEN resultN
-   ELSE result
-   END  
```

**61. What are different types of statements supported by SQL?**

**DDL** (Data Definition Language): It is used to define the database structure such as tables. It includes three statements such as Create, Alter, and Drop.

**DML** (Data Manipulation Language): These statements are used to manipulate the data in records. Commonly used DML statements are Select, Insert, Update, and Delete.

Note: Some people prefer to assign the SELECT statement to a category of its own called: DQL. Data Query Language.

**DCL** (Data Control Language): These statements are used to set privileges such as Grant and Revoke database access permission to the specific user.

  

  

**62. Which of the following SQL statements are DDL**

**DDL statements include:**

ALTER Statements

CREATE Statements

DROP Statements

TRUNCATE TABLE

**63. DML includes the following SQL statements**

**DML statements are:**
```
SELECT

INSERT

UPDATE

DELETE
```
  

**64. Grant and Revoke commands are under**

**DCL (Data Control Language)**

GRANT : Used to provide any user access privileges or other privileges for the database.

REVOKE : Used to take back permissions from any user.

  

  

**65. Which of the following is not a DML statement?**

Same answer as for the previous questions.

COMMIT is used to persist changes performed during a TRANSACTION.

**66. Which SQL statement is used to insert new data in a database?**

The INSERT INTO statement is used to insert new records in a table.

**67. When inserting data in a table do you have to specify the list of columns you are inserting values for?**

**INSERT INTO Syntax**

It is possible to write the INSERT INTO statement in two ways.

The first way specifies both the column names and the values to be inserted:
```
-   INSERT INTO table_name (column1, column2, column3, ...)
-   VALUES (value1, value2, value3, ...);
```
If you are adding values for all the columns of the table, you do not need to specify the column names in the SQL query. However, make sure the order of the values is in the same order as the columns in the table. The INSERT INTO syntax would be as follows:
```
-   INSERT INTO table_name
-   VALUES (value1, value2, value3, ...);
```
**68. With SQL, how can you insert a new record into the "Customers" table?**

Same answer as for the previous question.

**69. With SQL, how can you insert "Hawkins" as the "LastName" in the "Customers" table?**

Same answer as for the previous question.

  

**70. How do you create a temporary table in MySQL?**

To create a temporary table, you just need to add the TEMPORARY keyword to the CREATE TABLE statement.

Example:
```
-   CREATE TEMPORARY TABLE top10customers
-   SELECT customer.fname, customer.lname
-   FROM customers
```
-   /* all the conditions to fecth the top 10 customers */

**71. Which SQL statement is used to update data in a database?**

The UPDATE statement is used to modify the existing records in a table.

**UPDATE Syntax**
```
-   UPDATE table_name
-   SET column1 = value1, column2 = value2, ...
-   WHERE condition;
```
**72. What is the keyword is used in an UPDATE query to modify the existing value?**

The answer is SET .

**UPDATE Syntax**
```
-   UPDATE table_name
-   SET column1 = value1, column2 = value2, ...
-   WHERE condition;
```
**73. How can you change "Jackson" into "Hawkins" in the "LastName" column in the Customer table?**
```
UPDATE Customers SET LastName='Hawkins' WHERE LastName='Jackson'  
```
Same explanation as for the previous question.

**74. Which SQL statement is used to delete data from a database?**

The DELETE statement is used to delete existing records in a table.

**DELETE Syntax**
```
-   DELETE FROM table_name
-   WHERE condition;
```
  

**75. With SQL, how can you delete the records where the "FirstName" is "John" in the Customers Table?**

DELETE FROM Customers WHERE FirstName = 'John'  

**76. The FROM SQL keyword is used to**

Specify the table we are are selecting or deleting from.

**DELETE Syntax**
```
-   DELETE FROM table_name
-   WHERE condition;
```
**UPDATE Syntax**
```
-   UPDATE table_name
-   SET column1 = value1, column2 = value2, ...
-   WHERE condition;
```
**INSERT Syntax**
```
-   INSERT INTO table_name (column1, column2, column3, ...)
-   VALUES (value1, value2, value3, ...);
```
**SELECT Syntax**
```
-   SELECT column1, column2, ...
-   FROM table_name;
```
**77. What is the difference between DELETE and TRUNCATE?**

The basic difference in both is DELETE is DML command and TRUNCATE is DDL.

DELETE is used to delete a specific row from the table whereas TRUNCATE is used to remove all rows from the table

We can use DELETE with WHERE clause but cannot use TRUNCATE with it.

**78. Which SQL statement is used to create a table in a database?**

The CREATE TABLE statement is used to create a new table in a database.

**Syntax**
```
-   CREATE TABLE table_name (
-   column1 datatype,
-   column2 datatype,
-   column3 datatype,
-   ....
-   );
```
  

  

  

  

  

  

  

  

  

**79. What is Collation in SQL?**

A collation is a set of rules that defines how to compare and sort character strings.

**Detailed Explanation:**

A character set is a set of symbols and encodings. A collation is a set of rules for comparing characters in a character set. Let's make the distinction clear with an example of an imaginary character set.

Suppose that we have an alphabet with four letters: A, B, a, b. We give each letter a number: A = 0, B = 1, a = 2, b = 3. The letter A is a symbol, the number 0 is the encoding for A, and the combination of all four letters and their encodings is a character set.

Suppose that we want to compare two string values, A and B. The simplest way to do this is to look at the encodings: 0 for A and 1 for B. Because 0 is less than 1, we say A is less than B. What we've just done is apply a collation to our character set. The collation is a set of rules (only one rule in this case): “compare the encodings.” We call this simplest of all possible collations a binary collation.

But what if we want to say that the lowercase and uppercase letters are equivalent? Then we would have at least two rules: (1) treat the lowercase letters a and b as equivalent to A and B; (2) then compare the encodings. We call this a case-insensitive collation. It is a little more complex than a binary collation.

In real life, most character sets have many characters: not just A and B but whole alphabets, sometimes multiple alphabets or eastern writing systems with thousands of characters, along with many special symbols and punctuation marks. Also in real life, most collations have many rules, not just for whether to distinguish lettercase, but also for whether to distinguish accents (an “accent” is a mark attached to a character as in German Ö), and for multiple-character mappings (such as the rule that Ö = OE in one of the two German collations).

_Source: dev.myslq.com_

**80. What is true about an AUTO_INCREMENT column in SQL?**

AUTO_INCREMENT allows a unique number to be generated automatically when a new record is inserted into a table. Often this is the primary key field that we would like to be created automatically every time a new record is inserted.

**Syntax for MySQL**

The following SQL statement defines the "ID" column to be an auto-increment primary key field in the "Persons" table:
```
-   CREATE TABLE Persons (
-   ID int NOT NULL AUTO_INCREMENT,
-   LastName varchar(255) NOT NULL,
-   FirstName varchar(255),
-   Age int,
-   PRIMARY KEY (ID)
-   );
```
**Syntax for SQL Server**

The following SQL statement defines the "ID" column to be an auto-increment primary key field in the "Persons" table:
```
-   CREATE TABLE Persons (
-   ID int IDENTITY(1,1) PRIMARY KEY,
-   LastName varchar(255) NOT NULL,
-   FirstName varchar(255),
-   Age int
-   );
```
**Syntax for Oracle**

In Oracle the code is a little bit more tricky.

You will have to create an auto-increment field with the sequence object (this object generates a number sequence).

Use the following **CREATE SEQUENCE syntax:**
```
-   CREATE SEQUENCE seq_person
-   MINVALUE 1
-   START WITH 1
-   INCREMENT BY 1
-   CACHE 10;
```
The code above creates a sequence object called seq_person, that starts with 1 and will increment by 1. It will also cache up to 10 values for performance. The cache option specifies how many sequence values will be stored in memory for faster access.

To insert a new record into the "Persons" table, we will have to use the nextval function (this function retrieves the next value from seq_person sequence):
```
-   INSERT INTO Persons (ID,FirstName,LastName)
-   VALUES (seq_person.nextval,'Lars','Monsen');
```
The SQL statement above would insert a new record into the "Persons" table. The "ID" column would be assigned the next number from the seq_person sequence. The "FirstName" column would be set to "Lars" and the "LastName" column would be set to "Monsen".

**81. What are valid constraints in MySQL?**

SQL constraints are used to specify rules for the data in a table.

Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

Constraints can be column level or table level. Column level constraints apply to a column, and table level constraints apply to the whole table.

The following constraints are commonly used in SQL:

NOT NULL - Ensures that a column cannot have a NULL value

UNIQUE - Ensures that all values in a column are different

PRIMARY KEY - A combination of a NOT NULL and UNIQUE . Uniquely identifies each row in a table

FOREIGN KEY - Uniquely identifies a row/record in another table

CHECK - Ensures that all values in a column satisfies a specific condition

DEFAULT - Sets a default value for a column when no value is specified

INDEX - Used to create and retrieve data from the database very quickly

  

**82. Which of the following is NOT TRUE about constraints?**

NOT NULL - Ensures that a column cannot have a NULL value

UNIQUE - Ensures that all values in a column are different

PRIMARY KEY - A combination of a NOT NULL and UNIQUE . Uniquely identifies each row in a table

FOREIGN KEY - Uniquely identifies a row/record in another table

  

**83. The NOT NULL constraint enforces a column to not accept null values.**

NOT NULL - Ensures that a column cannot have a NULL value.

  

**84. An unique (non-key) field**

The UNIQUE constraint ensures that all values in a column are different.

  

  

  

  

  

**85. What is CHECK Constraint?**

The CHECK constraint is used to limit the value range that can be placed in a column.

If you define a CHECK constraint on a single column it allows only certain values for this column.

If you define a CHECK constraint on a table it can limit the values in certain columns based on values in other columns in the row.

**SQL CHECK on CREATE TABLE**

The following SQL creates a CHECK constraint on the "Age" column when the "Persons" table is created. The CHECK constraint ensures that you can not have any person below 18 years:

**MySQL:**
```
-   CREATE TABLE Persons (
-   ID int NOT NULL,
-   LastName varchar(255) NOT NULL,
-   FirstName varchar(255),
-   Age int,
-   CHECK (Age>=18)
-   );
```
**SQL Server / Oracle / MS Access:**

-   CREATE TABLE Persons (
-   ID int NOT NULL,
-   LastName varchar(255) NOT NULL,
-   FirstName varchar(255),
-   Age int CHECK (Age>=18)
-   );

  

**86. What is the difference between UNIQUE and PRIMARY KEY constraints?**

UNIQUE vs PRIMARY KEY

Both the UNIQUE and PRIMARY KEY constraints provide a guarantee for uniqueness for a column or set of columns.

A PRIMARY KEY constraint automatically has a UNIQUE constraint.

However, you can have many UNIQUE constraints per table, but only one PRIMARY KEY constraint per table.

  

**87. What does SQL DROP TABLE clause do?**

The DROP TABLE statement is used to drop an existing table in a database.

**Syntax**
```
_DROP TABLE table_name;_
```
  

**88. What is the difference between DROP and TRUNCATE?**

TRUNCATE removes all rows from the table which cannot be retrieved back, DROP removes the entire table from the database and it cannot be retrieved back.

  

  

  

  

  

  

  

**89. How do you add a 'order_date' column to a table called 'order'?**

ALTER TABLE order ADD order_date DATE

The ALTER TABLE statement is used to add, delete, or modify columns in an existing table.

The ALTER TABLE statement is also used to add and drop various constraints on an existing table.

**ALTER TABLE - ADD Column**

To add a column in a table, use the following syntax:
```
-   ALTER TABLE table_name
-   ADD column_name datatype;
```
**90. What the correct syntax to rename column 'Address' to 'Addr' in 'Customer' table?**

ALTER TABLE Customer CHANGE Address Addr varchar(50);

ALTER TABLE - CHANGE

You rename a column using the ALTER TABLE and CHANGE commands together to change an existing column.

**Syntax**
```
-   ALTER TABLE table_name
-   CHANGE oldname newname datatype ;
```
  

  

  

  

**91. Consider the following schema ADDRESSES (id, street_name, number, city, state) Which code snippet will alter the table ADDRESSES and delete the column named CITY?**

ALTER TABLE addresses DROP COLUMN city;

ALTER TABLE - DROP COLUMN

To delete a column in a table, use the following syntax (notice that some database systems don't allow deleting a column):
```
-   ALTER TABLE table_name
-   DROP COLUMN column_name;
```
  

  

**92. What are Indexes in SQL?**

Indexes are used to retrieve data from the database very fast. The users cannot see the indexes, they are just used to speed up searches/queries.

Note: Updating a table with indexes takes more time than updating a table without (because the indexes also need an update). So, only create indexes on columns that will be frequently searched against.

**CREATE INDEX Syntax**

Creates an index on a table. Duplicate values are allowed:
```
-   CREATE INDEX index_name
-   ON table_name (column1, column2, ...);
```
  

  

  

**93. What is the difference between clustered and non-clustered indexes? Which of the following statements are true?**

One table can have only one clustered index but multiple nonclustered indexes.

Clustered indexes can be read rapidly rather than non-clustered indexes.

Clustered indexes store data physically in the table or view and non-clustered indexes do not store data in table as it has separate structure from data row.

**94. The statement for assigning access privileges is**

SQL GRANT and REVOKE commands are used to implement privileges in SQL multiple user environments. The administrator of the database can grant or revoke privileges to or from users of database object like SELECT , INSERT , UPDATE , DELETE , ALL etc.

GRANT Command: This command is used provide database access to user apart from an administrator.

**Syntax**
```
-   GRANT privilege_name
-   ON object_name
-   TO {user_name|PUBLIC|role_name}
-   [WITH GRANT OPTION];
```
In above syntax WITH GRANT OPTIONS indicates that the user can grant the access to another user too.

REVOKE Command: This command is used provide database deny or remove access to database objects.

**Syntax**
```
-   REVOKE privilege_name
-   ON object_name
-   FROM {user_name|PUBLIC|role_name};
```
  

  

**95. How many types of Privileges are available in SQL?**

There are two types of privileges used in SQL, such as

**System Privilege**: System privileges deal with an object of a particular type and specifies the right to perform one or more actions on it which include Admin allows a user to perform administrative tasks, ALTER ANY INDEX, ALTER ANY CACHE GROUP CREATE/ALTER/DELETE TABLE, CREATE/ALTER/DELETE VIEW etc.

**Object Privilege**: This allows to perform actions on an object or object of another user(s) viz. table, view, indexes etc. Some of the object privileges are EXECUTE, INSERT, UPDATE, DELETE, SELECT, FLUSH, LOAD, INDEX, REFERENCES etc.

**96. List the various privileges that a user can grant to another user?**

Same answers as for the previous question

**97. What does the term 'locking' refer to?**

Locking is a process preventing users from reading data being changed by other users, and prevents concurrent users from changing the same data at the same time.

  

  

  

  

  

  

  

  

  

  

  

  

**98. What are a transaction's main controls?**

COMMIT command is used to permanently save any transaction into the database.

When we use any DML command like INSERT , UPDATE or DELETE , the changes made by these commands are not permanent, until the current session is closed, the changes made by these commands can be rolled back.

To avoid that, we use the COMMIT command to mark the changes as permanent.

Following is commit command syntax:
```
_COMMIT;_
```
ROLLBACK command

This command restores the database to last committed state. It is also used with SAVEPOINT command to jump to a savepoint in an ongoing transaction.

If we have used the UPDATE command to make some changes into the database, and realise that those changes were not required, then we can use the ROLLBACK command to rollback those changes, if they were not committed using the COMMIT command.

Following is rollback command syntax:

_ROLLBACK TO savepoint_name;_

SAVEPOINT command

SAVEPOINT command is used to temporarily save a transaction so that you can rollback to that point whenever required.

  

  

  

Following is savepoint command syntax:

_SAVEPOINT savepoint_name;_

In short, using this command we can name the different states of our data in any table and then rollback to that state using the ROLLBACK command whenever required.

**99. A transaction completes its execution is said to be**

Committed**.**

**100. Consider the following code: START TRANSACTION /*transaction body*/ COMMIT; ROLLBACK; What does Rollback do?**

It does nothing. Once a transaction has executed commit, its effects can no longer be undone by rollback.

  

  

  

  

  

  

  

  

  

  

**101. What are valid properties of the transaction?**

The characteristics of these four properties as defined by Reuter and Härder are as follows:

**Atomicity**

Atomicity requires that each transaction be "all or nothing": if one part of the transaction fails, then the entire transaction fails, and the database state is left unchanged. An atomic system must guarantee atomicity in each and every situation, including power failures, errors and crashes. To the outside world, a committed transaction appears (by its effects on the database) to be indivisible ("atomic"), and an aborted transaction does not happen.

**Consistency**

The consistency property ensures that any transaction will bring the database from one valid state to another. Any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof. This does not guarantee correctness of the transaction in all ways the application programmer might have wanted (that is the responsibility of application-level code), but merely that any programming errors cannot result in the violation of any defined rules.

**Isolation**

The isolation property ensures that the concurrent execution of transactions results in a system state that would be obtained if transactions were executed sequentially, i.e., one after the other. Providing isolation is the main goal of concurrency control. Depending on the concurrency control method (i.e., if it uses strict - as opposed to relaxed - serializability), the effects of an incomplete transaction might not even be visible to another transaction.

**Durability**

The durability property ensures that once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors. In a relational database, for instance, once a group of SQL statements execute, the results need to be stored permanently (even if the database crashes immediately thereafter). To defend against power loss, transactions (or their effects) must be recorded in a non-volatile memory.

  

**102. What happens if autocommit is enabled?**

If autocommit mode is enabled, each SQL statement forms a single transaction on its own. By default, most of DBMS start the session for each new connection with autocommit enabled, so they do a commit after each SQL statement if that statement did not return an error. If a statement returns an error, the commit or rollback behavior depends on the error.

**103. What is the default isolation level used in MySQL?**

**REPEATABLE READ**

**104. In MySQL autocommit is enabled by default for each session.**

**TRUE**

**105. Which of these is also known as a virtual table in MySQL?**

**A view.**

In SQL, a view is a virtual table based on the result-set of an SQL statement.

A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database.

You can add SQL functions, WHERE , and JOIN statements to a view and present the data as if the data were coming from one single table.

**CREATE VIEW Syntax**
```
-   CREATE VIEW view_name AS
-   SELECT column1, column2, ...
-   FROM table_name
-   WHERE condition;
```
  

  

  

**106. Are views updatable using INSERT, DELETE or UPDATE?**

The SQL UPDATE VIEW command can be used to modify the data of a view.

All views are not updatable. So, UPDATE command is not applicable to all views. An updatable view is one which allows performing a UPDATE command on itself without affecting any other table.

When can a view be updated?

1. The view is defined based on one and only one table.

2. The view must include the PRIMARY KEY of the table based upon which the view has been created.

3. The view should not have any field made out of aggregate functions.

4. The view must not have any DISTINCT clause in its definition.

5. The view must not have any GROUP BY or HAVING clause in its definition.

6. The view must not have any SUBQUERIES in its definitions.

7. If the view you want to update is based upon another view, the later should be updatable.

8. Any of the selected output fields (of the view) must not use constants, strings or value expressions.

  

  

  

  

**107. What are the advantages of Views?**

Simplify queries: You can use database view to hide the complexity of underlying tables to the end-users and external applications

All changes performed by SQL statements are executed only after a COMMIT command.

A database view helps limit data access to specific users. You may not want a subset of sensitive data can be queryable by all users

**108. Does a View contain data?**

A view does not contain any data of its own, but is like a window through which data from other tables can be viewed and changed.

The answer depends on the type of view. In case of normal view, the answer is NO it only contains query based on a base table but in case of materialized view, YES it does contain data and for the updated data in the base table, it needs to be refreshed.

**109. What SQL statement do you have to use to remove a view?**

You can delete a view with the DROP VIEW command.

**SQL DROP VIEW Syntax**

_DROP VIEW view_name;_

  

**110. Can a View based on another View?**

Yes, A View is based on another View.

  

  

**111. Inside a stored procedure you to iterate over a set of rows returned by a query using a**

A CURSOR is a database object which is used to manipulate data in a row-to-row manner.

Cursor follows steps as given below:

-   Declare Cursor
-   Open Cursor
-   Retrieve row from the Cursor
-   Process the row
-   Close Cursor
-   Deallocate Cursor

  

**112. How do you call the process of finding a good strategy for processing a query?**

Query optimization is a function of many relational database management systems. The query optimizer attempts to determine the most efficient way to execute a given query by considering the possible query plans.

  

  

  

  

  

  

  

  

  

  

  

**113. What is a trigger?**

Triggers in SQL is kind of stored procedures used to create a response to a specific action performed on the table. You can invoke triggers explicitly on the table in the database.

Triggers are, in fact, written to be executed in response to any of the following events:

A database manipulation (DML) statement (DELETE , INSERT , or UPDATE )

A database definition (DDL) statement (CREATE , ALTER , or DROP ).

A database operation (SERVERERROR , LOGON , LOGOFF , STARTUP , or SHUTDOWN ).

Action and Event are two main components of SQL triggers when certain actions are performed the event occurs in response to that action.

**Syntax**
```
-   CREATE TRIGGER name {BEFORE|AFTER} (event [OR..]}
-   ON table_name [FOR [EACH] {ROW|STATEMENT}]
-   EXECUTE PROCEDURE functionname {arguments}
```
**114. There are triggers for…**

Same answer as for the previous question.

**115. A trigger is applied to**

Same answer as for the previous question.

  

  

**116. A special kind of a stored procedure that executes in response to certain action on the table like insertion, deletion or updation of data is called**

**Trigger.**

Same answer as for the previous question.

**117. What is SQL Injection?**

SQL injection is a code injection technique that might destroy your database.

SQL injection is one of the most common web hacking techniques.

SQL injection is the placement of malicious code in SQL statements, via web page input.

  

  

  

  

  

  

  

  

  

**_Resources_**

[www.wikipedia.org](http://www.wikipedia.org/)

[www.w3schools.com](http://www.w3schools.com/)

[www.freefeast.info](http://www.freefeast.info/)

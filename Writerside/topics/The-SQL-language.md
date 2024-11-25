# The SQL language

SQL commands are broadly grouped into categories based on their functionality: **Data Query Language (DQL)**, **Data Definition Language (DDL)**, **Data Manipulation Language (DML)**, **Data Control Language (DCL)**, and **Transaction Control Language (TCL)**.

---

## **1. Data Query Language (DQL)**
These commands retrieve data from the database.
- `SELECT` – Retrieve data from one or more tables.
    - `SELECT * FROM table_name;` – Select all columns.
    - `SELECT column1, column2 FROM table_name;` – Select specific columns.
    - `SELECT DISTINCT column_name FROM table_name;` – Retrieve unique values.

---

## **2. Data Definition Language (DDL)**
These commands define the structure of the database (e.g., tables, schemas).
- `CREATE DATABASE` – Create a new database.
- `CREATE TABLE` – Create a new table.
- `ALTER TABLE` – Modify an existing table.
    - Add a column: `ALTER TABLE table_name ADD column_name datatype;`
    - Modify a column: `ALTER TABLE table_name MODIFY column_name datatype;`
    - Drop a column: `ALTER TABLE table_name DROP column_name;`
- `DROP TABLE` – Delete a table.
- `DROP DATABASE` – Delete a database.
- `TRUNCATE TABLE` – Remove all rows from a table without logging individual row deletions.
- `COMMENT` – Add comments to the database schema.
- `RENAME` – Rename a table or column.

---

## **3. Data Manipulation Language (DML)**
These commands handle data manipulation within tables.
- `INSERT` – Add new rows to a table.
    - `INSERT INTO table_name (column1, column2) VALUES (value1, value2);`
- `UPDATE` – Modify existing rows in a table.
    - `UPDATE table_name SET column_name = value WHERE condition;`
- `DELETE` – Remove rows from a table.
    - `DELETE FROM table_name WHERE condition;`

---

## **4. Data Control Language (DCL)**
These commands control access to the database.
- `GRANT` – Provide privileges to users.
    - `GRANT SELECT, INSERT ON table_name TO user_name;`
- `REVOKE` – Remove privileges from users.
    - `REVOKE SELECT ON table_name FROM user_name;`

---

## **5. Transaction Control Language (TCL)**
These commands handle transactions within the database.
- `BEGIN TRANSACTION` – Start a transaction.
- `COMMIT` – Save changes made in the transaction.
- `ROLLBACK` – Revert changes made in the transaction.
- `SAVEPOINT` – Define a point within a transaction to rollback to.
- `RELEASE SAVEPOINT` – Remove a defined savepoint.
- `SET TRANSACTION` – Define properties for a transaction.

---

## **6. Miscellaneous Commands**
### **Joins**
- `INNER JOIN` – Select rows with matching values in both tables.
- `LEFT JOIN` (or `LEFT OUTER JOIN`) – Select all rows from the left table and matching rows from the right table.
- `RIGHT JOIN` (or `RIGHT OUTER JOIN`) – Select all rows from the right table and matching rows from the left table.
- `FULL JOIN` (or `FULL OUTER JOIN`) – Select all rows with matches in either table.

### **Constraints**
- `NOT NULL` – Ensure a column cannot have NULL values.
- `UNIQUE` – Ensure all values in a column are unique.
- `PRIMARY KEY` – Combine `NOT NULL` and `UNIQUE` for a column or set of columns.
- `FOREIGN KEY` – Ensure referential integrity between tables.
- `CHECK` – Ensure all column values satisfy a condition.
- `DEFAULT` – Set a default value for a column.

### **Functions**
- Aggregate Functions:
    - `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- Scalar Functions:
    - `LEN()`, `ROUND()`, `UCASE()`/`UPPER()`, `LCASE()`/`LOWER()`

### **Views**
- `CREATE VIEW` – Create a virtual table.
- `DROP VIEW` – Remove a view.

### **Indexes**
- `CREATE INDEX` – Create an index for faster retrieval.
- `DROP INDEX` – Remove an index.

### **Set Operations**
- `UNION` – Combine results of two queries without duplicates.
- `UNION ALL` – Combine results of two queries including duplicates.
- `INTERSECT` – Return rows present in both queries.
- `EXCEPT` (or `MINUS`) – Return rows from the first query not in the second.

### **Conditions and Operators**
- Logical: `AND`, `OR`, `NOT`
- Comparison: `=`, `!=`, `<`, `>`, `<=`, `>=`
- Pattern Matching: `LIKE`, `NOT LIKE`
- NULL Checking: `IS NULL`, `IS NOT NULL`
- Ranges: `BETWEEN`, `NOT BETWEEN`
- Lists: `IN`, `NOT IN`

---

## **7. Advanced Commands**
- `WITH` (Common Table Expression or CTE) – Create temporary result sets.
- `CASE` – Implement conditional logic in queries.
- `GROUP BY` – Group rows sharing a property for aggregate functions.
- `HAVING` – Apply filters to grouped data.
- `ORDER BY` – Sort results by one or more columns.
- `LIMIT` or `FETCH` – Restrict the number of rows returned.

---

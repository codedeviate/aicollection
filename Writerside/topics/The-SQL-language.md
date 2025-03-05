# The SQL Language

SQL commands are broadly grouped into categories based on their functionality: **Data Query Language (DQL)**, **Data Definition Language (DDL)**, **Data Manipulation Language (DML)**, **Data Control Language (DCL)**, and **Transaction Control Language (TCL)**.

---

## 1. Data Query Language (DQL)
These commands retrieve data from the database.
- **`SELECT`** – Retrieve data from one or more tables.
  - `SELECT * FROM table_name;` – Select all columns.
  - `SELECT column1, column2 FROM table_name;` – Select specific columns.
  - `SELECT DISTINCT column_name FROM table_name;` – Retrieve unique values.

---

## 2. Data Definition Language (DDL)
These commands define the structure of the database (e.g., tables, schemas).
- **`CREATE DATABASE`** – Create a new database.
- **`CREATE TABLE`** – Create a new table.
- **`ALTER TABLE`** – Modify an existing table.
  - Add a column: `ALTER TABLE table_name ADD column_name datatype;`
  - Modify a column: `ALTER TABLE table_name MODIFY column_name datatype;`
  - Drop a column: `ALTER TABLE table_name DROP column_name;`
- **`DROP TABLE`** – Delete a table.
- **`DROP DATABASE`** – Delete a database.
- **`TRUNCATE TABLE`** – Remove all rows from a table without logging individual row deletions.
- **`COMMENT`** – Add comments to the database schema.
- **`RENAME`** – Rename a table or column.

---

## 3. Data Manipulation Language (DML)
These commands handle data manipulation within tables.
- **`INSERT`** – Add new rows to a table.
  - `INSERT INTO table_name (column1, column2) VALUES (value1, value2);`
- **`UPDATE`** – Modify existing rows in a table.
  - `UPDATE table_name SET column_name = value WHERE condition;`
- **`DELETE`** – Remove rows from a table.
  - `DELETE FROM table_name WHERE condition;`

---

## 4. Data Control Language (DCL)
These commands control access to the database.
- **`GRANT`** – Provide privileges to users.
  - `GRANT SELECT, INSERT ON table_name TO user_name;`
- **`REVOKE`** – Remove privileges from users.
  - `REVOKE SELECT ON table_name FROM user_name;`

---

## 5. Transaction Control Language (TCL)
These commands handle transactions within the database.
- **`BEGIN TRANSACTION`** – Start a transaction.
- **`COMMIT`** – Save changes made in the transaction.
- **`ROLLBACK`** – Revert changes made in the transaction.
- **`SAVEPOINT`** – Define a point within a transaction to rollback to.
- **`RELEASE SAVEPOINT`** – Remove a defined savepoint.
- **`SET TRANSACTION`** – Define properties for a transaction.

---

## 6. Miscellaneous Commands

### Joins
- **`INNER JOIN`** – Select rows with matching values in both tables.
- **`LEFT JOIN`** (or **`LEFT OUTER JOIN`**) – Select all rows from the left table and matching rows from the right table.
- **`RIGHT JOIN`** (or **`RIGHT OUTER JOIN`**) – Select all rows from the right table and matching rows from the left table.
- **`FULL JOIN`** (or **`FULL OUTER JOIN`**) – Select all rows with matches in either table.

### Constraints
- **`NOT NULL`** – Ensure a column cannot have NULL values.
- **`UNIQUE`** – Ensure all values in a column are unique.
- **`PRIMARY KEY`** – Combine `NOT NULL` and `UNIQUE` for a column or set of columns.
- **`FOREIGN KEY`** – Ensure referential integrity between tables.
- **`CHECK`** – Ensure all column values satisfy a condition.
- **`DEFAULT`** – Set a default value for a column.

### Functions
- **Aggregate Functions:**
  - `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- **Scalar Functions:**
  - `LEN()`, `ROUND()`, `UCASE()`/`UPPER()`, `LCASE()`/`LOWER()`

### Views
- **`CREATE VIEW`** – Create a virtual table.
- **`DROP VIEW`** – Remove a view.

### Indexes
- **`CREATE INDEX`** – Create an index for faster retrieval.
- **`DROP INDEX`** – Remove an index.

### Set Operations
- **`UNION`** – Combine results of two queries without duplicates.
- **`UNION ALL`** – Combine results of two queries including duplicates.
- **`INTERSECT`** – Return rows present in both queries.
- **`EXCEPT`** (or **`MINUS`**) – Return rows from the first query not in the second.

### Conditions and Operators
- **Logical:** `AND`, `OR`, `NOT`
- **Comparison:** `=`, `!=`, `<`, `>`, `<=`, `>=`
- **Pattern Matching:** `LIKE`, `NOT LIKE`
- **NULL Checking:** `IS NULL`, `IS NOT NULL`
- **Ranges:** `BETWEEN`, `NOT BETWEEN`
- **Lists:** `IN`, `NOT IN`

---

## 7. Advanced Commands
- **`WITH`** (Common Table Expression or CTE) – Create temporary result sets.
- **`CASE`** – Implement conditional logic in queries.
- **`GROUP BY`** – Group rows sharing a property for aggregate functions.
- **`HAVING`** – Apply filters to grouped data.
- **`ORDER BY`** – Sort results by one or more columns.
- **`LIMIT`** or **`FETCH`** – Restrict the number of rows returned.

---

## 8. JSON Functions and Their Role in SQL

With the rise of semi-structured data, many modern databases have integrated JSON support into SQL. JSON functions enable you to store, query, and manipulate JSON data directly within your relational database. This fusion allows you to harness the flexibility of JSON while maintaining the rigor of SQL.

### Key Features of JSON Functions:
- **Storage and Data Types:**
  - **PostgreSQL:** Offers both `JSON` (textual) and `JSONB` (binary) types.
  - **MySQL:** Uses the `JSON` data type for optimized storage.
  - **SQL Server:** Stores JSON as `NVARCHAR` while providing JSON-specific functions.
  - **Oracle:** Supports JSON storage in `CLOB`, `BLOB`, or `VARCHAR2` fields.

- **Core JSON Functions:**
  - **Extraction:**
    - PostgreSQL: `->` and `->>` operators
    - MySQL: `JSON_EXTRACT()`
    - SQL Server: `JSON_VALUE()`
    - Oracle: `JSON_VALUE()`

  - **Modification:**
    - PostgreSQL: `jsonb_set()`
    - MySQL: `JSON_SET()`
    - SQL Server: Use custom functions or application logic
    - Oracle: `JSON_QUERY()` for extracting objects/arrays

  - **Construction:**
    - PostgreSQL: `to_json()`, `json_build_object()`
    - MySQL: `JSON_OBJECT()`, `JSON_ARRAY()`
    - SQL Server: `FOR JSON` clause
    - Oracle: `JSON_OBJECT()`, `JSON_ARRAY()`

### Practical Example (PostgreSQL):

```sql
-- Extracting a field from a JSONB column
SELECT info->>'name' AS employee_name
FROM employees
WHERE info->>'department' = 'Engineering';

-- Updating a JSONB field
UPDATE employees
SET info = jsonb_set(info, '{salary}', '75000'::jsonb)
WHERE info->>'employee_id' = '12345';
```

### Best Practices (JSON Functions):
- **Index JSON Attributes:** Use expression indexes where supported (e.g., PostgreSQL JSONB).
- **Validate JSON Format:** Employ constraints (e.g., Oracle’s `IS JSON`) to ensure data integrity.
- **Minimize Nesting:** Keep JSON structures as flat as possible for better performance.
- **Combine with Relational Data:** Use JSON functions alongside SQL to balance flexibility and performance.

---

## 9. Regular Expressions in SQL

Regular expressions (regex) provide advanced pattern matching capabilities that are essential for data validation, searching, and transformation. Many databases now support regex either natively or through additional functions, allowing you to integrate powerful text processing into your SQL queries.

### Regular Expression Support Across Databases:

- **PostgreSQL:**
  - **Operators:** `~` (case-sensitive), `~*` (case-insensitive), `!~`, `!~*`
  - **Functions:**
    - `regexp_matches()` to extract matching patterns
    - `regexp_replace()` to substitute parts of strings
  - **Example:**
    ```sql
    SELECT regexp_replace(phone, '[^\d]', '', 'g') AS clean_phone
    FROM customers;
    ```

- **MySQL:**
  - **Operators:** `REGEXP` or `RLIKE`
  - **Functions:**
    - `REGEXP_REPLACE()` for substitutions
    - `REGEXP_INSTR()` and `REGEXP_SUBSTR()` for extraction
  - **Example:**
    ```sql
    SELECT REGEXP_REPLACE(phone, '[^0-9]', '') AS clean_phone
    FROM customers;
    ```

- **Oracle:**
  - **Functions:**
    - `REGEXP_LIKE()` for filtering
    - `REGEXP_REPLACE()` for substitutions
    - `REGEXP_INSTR()` and `REGEXP_SUBSTR()` for locating and extracting text
  - **Example:**
    ```sql
    SELECT REGEXP_SUBSTR(notes, '[0-9]+') AS extracted_number
    FROM orders;
    ```

- **SQL Server:**
  - **Approaches:**
    - No native regex functions; can use CLR integration for custom regex functions
    - T-SQL’s `LIKE` offers limited pattern matching
  - **Example (CLR-based):**
    ```sql
    -- Assuming dbo.RegexMatch is a user-defined CLR function
    SELECT * FROM employees
    WHERE dbo.RegexMatch(first_name, '^A') = 1;
    ```

### Best Practices (Regular Expressions):
- **Optimize for Performance:** Regex operations can be resource-intensive; combine them with indexed filtering where possible.
- **Test Your Patterns:** Use external regex testers to validate patterns before embedding them in queries.
- **Keep It Readable:** Comment and document complex regex patterns to aid future maintenance.
- **Understand Database Nuances:** Each database has its own regex syntax and capabilities—ensure your regex functions are tailored to your chosen system.

---

## Conclusion

This comprehensive overview of the SQL language has explored not only the classic command categories—DQL, DDL, DML, DCL, and TCL—but also the array of miscellaneous and advanced commands that empower developers to build robust, secure, and efficient databases. With additional sections on JSON functions and regular expressions, modern SQL has evolved to handle both structured and semi-structured data, and to perform sophisticated text processing directly within queries.

By leveraging these features and following best practices, you can harness the full potential of SQL to meet the demands of today's data-driven applications.
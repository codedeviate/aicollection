# WITH

*An In-Depth Guide*

The SQL **WITH** clause, also known as Common Table Expressions (CTEs), is a powerful feature that allows you to write cleaner, more maintainable queries. By letting you define temporary result sets that can be referenced within your main query, the WITH clause enhances readability, modularity, and even performance in some cases. In this article, we’ll dive deep into how to use the WITH clause, exploring various examples and advanced use cases.

> This is the initial version on the article about [CTEs](Languages-SQL-CTE.md). There are some minor differences between the articles, but not enough to throw this one away.
---

## Table of Contents

1. [Introduction to CTEs](#introduction-to-ctes)
2. [Basic Syntax and Examples](#basic-syntax-and-examples)
3. [Using Multiple CTEs](#using-multiple-ctes)
4. [Recursive CTEs](#recursive-ctes)
5. [Advanced Examples and Use Cases](#advanced-examples-and-use-cases)
6. [Best Practices and Considerations](#best-practices-and-considerations)
7. [Conclusion](#conclusion)

---

## Introduction to CTEs

A Common Table Expression (CTE) is a temporary result set that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement. Introduced with the SQL:1999 standard, CTEs simplify complex joins and subqueries by breaking them down into reusable building blocks. They improve the organization of your SQL code, making it easier to read and debug.

**Key Benefits:**

- **Improved Readability:** Break complex queries into understandable parts.
- **Modularity:** Reuse temporary result sets within a single query.
- **Recursive Queries:** Simplify hierarchical or recursive data relationships.
- **Maintainability:** Isolate logic in separate CTEs for easier debugging and future modifications.

---

## Basic Syntax and Examples

### Basic Structure

The basic syntax of a CTE is:

```sql
WITH cte_name AS (
    -- Your query goes here
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition
)
SELECT *
FROM cte_name;
```

### Example 1: Simple CTE

Suppose you have a table named `employees` and you want to filter out employees with a salary greater than 50,000. Using a CTE can simplify the query:

```sql
WITH high_salary_employees AS (
    SELECT employee_id, first_name, last_name, salary
    FROM employees
    WHERE salary > 50000
)
SELECT *
FROM high_salary_employees;
```

This query first creates a temporary table `high_salary_employees` containing employees with high salaries, and then it selects all columns from that CTE.

---

## Using Multiple CTEs

CTEs can be chained together in a single query. This is useful when you need to build a series of steps to transform your data.

### Example 2: Multiple CTEs

Imagine you need to process sales data. First, filter out recent sales, then calculate the total sales per region.

```sql
WITH recent_sales AS (
    SELECT sale_id, region, amount, sale_date
    FROM sales
    WHERE sale_date >= '2025-01-01'
),
region_totals AS (
    SELECT region, SUM(amount) AS total_sales
    FROM recent_sales
    GROUP BY region
)
SELECT *
FROM region_totals
ORDER BY total_sales DESC;
```

Here, `recent_sales` is used to isolate sales from 2025 onward, and `region_totals` aggregates the results by region.

---

## Recursive CTEs

Recursive CTEs are especially useful for querying hierarchical data, such as organizational charts or folder structures.

### Basic Structure of a Recursive CTE

A recursive CTE consists of two parts:

1. **Anchor Member:** The initial query that defines the starting point.
2. **Recursive Member:** A query that references the CTE itself, which is repeatedly executed until it no longer returns any new rows.

### Example 3: Hierarchical Employee Reporting

Assume you have an `employees` table with columns `employee_id`, `manager_id`, and `employee_name`. To list all employees under a particular manager, you could write:

```sql
WITH RECURSIVE employee_hierarchy AS (
    -- Anchor member: start with the manager
    SELECT employee_id, employee_name, manager_id
    FROM employees
    WHERE employee_id = 1  -- Starting manager's ID
    
    UNION ALL
    
    -- Recursive member: get employees reporting to the ones already found
    SELECT e.employee_id, e.employee_name, e.manager_id
    FROM employees e
    INNER JOIN employee_hierarchy eh ON e.manager_id = eh.employee_id
)
SELECT *
FROM employee_hierarchy;
```

This query starts with the manager with `employee_id = 1` and recursively finds all employees that report directly or indirectly to this manager.

---

## Advanced Examples and Use Cases

### Example 4: Using CTEs for Data Transformation

CTEs can be used to perform complex data transformations. For instance, if you have a table of transactions and want to calculate running totals, you might combine window functions with CTEs.

```sql
WITH ordered_transactions AS (
    SELECT 
        transaction_id,
        amount,
        transaction_date,
        ROW_NUMBER() OVER (ORDER BY transaction_date) AS rn
    FROM transactions
),
running_totals AS (
    SELECT 
        t1.transaction_id,
        t1.amount,
        t1.transaction_date,
        SUM(t2.amount) AS running_total
    FROM ordered_transactions t1
    JOIN ordered_transactions t2 ON t2.rn <= t1.rn
    GROUP BY t1.transaction_id, t1.amount, t1.transaction_date
)
SELECT *
FROM running_totals
ORDER BY transaction_date;
```

This example creates a row number for each transaction and calculates a running total by summing amounts up to each transaction row.

### Example 5: Combining CTEs with Other SQL Constructs

CTEs are not limited to SELECT queries. They can also be integrated into INSERT, UPDATE, or DELETE statements.

#### Using CTE in an UPDATE Statement

Suppose you want to update the salary of employees based on a computed bonus stored in a CTE:

```sql
WITH bonus_calculation AS (
    SELECT 
        employee_id,
        salary,
        salary * 0.10 AS bonus  -- 10% bonus calculation
    FROM employees
    WHERE performance_rating = 'Excellent'
)
UPDATE employees
SET salary = salary + bonus
FROM bonus_calculation
WHERE employees.employee_id = bonus_calculation.employee_id;
```

This query calculates a 10% bonus for employees with an 'Excellent' performance rating and then updates their salaries accordingly.

---

## Best Practices and Considerations

1. **Readability:** Use meaningful names for your CTEs. This makes the code easier to understand for you and your colleagues.
2. **Performance:** While CTEs can simplify your queries, they are not always optimized by every SQL engine. Sometimes, rewriting the query without a CTE may yield better performance. Always review execution plans.
3. **Limit Recursion:** For recursive CTEs, most databases have a default recursion limit (e.g., 100 iterations). Ensure that your recursive logic terminates properly to avoid infinite loops.
4. **Modularity:** Break down large queries into multiple CTEs to isolate logic and simplify debugging.
5. **Temporary Nature:** Remember that CTEs exist only for the duration of the query. They are not stored as database objects.

---

## Conclusion

The SQL WITH clause and CTEs are invaluable tools for crafting efficient, readable, and maintainable SQL queries. From simplifying complex joins and subqueries to handling recursive data structures, mastering CTEs can significantly improve your database querying skills. Whether you're filtering data, performing transformations, or updating records based on computed values, the WITH clause provides a flexible and powerful way to manage your SQL logic.

By understanding both the basic and advanced uses of CTEs, you can build robust solutions that are both easy to maintain and performant. Happy querying!

--- 

This in-depth article has walked through the fundamentals of the SQL WITH clause along with practical examples and advanced use cases to help you harness its full potential in your projects.
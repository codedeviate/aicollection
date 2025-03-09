# UNION

*In-Depth Guide, Examples, and Alternatives*

SQL’s **UNION** operator is a fundamental tool for combining the results of multiple SELECT queries into one unified result set. Unlike UNION ALL, which simply appends rows together, UNION eliminates duplicate rows, ensuring that the final dataset contains only unique records. In this article, we’ll explore the intricacies of UNION, illustrate its use with practical examples, and discuss alternative methods to address similar challenges.

---

## Table of Contents

1. [Understanding UNION](#understanding-union)
2. [UNION vs. UNION ALL](#union-vs-union-all)
3. [Basic Syntax and Examples](#basic-syntax-and-examples)
4. [Advanced Use Cases](#advanced-use-cases)
5. [Alternative Approaches](#alternative-approaches)
6. [Performance Considerations](#performance-considerations)
7. [Conclusion](#conclusion)

---

## Understanding UNION

The SQL **UNION** operator allows you to combine the results of two or more SELECT queries into a single result set. Its key characteristic is that it removes duplicate rows from the final output. This behavior makes UNION ideal when you need a consolidated view of data and want to ensure each record appears only once.

**Key Points:**

- **Eliminates Duplicates:** UNION performs a distinct operation on the result set.
- **Multiple Data Sources:** It’s useful for merging data from different tables or queries.
- **Schema Consistency:** All SELECT statements must have the same number of columns and compatible data types.

---

## UNION vs. UNION ALL

Before diving deeper, it’s important to understand how UNION differs from UNION ALL:

- **UNION:**
    - Combines results and removes duplicates.
    - May involve additional processing overhead due to duplicate elimination.
    - Ideal when you need a unique set of records.

- **UNION ALL:**
    - Combines results without removing duplicates.
    - Typically faster because it avoids the overhead of checking for duplicates.
    - Best used when you are sure that duplicates are either acceptable or impossible.

---

## Basic Syntax and Examples

### Basic UNION Example

Suppose you have two tables, `table_a` and `table_b`, with the same structure, and you want to combine their data without duplicates:

```sql
SELECT id, name, created_date
FROM table_a
UNION
SELECT id, name, created_date
FROM table_b;
```

In this example, UNION ensures that if the same row appears in both tables, it will be returned only once in the final result set.

### Example with Different Conditions

Imagine you have two sales channels and you want a unique list of sales IDs from both channels:

```sql
SELECT sale_id, sale_date, amount
FROM online_sales
WHERE amount > 100
UNION
SELECT sale_id, sale_date, amount
FROM store_sales
WHERE amount > 100;
```

Here, UNION merges the filtered sales data from both channels, eliminating any duplicate records that might arise if a sale is recorded in both tables.

---

## Advanced Use Cases

### Example 1: Aggregated Reporting with Unique Data

Consider a scenario where you want to report on customer orders from two systems and ensure that each order is counted only once. You might have:

```sql
SELECT customer_id, COUNT(order_id) AS total_orders
FROM (
    SELECT order_id, customer_id
    FROM online_orders
    UNION
    SELECT order_id, customer_id
    FROM retail_orders
) AS combined_orders
GROUP BY customer_id;
```

This query uses a subquery with UNION to combine orders from both systems and then aggregates them by customer, ensuring duplicates are removed before the count.

### Example 2: Combining Data with Standardized Columns

When data sources have slightly different column names or formats, you can standardize them for a unified query:

```sql
SELECT customer_id, order_date, total_amount, 'Online' AS source
FROM online_orders
UNION
SELECT client_id AS customer_id, purchase_date AS order_date, amount AS total_amount, 'Retail' AS source
FROM retail_orders;
```

This approach aligns columns and labels data sources, making it easier to analyze consolidated data without duplicate entries.

### Example 3: Hierarchical Data Considerations

While UNION is not inherently recursive, you might combine it with recursive queries to ensure unique hierarchical data is returned. For instance, consider:

```sql
WITH RECURSIVE org_chart AS (
    SELECT employee_id, manager_id, employee_name
    FROM employees
    WHERE manager_id IS NULL  -- top-level employees
    UNION
    SELECT e.employee_id, e.manager_id, e.employee_name
    FROM employees e
    INNER JOIN org_chart oc ON e.manager_id = oc.employee_id
)
SELECT DISTINCT employee_id, manager_id, employee_name
FROM org_chart;
```

Here, UNION is used in a recursive CTE to build an organizational chart, and the DISTINCT clause (which is conceptually similar to UNION’s duplicate removal) ensures each employee appears only once.

---

## Alternative Approaches

While UNION is a powerful tool, there are scenarios where alternative methods might be more appropriate:

### 1. UNION ALL with DISTINCT

If you prefer to control duplicate elimination explicitly, you might first combine results with UNION ALL and then apply a DISTINCT:

```sql
SELECT DISTINCT id, name, created_date
FROM (
    SELECT id, name, created_date
    FROM table_a
    UNION ALL
    SELECT id, name, created_date
    FROM table_b
) AS combined_tables;
```

This two-step process gives you more control over when and how duplicates are removed.

### 2. JOINs

**When to Use:**
- To combine data based on a common key rather than simply appending rows.

**Example:**

```sql
SELECT a.id, a.name, b.order_total
FROM customers a
JOIN orders b ON a.id = b.customer_id;
```

JOINs combine rows based on related keys and are a preferred method when you need relational data rather than a flat union of two datasets.

### 3. Conditional Aggregation

**When to Use:**
- When pivoting or summarizing data from multiple sources into distinct categories.

**Example:**

```sql
SELECT
    customer_id,
    COUNT(CASE WHEN source = 'Online' THEN order_id END) AS online_orders,
    COUNT(CASE WHEN source = 'Retail' THEN order_id END) AS retail_orders
FROM (
    SELECT order_id, customer_id, 'Online' AS source
    FROM online_orders
    UNION ALL
    SELECT order_id, customer_id, 'Retail' AS source
    FROM retail_orders
) AS combined_orders
GROUP BY customer_id;
```

Here, UNION ALL is used to combine data and conditional aggregation is applied to derive insights, while ensuring that duplicates are properly handled through the logic of aggregation.

---

## Performance Considerations

- **Duplicate Elimination Overhead:**  
  UNION’s built-in mechanism to remove duplicates requires extra processing, which might impact performance on very large datasets.
- **Execution Plans:**  
  Always examine your SQL engine’s execution plan. Some systems optimize UNION operations effectively, while others might benefit from alternative approaches like UNION ALL followed by DISTINCT.
- **Data Volume:**  
  For large data sets where duplicates are rare or already handled by data integrity constraints, UNION ALL might be a more efficient choice. In such cases, consider whether the overhead of duplicate elimination is necessary.

---

## Conclusion

The SQL **UNION** operator is an essential tool for merging multiple result sets while ensuring uniqueness. Its ability to eliminate duplicates makes it ideal for consolidated reporting and data integration tasks where data redundancy must be avoided. However, it’s important to weigh its use against alternatives—such as UNION ALL with DISTINCT, JOINs, or conditional aggregation—depending on your specific requirements and data characteristics.

By understanding UNION’s behavior, syntax, and performance implications, you can choose the most appropriate method for your data needs and craft SQL queries that are both efficient and maintainable.

Happy querying!
# UNION ALL

*In-Depth Guide, Examples, and Alternatives*

SQL offers multiple ways to combine results from separate queries. One of the most powerful and frequently used operators for this purpose is **UNION ALL**. This article explores the ins and outs of SQL's UNION ALL operator, provides several practical examples, and discusses alternative methods for solving similar problems.

---

## Table of Contents

1. [Understanding UNION ALL](#understanding-union-all)
2. [UNION ALL vs. UNION](#union-all-vs-union)
3. [Basic Syntax and Examples](#basic-syntax-and-examples)
4. [Advanced Use Cases](#advanced-use-cases)
5. [Alternative Approaches](#alternative-approaches)
6. [Performance Considerations](#performance-considerations)
7. [Conclusion](#conclusion)

---

## Understanding UNION ALL

**UNION ALL** is used to combine the results of two or more SELECT queries into a single result set. Unlike the plain **UNION** operator, which eliminates duplicate rows, UNION ALL returns all rows from each query, including duplicates.

### When to Use UNION ALL

- **Performance:** Since UNION ALL does not remove duplicates, it generally runs faster than UNION.
- **Data Aggregation:** When you know your data sets are mutually exclusive or duplicates are acceptable.
- **Reporting:** When you need to merge data from multiple sources without filtering out repeated values.

---

## UNION ALL vs. UNION

- **UNION:** Combines query results and removes duplicate rows. This duplicate removal requires additional processing.

  ```sql
  SELECT column1 FROM table1
  UNION
  SELECT column1 FROM table2;
  ```

- **UNION ALL:** Combines query results without duplicate elimination, making it more efficient when duplicates are not a concern.

  ```sql
  SELECT column1 FROM table1
  UNION ALL
  SELECT column1 FROM table2;
  ```

Understanding the difference is crucial when performance and data integrity are a priority.

---

## Basic Syntax and Examples

### Example 1: Simple UNION ALL

Suppose you have two tables, `online_sales` and `store_sales`, with similar structures. You want to create a combined list of all sales:

```sql
SELECT sale_id, sale_date, amount
FROM online_sales
UNION ALL
SELECT sale_id, sale_date, amount
FROM store_sales;
```

This query will merge all rows from both tables, including any duplicates, into a single result set.

### Example 2: Combining Data with Different Conditions

Imagine you need a report of current year sales from two different departments:

```sql
SELECT sale_id, sale_date, amount, 'Electronics' AS department
FROM electronics_sales
WHERE YEAR(sale_date) = 2025
UNION ALL
SELECT sale_id, sale_date, amount, 'Clothing' AS department
FROM clothing_sales
WHERE YEAR(sale_date) = 2025;
```

Here, UNION ALL not only combines the rows but also tags each record with a department name.

---

## Advanced Use Cases

### Example 3: Aggregating Data from Multiple Sources

Suppose you want to see a combined total of revenue from various channels:

```sql
SELECT channel, SUM(amount) AS total_revenue
FROM (
    SELECT 'Online' AS channel, amount
    FROM online_sales
    UNION ALL
    SELECT 'In-Store' AS channel, amount
    FROM store_sales
    UNION ALL
    SELECT 'Phone' AS channel, amount
    FROM phone_sales
) AS all_sales
GROUP BY channel;
```

In this example, UNION ALL is used inside a subquery to consolidate data from three channels before performing aggregation.

### Example 4: Handling Heterogeneous Data

When combining data from different sources, sometimes you need to adjust the schema to match:

```sql
SELECT customer_id, order_date, amount, 'E-commerce' AS order_source
FROM ecommerce_orders
UNION ALL
SELECT client_id AS customer_id, purchase_date AS order_date, total AS amount, 'Retail' AS order_source
FROM retail_orders;
```

This query standardizes column names and formats, making it possible to analyze data from different systems in a unified way.

---

## Alternative Approaches

While UNION ALL is often the best tool for combining result sets, there are scenarios where alternative methods might be appropriate:

### 1. **JOINs**

**When to Use:**
- If you need to combine rows based on a common key rather than appending them vertically.

**Example:**

```sql
SELECT o.order_id, o.amount, c.customer_name
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id;
```

This join-based approach is ideal when data from two tables share a relationship, unlike UNION ALL, which simply stacks rows.

### 2. **Conditional Aggregation**

**When to Use:**
- To pivot data or consolidate similar rows from multiple sources into a single summary.

**Example:**

```sql
SELECT
    SUM(CASE WHEN channel = 'Online' THEN amount ELSE 0 END) AS online_revenue,
    SUM(CASE WHEN channel = 'In-Store' THEN amount ELSE 0 END) AS in_store_revenue
FROM sales;
```

This method can sometimes replace UNION ALL by combining rows into aggregated columns.

### 3. **Subqueries with Combined SELECTs**

**When to Use:**
- When data transformation or filtering needs to occur before combining rows.

**Example:**

```sql
SELECT sale_id, sale_date, amount
FROM (
    SELECT sale_id, sale_date, amount
    FROM online_sales
    WHERE amount > 100
    UNION ALL
    SELECT sale_id, sale_date, amount
    FROM store_sales
    WHERE amount > 100
) AS high_value_sales;
```

This alternative demonstrates how subqueries can be nested to pre-filter data, similar to how UNION ALL operates.

---

## Performance Considerations

- **Efficiency:** UNION ALL is more efficient than UNION because it doesn’t require a distinct operation to eliminate duplicates.
- **Execution Plan:** Most modern SQL optimizers are smart enough to handle both UNION and UNION ALL effectively. However, reviewing execution plans in your environment is always recommended.
- **Data Volume:** For large data sets, the overhead of duplicate elimination in UNION might become significant, making UNION ALL the preferred choice when duplicates are not an issue.

---

## Conclusion

**UNION ALL** is a versatile operator that allows you to merge result sets from multiple queries without the overhead of duplicate elimination. It’s especially useful for performance-critical applications, data aggregation, and consolidating heterogeneous data sources. While UNION ALL is often the best choice, it’s important to understand alternative methods such as JOINs, conditional aggregation, or subqueries, as these can sometimes provide more suitable solutions based on your specific data relationships and reporting needs.

By mastering UNION ALL and its alternatives, you can write cleaner, more efficient, and more flexible SQL queries tailored to a wide range of real-world scenarios. Happy querying!
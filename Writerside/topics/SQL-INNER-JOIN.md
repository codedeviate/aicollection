# INNER JOIN

## **SQL INNER JOIN: Comprehensive Explanation**

The `INNER JOIN` is one of the most commonly used join types in SQL. It retrieves records that have matching values in both tables being joined. Essentially, it creates a new result table by combining columns from both tables based on a related column (called the "join condition").

---

## **Syntax**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

- `table1` and `table2`: The tables you are joining.
- `ON`: Specifies the condition to match rows from `table1` and `table2`.
- `column_name`: The column(s) used to establish the relationship between the two tables.

---

## **How it Works**
- Only rows that satisfy the `ON` condition are included in the result.
- If no match is found, those rows are excluded from the output.

---

## **Example Scenario**
Suppose we have two tables:

**1. `Customers` Table**
| CustomerID | Name        | Country  |
|------------|-------------|----------|
| 1          | Alice       | USA      |
| 2          | Bob         | Canada   |
| 3          | Charlie     | UK       |

**2. `Orders` Table**
| OrderID | CustomerID | Product   |
|---------|------------|-----------|
| 101     | 1          | Laptop    |
| 102     | 2          | Tablet    |
| 103     | 1          | Smartphone|
| 104     | 4          | Monitor   |

---

## **Example 1: Joining Two Tables**
Query to find all customers who placed orders:
```sql
SELECT Customers.CustomerID, Customers.Name, Orders.Product
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

**Result:**
| CustomerID | Name   | Product     |
|------------|--------|-------------|
| 1          | Alice  | Laptop      |
| 1          | Alice  | Smartphone  |
| 2          | Bob    | Tablet      |

**Explanation:**
- Only rows with matching `CustomerID` in both tables are included.
- The row for `CustomerID = 3` from `Customers` is excluded because Charlie hasn't placed any orders.
- The row for `CustomerID = 4` in `Orders` is excluded because no matching customer exists.

---

## **Example 2: Using Aliases for Better Readability**
You can use table aliases to simplify the query:
```sql
SELECT C.Name, O.Product
FROM Customers C
INNER JOIN Orders O
ON C.CustomerID = O.CustomerID;
```
This produces the same result as above.

---

## **Example 3: Filtering with INNER JOIN**
Add a `WHERE` clause to filter the results further. For instance, find orders placed by customers from the USA:
```sql
SELECT C.Name, O.Product
FROM Customers C
INNER JOIN Orders O
ON C.CustomerID = O.CustomerID
WHERE C.Country = 'USA';
```

**Result:**
| Name   | Product     |
|--------|-------------|
| Alice  | Laptop      |
| Alice  | Smartphone  |

---

## **Example 4: Multiple Conditions in the JOIN**
If you need to join tables on more than one condition:
```sql
SELECT *
FROM Customers C
INNER JOIN Orders O
ON C.CustomerID = O.CustomerID AND C.Country = 'USA';
```

This query ensures that only orders placed by customers from the USA are joined.

---

## **Example 5: INNER JOIN on Multiple Tables**
You can join more than two tables in one query. Suppose we have another table, `Products`:

**`Products` Table**
| ProductID | Product      | Price |
|-----------|--------------|-------|
| 1         | Laptop       | 1000  |
| 2         | Smartphone   | 700   |
| 3         | Tablet       | 500   |

Join all three tables:
```sql
SELECT C.Name, O.Product, P.Price
FROM Customers C
INNER JOIN Orders O
ON C.CustomerID = O.CustomerID
INNER JOIN Products P
ON O.Product = P.Product;
```

**Result:**
| Name   | Product     | Price |
|--------|-------------|-------|
| Alice  | Laptop      | 1000  |
| Alice  | Smartphone  | 700   |
| Bob    | Tablet      | 500   |

---

## **Key Points**
1. **Default Behavior:** If no matching rows exist in either table, those rows are excluded from the result.
2. **Efficiency:** `INNER JOIN` can be optimized using indexes on the join columns.
3. **Aliases:** Use table aliases for readability in queries involving multiple tables.

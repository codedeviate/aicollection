# JOIN

In SQL, joins are used to combine rows from two or more tables based on a related column between them. Here are the different types of joins:

1. **INNER JOIN**: Returns only the rows that have matching values in both tables.
   ```sql
   SELECT columns
   FROM table1
   INNER JOIN table2
   ON table1.common_column = table2.common_column;
   ```

2. **LEFT JOIN (or LEFT OUTER JOIN)**: Returns all rows from the left table, and the matched rows from the right table. If no match is found, NULL values are returned for columns from the right table.
   ```sql
   SELECT columns
   FROM table1
   LEFT JOIN table2
   ON table1.common_column = table2.common_column;
   ```

3. **RIGHT JOIN (or RIGHT OUTER JOIN)**: Returns all rows from the right table, and the matched rows from the left table. If no match is found, NULL values are returned for columns from the left table.
   ```sql
   SELECT columns
   FROM table1
   RIGHT JOIN table2
   ON table1.common_column = table2.common_column;
   ```

4. **FULL JOIN (or FULL OUTER JOIN)**: Returns all rows when there is a match in either table. If there is no match, the result is NULL on the side that does not have a match.
   ```sql
   SELECT columns
   FROM table1
   FULL JOIN table2
   ON table1.common_column = table2.common_column;
   ```

5. **CROSS JOIN**: Returns the Cartesian product of the two tables, i.e., it returns all possible combinations of rows from the tables.
   ```sql
   SELECT columns
   FROM table1
   CROSS JOIN table2;
   ```

6. **SELF JOIN**: A regular join but the table is joined with itself.
   ```sql
   SELECT a.columns, b.columns
   FROM table a, table b
   WHERE a.common_column = b.common_column;
   ```

These joins allow you to retrieve and combine data from multiple tables in various ways depending on the relationships and requirements of your query.
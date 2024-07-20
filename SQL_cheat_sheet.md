## **SQL Cheat Sheet**

### **1. Basics**

- **Basic Query**
  ```sql
  SELECT column1, column2
  FROM table_name;
  ```

- **Select All Columns**
  ```sql
  SELECT * FROM table_name;
  ```

- **Filtering Rows (WHERE)**
  ```sql
  SELECT column1, column2
  FROM table_name
  WHERE condition;
  ```

- **Ordering Results (ORDER BY)**
  ```sql
  SELECT column1, column2
  FROM table_name
  ORDER BY column1 ASC;  -- or DESC for descending
  ```

- **Limiting Results (LIMIT)**
  ```sql
  SELECT column1, column2
  FROM table_name
  LIMIT 10;
  ```

- **Inserting Data**
  ```sql
  INSERT INTO table_name (column1, column2)
  VALUES (value1, value2);
  ```

- **Updating Data**
  ```sql
  UPDATE table_name
  SET column1 = value1, column2 = value2
  WHERE condition;
  ```

- **Deleting Data**
  ```sql
  DELETE FROM table_name
  WHERE condition;
  ```

### **2. Joins**

- **Inner Join**
  ```sql
  SELECT columns
  FROM table1
  INNER JOIN table2
  ON table1.common_column = table2.common_column;
  ```

- **Left Join (or Left Outer Join)**
  ```sql
  SELECT columns
  FROM table1
  LEFT JOIN table2
  ON table1.common_column = table2.common_column;
  ```

- **Right Join (or Right Outer Join)**
  ```sql
  SELECT columns
  FROM table1
  RIGHT JOIN table2
  ON table1.common_column = table2.common_column;
  ```

- **Full Join (or Full Outer Join)**
  ```sql
  SELECT columns
  FROM table1
  FULL OUTER JOIN table2
  ON table1.common_column = table2.common_column;
  ```

- **Self Join**
  ```sql
  SELECT a.column1, b.column2
  FROM table_name a
  INNER JOIN table_name b
  ON a.common_column = b.common_column;
  ```

### **3. Aggregations**

- **COUNT**
  ```sql
  SELECT COUNT(*)
  FROM table_name;
  ```

- **SUM**
  ```sql
  SELECT SUM(column_name)
  FROM table_name;
  ```

- **AVG**
  ```sql
  SELECT AVG(column_name)
  FROM table_name;
  ```

- **MIN and MAX**
  ```sql
  SELECT MIN(column_name), MAX(column_name)
  FROM table_name;
  ```

- **GROUP BY**
  ```sql
  SELECT column1, COUNT(*)
  FROM table_name
  GROUP BY column1;
  ```

- **HAVING**
  ```sql
  SELECT column1, COUNT(*)
  FROM table_name
  GROUP BY column1
  HAVING COUNT(*) > 5;
  ```

### **4. Subqueries**

- **Subquery in SELECT**
  ```sql
  SELECT column1,
         (SELECT column2 FROM table2 WHERE table2.id = table1.id) AS subquery_result
  FROM table1;
  ```

- **Subquery in WHERE**
  ```sql
  SELECT column1
  FROM table_name
  WHERE column2 = (SELECT column2 FROM table2 WHERE condition);
  ```

- **EXISTS**
  ```sql
  SELECT column1
  FROM table_name
  WHERE EXISTS (SELECT 1 FROM table2 WHERE condition);
  ```

### **5. Set Operations**

- **UNION**
  ```sql
  SELECT column1 FROM table1
  UNION
  SELECT column1 FROM table2;
  ```

- **UNION ALL**
  ```sql
  SELECT column1 FROM table1
  UNION ALL
  SELECT column1 FROM table2;
  ```

- **INTERSECT**
  ```sql
  SELECT column1 FROM table1
  INTERSECT
  SELECT column1 FROM table2;
  ```

- **EXCEPT (or MINUS in some databases)**
  ```sql
  SELECT column1 FROM table1
  EXCEPT
  SELECT column1 FROM table2;
  ```

### **6. Indexes**

- **Creating Index**
  ```sql
  CREATE INDEX index_name
  ON table_name (column_name);
  ```

- **Dropping Index**
  ```sql
  DROP INDEX index_name;
  ```

### **7. Views**

- **Creating a View**
  ```sql
  CREATE VIEW view_name AS
  SELECT column1, column2
  FROM table_name
  WHERE condition;
  ```

- **Using a View**
  ```sql
  SELECT * FROM view_name;
  ```

- **Dropping a View**
  ```sql
  DROP VIEW view_name;
  ```

### **8. Transactions**

- **BEGIN TRANSACTION**
  ```sql
  BEGIN TRANSACTION;
  ```

- **COMMIT**
  ```sql
  COMMIT;
  ```

- **ROLLBACK**
  ```sql
  ROLLBACK;
  ```

### **9. Stored Procedures and Functions**

- **Creating a Stored Procedure**
  ```sql
  CREATE PROCEDURE procedure_name AS
  BEGIN
      -- SQL statements
  END;
  ```

- **Executing a Stored Procedure**
  ```sql
  EXEC procedure_name;
  ```

- **Creating a Function**
  ```sql
  CREATE FUNCTION function_name (param1 data_type, param2 data_type)
  RETURNS data_type
  AS
  BEGIN
      -- SQL statements
      RETURN value;
  END;
  ```

- **Using a Function**
  ```sql
  SELECT function_name(param1, param2);
  ```

### **10. User Management**

- **Creating a User**
  ```sql
  CREATE USER username WITH PASSWORD 'password';
  ```

- **Granting Privileges**
  ```sql
  GRANT ALL PRIVILEGES ON database_name TO username;
  ```

- **Revoking Privileges**
  ```sql
  REVOKE ALL PRIVILEGES ON database_name FROM username;
  ```

- **Dropping a User**
  ```sql
  DROP USER username;
  ```

### **11. Advanced Topics**

- **Common Table Expressions (CTEs)**
  ```sql
  WITH cte_name AS (
      SELECT column1, column2
      FROM table_name
      WHERE condition
  )
  SELECT * FROM cte_name;
  ```

- **Recursive CTE**
  ```sql
  WITH RECURSIVE cte_name AS (
      SELECT column1, column2
      FROM table_name
      WHERE condition
      UNION ALL
      SELECT t.column1, t.column2
      FROM table_name t
      INNER JOIN cte_name c ON t.column1 = c.column1
  )
  SELECT * FROM cte_name;
  ```

- **Window Functions**
  ```sql
  SELECT column1,
         ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column1) AS row_num
  FROM table_name;
  ```

- **Pivot Tables (In SQL Server)**
  ```sql
  SELECT *
  FROM (SELECT year, month, sales FROM sales_table) AS source_table
  PIVOT
  (
      SUM(sales)
      FOR month IN ([Jan], [Feb], [Mar])
  ) AS pivot_table;
  ```

- **Full-Text Search (In SQL Server)**
  ```sql
  SELECT * 
  FROM table_name
  WHERE CONTAINS(column_name, 'search_term');
  ```

- **JSON Handling (In MySQL)**
  ```sql
  SELECT JSON_EXTRACT(json_column, '$.key') AS value
  FROM table_name;
  ```

---

This cheat sheet provides an extensive overview of SQL commands and features, from basic queries to advanced techniques. Use it as a reference to handle various SQL tasks efficiently.
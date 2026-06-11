## Understanding SQL Query Execution Order

When we write a SQL query, it is not executed from top to bottom. The database follows its own logical execution order.

Consider the query:

```sql
SELECT department,
       COUNT(*) AS total_employees,
       AVG(salary) AS avg_salary
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING COUNT(*) > 2
ORDER BY avg_salary DESC
LIMIT 5;
```

### Actual Execution Order

1. **FROM**

   * The database first identifies the source table.
   * Here, it reads data from the `employees` table.

2. **WHERE**

   * Rows with `salary <= 50000` are filtered out.

3. **GROUP BY**

   * Remaining rows are grouped by `department`.

4. **HAVING**

   * Groups with 2 or fewer employees are removed.

5. **SELECT**

   * Required columns and aggregate functions are calculated.

6. **ORDER BY**

   * Results are sorted by average salary in descending order.

7. **LIMIT**

   * Only the first 5 rows are returned.

### Easy Way to Remember

```text
FROM
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
```

Although `SELECT` appears first in the query, it is processed after `FROM`, `WHERE`, `GROUP BY`, and `HAVING`.

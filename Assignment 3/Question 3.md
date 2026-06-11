## How DISTINCT Works with `*`

When we use:

```sql
SELECT DISTINCT * 
FROM employees;
```

the database removes rows that are completely identical. It compares all columns in each row, not just a single column.

For example:

| id | name   | department |
| -- | ------ | ---------- |
| 1  | Unnati | IT         |
| 1  | Unnati | IT         |
| 2  | Priya  | HR         |

After applying `DISTINCT *`, the result becomes:

| id | name   | department |
| -- | ------ | ---------- |
| 1  | Unnati | IT         |
| 2  | Priya  | HR         |

The duplicate row is removed because all column values are the same.

If even one column value is different, the rows are considered unique and both rows will be returned.

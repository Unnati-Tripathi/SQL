## ARRAY_AGG vs STRING_AGG in SQL

Both `ARRAY_AGG()` and `STRING_AGG()` are aggregate functions used to combine multiple values into a single result, but they return different data types.

### ARRAY_AGG()

`ARRAY_AGG()` collects values into an array.

Example:

```sql
SELECT department,
       ARRAY_AGG(name) AS employees
FROM employees
GROUP BY department;
```

Output:

```text
IT  | {Unnati,Priya,Riya}
HR  | {Amit,Sara}
```

### STRING_AGG()

`STRING_AGG()` combines values into a single string using a separator.

Example:

```sql
SELECT department,
       STRING_AGG(name, ', ') AS employees
FROM employees
GROUP BY department;
```

Output:

```text
IT  | Unnati, Priya, Riya
HR  | Amit, Sara
```

### Key Difference

| ARRAY_AGG()                     | STRING_AGG()                    |
| ------------------------------- | ------------------------------- |
| Returns an array                | Returns a string                |
| Values remain separate elements | Values are joined into one text |
| Useful for further processing   | Useful for reports and display  |

### When to Use

* Use **ARRAY_AGG()** when you need the result as a collection of values.
* Use **STRING_AGG()** when you want a readable comma-separated list.

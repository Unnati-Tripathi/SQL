# Question 1: String Aggregation

## Query

```sql
SELECT
    department_name,
    STRING_AGG(employee_name, ', ' ORDER BY employee_name) AS employee_list
FROM department_employees
GROUP BY department_name
ORDER BY department_name;
```

## My Understanding

Normally, each employee is stored in a separate row.

Example:

| department_name | employee_name |
|---------------|---------------|
| Engineering | Amit Kumar |
| Engineering | Priya Sharma |
| Engineering | Rahul Verma |

Using `STRING_AGG()` we can combine all employee names belonging to the same department into a single comma-separated string.

Output becomes:

```text
Engineering → Amit Kumar, Priya Sharma, Rahul Verma
```

### Functions Used

| Function | Purpose |
|----------|----------|
| `STRING_AGG()` | Combines multiple rows into a single string |
| `GROUP BY` | Creates one result row for each department |
| `ORDER BY employee_name` | Sorts employee names alphabetically inside the list |

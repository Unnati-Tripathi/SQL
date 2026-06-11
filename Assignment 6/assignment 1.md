# Assignment 5: Correlated Subquery

## Table Creation

```sql
CREATE TABLE employee_sales (
    emp_id      INT PRIMARY KEY,
    emp_name    VARCHAR(100),
    department  VARCHAR(50),
    city        VARCHAR(50),
    sale_amount DECIMAL(10,2),
    sale_month  VARCHAR(20),
    status      VARCHAR(20)
);
```

## Insert Data

```sql
INSERT INTO employee_sales VALUES
(101, 'Ananya', 'Tech', 'Lucknow', 45000.75, 'January', 'active'),
(102, 'Rohit', 'Tech', 'Kanpur', 62000.50, 'February', 'active'),
(103, 'Meera', 'Marketing', 'Delhi', 38000.25, 'March', 'active'),
(104, 'Kunal', 'Marketing', 'Noida', 52000.00, 'April', 'inactive'),
(105, 'Sneha', 'Finance', 'Pune', 70000.40, 'January', 'active'),
(106, 'Aman', 'Finance', 'Mumbai', 56000.90, 'February', 'inactive');
```

## View Table

```sql
SELECT * FROM employee_sales;
```

## Problem Statement

Find employees whose sale amount is greater than the average sale amount of employees working in the same department.

## Query

```sql
SELECT
    e1.emp_id,
    e1.emp_name,
    e1.department,
    e1.sale_amount
FROM employee_sales e1
WHERE e1.sale_amount > (
    SELECT AVG(e2.sale_amount)
    FROM employee_sales e2
    WHERE e2.department = e1.department
);
```

## Explanation

In this query, the outer query checks each employee one by one. For every employee, the inner query calculates the average sale amount of that employee's own department. The outer query then compares the employee's sale amount with that average and returns only those employees whose sale amount is greater than their department average.
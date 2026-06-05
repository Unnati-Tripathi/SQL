Find departments having at least 2 employees, where employee salary is greater than 50000. Show department name, employee count, and average salary. Sort by average salary high to low. Show only top 2 departments.


SELECT 
    d.dept_name,
    COUNT(e.emp_id) AS employee_count,
    AVG(e.salary) AS avg_salary
FROM employees e
JOIN departments d
    ON e.dept_id = d.dept_id
WHERE e.salary > 50000
GROUP BY d.dept_name
HAVING COUNT(e.emp_id) >= 2
ORDER BY avg_salary DESC
LIMIT 2;




Execution flow
1. FROM employees

SQL starts with:

FROM employees e

Main table:

Amit, Sara, Ravi, Neha, Karan, Priya, Dev, Meera
2. JOIN departments
JOIN departments d

SQL brings departments table.

3. Apply ON condition
ON e.dept_id = d.dept_id

Only matching employees remain.

Meera removed because her dept_id is NULL.

4. Produce joined rows

Now rows look like:

Amit  Engineering 85000
Sara  Marketing   62000
Ravi  Engineering 91000
Neha  HR          48000
Karan Engineering 95000
Priya Marketing   78000
Dev   HR          71000
5. WHERE
WHERE e.salary > 50000

Neha removed because salary is 48000.

Remaining:

Engineering: Amit, Ravi, Karan
Marketing: Sara, Priya
HR: Dev
6. GROUP BY
GROUP BY d.dept_name

Rows are grouped department-wise.

Engineering → 3 employees
Marketing   → 2 employees
HR          → 1 employee
7. HAVING
HAVING COUNT(e.emp_id) >= 2

Removes groups having less than 2 employees.

HR removed.

Remaining:

Engineering
Marketing
8. SELECT
SELECT d.dept_name, COUNT(e.emp_id), AVG(e.salary)

Output becomes:

Engineering | 3 | 90333.33
Marketing   | 2 | 70000.00
9. ORDER BY
ORDER BY avg_salary DESC

Highest average salary first.

Engineering first
Marketing second
10. LIMIT
LIMIT 2

Only first 2 rows shown.

Final output:

Engineering | 3 | 90333.33
Marketing   | 2 | 70000.00


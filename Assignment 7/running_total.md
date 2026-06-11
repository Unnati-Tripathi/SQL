## 1. Create Table

```sql
CREATE TABLE sales (
    id INT PRIMARY KEY,
    sale_date DATE,
    amount INT
);
```

---

## 2. Insert Data

```sql
INSERT INTO sales VALUES
(1, '2026-01-01', 100),
(2, '2026-01-02', 200),
(3, '2026-01-03', 300),
(4, '2026-01-04', 400),
(5, '2026-01-05', 500),
(6, '2026-01-06', 600),
(7, '2026-01-07', 700);
```

---
## 3. Dataset Preview

| id | sale_date  | amount |
|----|------------|--------|
| 1  | 2026-01-01 | 100    |
| 2  | 2026-01-02 | 200    |
| 3  | 2026-01-03 | 300    |
| 4  | 2026-01-04 | 400    |
| 5  | 2026-01-05 | 500    |
| 6  | 2026-01-06 | 600    |
| 7  | 2026-01-07 | 700    |

---
##  Calculate running total of sales

### Requirement
For each date, calculate total sales from the first date up to the current date.

### Answer

```sql
SELECT
    id,
    sale_date,
    amount,
    SUM(amount) OVER (
        ORDER BY sale_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM sales;
```

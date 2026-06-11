
---
## Calculate 2-row moving average

### Requirement
For each row, calculate the average of the current row and previous 1 row.

### Answer

```sql
SELECT
    id,
    sale_date,
    amount,
    AVG(amount) OVER (
        ORDER BY sale_date
        ROWS BETWEEN 1 PRECEDING AND CURRENT ROW
    ) AS moving_avg_2
FROM sales;
```

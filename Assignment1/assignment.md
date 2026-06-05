# Student Scholarship and Payment Management

## Overview

This system manages student scholarships and fee payments using three tables:

* `student`
* `scholarship`
* `payment`

The workflow is:

1. A student record is created.
2. If the student receives a scholarship, a scholarship record is inserted.
3. The remaining fee amount is calculated as:

```text
remaining_amount = total_amount - scholarship_amount
```

4. When the student pays the remaining fee, the payment status is updated.
5. Additional queries can be executed to track paid students and generate reports.

---

# Database Schema

## Student Table

```sql
CREATE TABLE student (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50) NOT NULL
);
```

Stores basic student information.

---

## Scholarship Table

```sql
CREATE TABLE scholarship (
    scholarship_id INT PRIMARY KEY,
    student_id INT,

    scholarship_amount INT,
    sch_status BOOLEAN DEFAULT FALSE,

    total_amount INT,
    remaining_amount INT,

    FOREIGN KEY (student_id)
    REFERENCES student(student_id)
);
```

### Columns

| Column             | Description                            |
| ------------------ | -------------------------------------- |
| scholarship_id     | Unique scholarship identifier          |
| student_id         | Student receiving scholarship          |
| scholarship_amount | Scholarship amount granted             |
| sch_status         | Scholarship granted status             |
| total_amount       | Total fee amount                       |
| remaining_amount   | Fee amount remaining after scholarship |

---

## Payment Table

```sql
CREATE TABLE payment (
    payment_id INT PRIMARY KEY,
    student_id INT,

    pay_status BOOLEAN DEFAULT FALSE,

    FOREIGN KEY (student_id)
    REFERENCES student(student_id)
);
```

### Columns

| Column     | Description               |
| ---------- | ------------------------- |
| payment_id | Unique payment identifier |
| student_id | Student making payment    |
| pay_status | Payment completion status |

---

# Scholarship Allocation

Assume:

* Scholarship Amount = `x`
* Student ID = `id`
* Scholarship ID = `y`
* Total Fee Amount = `total`

When a scholarship is granted, the remaining amount is calculated as:

```text
remaining_amount = total_amount - scholarship_amount
```

### Insert Scholarship Record

```sql
INSERT INTO scholarship (
    scholarship_id,
    student_id,
    scholarship_amount,
    sch_status,
    total_amount,
    remaining_amount
)
VALUES (
    y,
    id,
    x,
    TRUE,
    total,
    total - x
);
```

### Example

If:

```text
Total Fee = 100000
Scholarship = 25000
```

Then:

```text
Remaining Amount = 100000 - 25000
                 = 75000
```

---

# Fee Payment Process

At the time of payment:

1. Fetch `remaining_amount` from the `scholarship` table.
2. Collect the remaining fee amount.
3. Update payment status after successful payment.

### Update Payment Status

```sql
UPDATE payment
SET pay_status = TRUE
WHERE student_id = id;
```

---

# Count Students Who Have Paid

To determine how many students have completed payment:

```sql
SELECT COUNT(*)
FROM payment
WHERE pay_status = TRUE;
```

---

# Workflow Summary

```text
Student Created
       │
       ▼
Scholarship Granted
       │
       ▼
remaining_amount =
total_amount - scholarship_amount
       │
       ▼
Student Pays Remaining Amount
       │
       ▼
pay_status = TRUE
       │
       ▼
Reports / Analytics / Count Queries
```

---

# Future Enhancements

* Partial payment support
* Multiple scholarship types
* Payment transaction history
* Scholarship approval workflow
* Fee installment management
* Payment receipt generation
* Dashboard and reporting system

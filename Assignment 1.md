# Assignment - 1

## Problem Statement
Transaction Management at Scale

A nightly billing job needs to update 1 million records. Last week, the job crashed midway and the entire process had to restart from the beginning.
Write a SQL script that commits transactions efficiently and handles failures gracefully so the job never needs to restart from zero.

---

# Solution

In this nightly billing job scenario, I would not update all 1 million records in a single transaction.  
If the system crashes in between, the entire progress may be lost and the whole process would need to restart from the beginning. This would waste time and also put unnecessary load on the database.

A better and more practical approach would be to process the records in smaller batches, for example `x` number of records at a time.

After processing each batch successfully, the transaction should be committed immediately.  
This makes the transactions smaller, safer, and easier to recover in case of failure.

I would also maintain a small checkpoint table that stores the ID of the last successfully processed record.

Because of this, if the job crashes after processing some records, the next execution can continue from the last saved checkpoint instead of starting again from zero.

---

# Workflow of the Billing Job

The billing job would follow these steps:

1. Read the last processed ID from the checkpoint table.
2. Process the next batch of records.
3. Commit the transaction.
4. Update the checkpoint table.
5. Continue until all records are processed.

---

# Example SQL Script with batch of x records..

```sql
START TRANSACTION;

UPDATE billing_records
SET billing_status = 'PROCESSING DONE'
WHERE id > x
ORDER BY id
LIMIT x;

COMMIT;
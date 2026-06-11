## Fastest Way to Rollback After DELETE

The fastest way to undo a `DELETE` operation is by using the `ROLLBACK` command. This works only if the transaction has not been committed.

```sql
START TRANSACTION;

DELETE FROM employees
WHERE id = 10;

ROLLBACK;
```

When `ROLLBACK` is executed, the database discards the uncommitted changes and restores the previous state using its transaction logs. Since the data has not been permanently saved, the recovery process is very quick.

### Why is it Fast?

* No backup restoration is required.
* The database already has the old data stored in its transaction logs.
* It simply reverses the changes made by the current transaction.

### Limitation

If a `COMMIT` has already been executed, `ROLLBACK` cannot recover the deleted data.

### Slowest Recovery Method

After a committed delete, recovery usually involves restoring data from a backup. This process is slower because the backup must be located, restored, and the required records must be extracted and inserted back into the database.

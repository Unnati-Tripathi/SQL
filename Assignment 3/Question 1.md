# How Does a Database Know About the Last Commit?

Modern database systems maintain a special log file to keep track of all transactions. This log is known by different names depending on the database:

* **PostgreSQL** → Write Ahead Log (WAL)
* **MySQL** → Redo Log
* **Oracle** → Redo Log

The purpose of these logs is to record transaction activity so that the database can recover correctly after failures.

## Transaction Tracking

Whenever a transaction starts, the database assigns it a unique **Transaction ID (TXN ID)**.

Example:

| TXN ID | Operation          | Status      |
| ------ | ------------------ | ----------- |
| 101    | INSERT INTO users  | COMMITTED   |
| 102    | DELETE FROM orders | ROLLED BACK |
| 103    | UPDATE salary      | COMMITTED   |

The database uses these records to determine which transactions were successfully completed and which were not.

## Why Are Transaction Logs Important?

Transaction logs become extremely important during:

* System crashes
* Database recovery
* Rollbacks
* Replication

Consider a situation where an `UPDATE` statement executes, but the server crashes before the transaction is committed.

When the database restarts, it checks the transaction log:

* If the transaction was committed, the changes are restored.
* If the transaction was not committed, the changes are discarded.

This behavior helps maintain the ACID properties of a database:

* **Atomicity**
* **Consistency**
* **Isolation**
* **Durability**

---

# Understanding REDO Operations

The term **REDO** refers to reapplying committed changes during database recovery.

In simple words, if a transaction was successfully committed before a crash, the database ensures that its changes are applied again if necessary.

## Example

Suppose the following query is executed:

```sql
UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

COMMIT;
```

### Internal Processing

Before modifying the actual table data, the database first writes the transaction information into its log file.

Example log entry:

```text
TXN 101
Operation: UPDATE accounts
Old Balance: 500
New Balance: 400
Status: COMMITTED
```

This follows the Write Ahead Logging principle, where the log is updated before the actual data page.

---

## Crash Scenario

Assume the following sequence:

1. The transaction is written to the log.
2. The COMMIT is recorded successfully.
3. The system crashes before the updated data page is saved to disk.

At this point, the disk might still contain:

```text
Balance = 500
```

even though the transaction was committed.

---

## Recovery Process

When the database starts again, it scans the transaction log.

It finds:

```text
TXN 101 → COMMITTED
```

Since the transaction was committed, the database knows that the change must exist in the final state of the database.

Therefore, it applies the update again:

```text
Balance = 400
```

This process is called **REDO**.

### Definition of REDO

REDO is the process of reapplying committed transactions from the transaction log during recovery to ensure that no committed data is lost.

## Conclusion

Transaction logs allow the database to remember the state of every transaction. During recovery, committed transactions are reapplied using REDO operations, while incomplete transactions are discarded. This mechanism guarantees data durability and helps maintain database consistency even after unexpected failures.

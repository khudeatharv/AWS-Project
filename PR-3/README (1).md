# Amazon RDS MySQL Backup and Recovery

## Objective

Create an Amazon RDS MySQL database and implement a backup and recovery scenario.

The following tasks were completed:

1. Create an Amazon RDS MySQL database.
2. Configure automated backups.
3. Insert sample records into the database.
4. Create a manual DB snapshot.
5. Simulate data loss by deleting a record.
6. Restore the database from the manual snapshot.
7. Verify that the deleted record was recovered.

---

## 1. Create the Amazon RDS MySQL Database

An Amazon RDS MySQL database instance was created and configured successfully.

The restored database instance is shown below. The database status is **Available**, the engine is **MySQL Community**, and the instance class is **db.t3.micro**.

![RDS MySQL restored database details](screenshots/01-restored-db-details.png)

---

## 2. Configure Automated Backups

Automated backups were enabled while configuring the RDS MySQL database.

The RDS snapshot details below also show a **Backup retention period of 1 day**, confirming the backup configuration used for this practical.

![RDS snapshot and backup configuration details](screenshots/03-manual-snapshot-details.png)

---

## 3. Insert Sample Records

Sample records were inserted into the MySQL database table `students`.

Initial data:

| ID | Name  | Course |
|---:|-------|--------|
| 1 | Rahul | Cloud Computing |
| 2 | Amit | DevOps |
| 3 | Sneha | Data Analytics |

The MySQL query used to verify the original records was:

```sql
SELECT * FROM students;
```

![Original sample data](screenshots/06-original-sample-data.png)

---

## 4. Create a Manual DB Snapshot

A manual DB snapshot named **my-rds-mysql-data-snapshot** was created from the RDS MySQL database.

The snapshot details show:

- Snapshot type: **manual**
- DB engine: **mysql**
- DB engine version: **8.4.9**
- Master username: **admin**
- Backup retention period: **1 day**
- Status: **Available**
- Storage: **20 GiB**

![Manual DB snapshot details](screenshots/03-manual-snapshot-details.png)

---

## 5. Simulate Data Loss

To simulate data loss, one record was deleted from the `students` table.

After the deletion, the query:

```sql
SELECT * FROM students;
```

returned only two records:

| ID | Name  | Course |
|---:|-------|--------|
| 1 | Rahul | Cloud Computing |
| 3 | Sneha | Data Analytics |

This confirms that the **Amit / DevOps** record was missing after the simulated data loss.

![Data loss simulated](screenshots/05-data-loss-simulated.png)

---

## 6. Restore the Database from the Snapshot

The database was restored from the manual snapshot **my-rds-mysql-data-snapshot** into a new RDS instance.

The AWS console displayed the message:

**Snapshot restored successfully**

The restored database instance was created as **my-rds-mysql-restored2** and its status is **Available**.

![Snapshot restored successfully](screenshots/02-snapshot-restore-success.png)

---

## 7. Verify the Recovered Records

After connecting to the restored MySQL database, the following command was executed:

```sql
SELECT * FROM students;
```

The result again contained all three original records:

| ID | Name  | Course |
|---:|-------|--------|
| 1 | Rahul | Cloud Computing |
| 2 | Amit | DevOps |
| 3 | Sneha | Data Analytics |

The deleted **Amit / DevOps** record was successfully recovered from the snapshot.

![Recovered records after restore](screenshots/04-data-after-recovery.png)

---

## 8. Verification Result

The backup and recovery process was successful.

### Before Data Loss

- Rahul - Cloud Computing
- Amit - DevOps
- Sneha - Data Analytics

### After Simulated Data Loss

- Rahul - Cloud Computing
- Sneha - Data Analytics

### After Snapshot Recovery

- Rahul - Cloud Computing
- Amit - DevOps
- Sneha - Data Analytics

Therefore, the manual RDS snapshot successfully restored the deleted data.

---

## Conclusion

Amazon RDS MySQL backup and recovery was successfully implemented. A manual DB snapshot was created, sample data was inserted, data loss was simulated, and the database was restored from the snapshot. The final verification confirmed that the deleted record was recovered successfully.


## Task: Exploring SQL Server Backup Types
## Part 1: Research Task 
Objective: Understand the different types of backup available in SQL Server.

1. 🗂️ Full Backup
What It Does: Backs up the entire database, including all data, objects, system tables, and part of the transaction log (to ensure consistency).

Use Case: Used as the base for all other backups. Essential for complete recovery.

Frequency: Typically done daily or weekly in production environments.

Restore Needs: You only need the most recent full backup and any subsequent log or differential backups.

2. 📄 Differential Backup
What It Does: Backs up only the changes made since the last full backup.

Use Case: Saves time and space by not duplicating unchanged data. Common between full backups (e.g., every few hours).

Restore Needs: Requires the last full backup + the latest differential backup.

Example: If a full backup was taken on Sunday, and a differential on Tuesday, it includes changes from Sunday to Tuesday.

3. 🧾 Transaction Log Backup
What It Does: Backs up the transaction log, capturing all changes made since the last log backup.

Use Case: Enables point-in-time recovery, vital for high-availability databases.

Restore Needs: Requires a full backup and all log backups in sequence up to the desired point.

Note: Only available if the database is in Full or Bulk-logged recovery model.

4. 📋 Copy-Only Backup
What It Does: Creates a backup without affecting the sequence of other backups (like log chains or differential bases).

Use Case: Useful for on-demand backups without disturbing the backup strategy (e.g., creating a temporary backup before an update).

Types: Can be full or transaction log copy-only backups.

Restore Needs: Treated independently; does not replace regular backups.

5. 📦 File / Filegroup Backup
What It Does: Backs up individual database files or filegroups.

Use Case: Useful for very large databases (VLDBs) to back up/restore only parts instead of the entire database.

Restore Needs: Can restore a file or group of files instead of the whole DB, combined with log backups for consistency.
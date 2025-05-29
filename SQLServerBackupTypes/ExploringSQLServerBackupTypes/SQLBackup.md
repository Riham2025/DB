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
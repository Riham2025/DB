## Task: Exploring SQL Server Backup Types
## Part 1: Research Task 
Objective: Understand the different types of backup available in SQL Server.

1. 🗂️ Full Backup
What It Does: Backs up the entire database, including all data, objects, system tables, and part of the transaction log (to ensure consistency).

Use Case: Used as the base for all other backups. Essential for complete recovery.

Frequency: Typically done daily or weekly in production environments.

Restore Needs: You only need the most recent full backup and any subsequent log or differential backups.
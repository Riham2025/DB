##Topics: 
1. UNION / UNION ALL 
2. DROP vs DELETE vs TRUNCATE 
3. Subqueries (exploratory task – they search and try it) 
4. Transaction & Batch Script (exploratory and guided) 
5. *Hands-on comparison with real effect on data 
Practice Scenario: Training & Job Application System 
Your institute is managing two main datasets: 
• Trainees: People who complete training at your institute. 
• Job Applicants: External applicants who apply directly to job posts. 
Your goal is to: 
• Compare the data of both groups. 
• Clean or restructure the database safely. 
• Explore more advanced SQL topics on your own (subqueries, transactions).
 ![](../image/a.PNG)

Part 1: UNION Practice 
1. List all unique people who either trained or applied for a job. 
o Show their full names and emails. 
o Use UNION (not UNION ALL) to avoid duplicates.
 ![](../image/s.PNG)

 2. Now use UNION ALL. What changes in the result? 
o Explain why one name appears twice. 
![](../image/d.PNG)

3. Find people who are in both tables. 
o You must use INTERSECT if supported, or simulate it using INNER JOIN on Email. 
 ![](../image/f.PNG)

 Part 2: DROP, DELETE, TRUNCATE Observation 
Let’s test destructive commands.

4. Try DELETE FROM Trainees WHERE Program = 'Outsystems'. 
o Check if the table structure still exists.
![](../image/g.PNG)

5.Try TRUNCATE TABLE Applicants. 
o What happens to the data? Can you roll it back? 
![](../image/h.PNG)

6. Try DROP TABLE Applicants. 
o What happens if you run a SELECT after that?
![](../image/i.PNG)

Part 3: Self-Discovery & Applied Exploration
In this section, you’ll independently research, experiment, and apply advanced SQL concepts. 
Follow the guided prompts below.
Part 3: Self-Discovery & Applied Exploration 
In this section, you’ll independently research, experiment, and apply advanced SQL concepts. 
Follow the guided prompts below. 
Subquery Exploration 
Goal: Understand what a subquery is and how it's used inside SQL commands.

 1. Research: 
	
1. What is a Subquery in SQL?
A subquery (or inner query) is an SQL query nested inside another SQL query.
It is used to get data needed by the main (outer) query.
It can be placed inside SELECT, FROM, WHERE, or other parts of an SQL statement.
It returns a result (one or more rows) that the outer query uses..


2. Where can we use subqueries? (e.g., in SELECT, WHERE, FROM)
In the WHERE clause
To filter rows based on the result of another query.
1. In the FROM clause
To treat the subquery result as a temporary table (called a derived table or inline view).
3. In the SELECT clause
To calculate or retrieve a single value per row.
4. In the HAVING clause
To filter groups based on a subquery condition.


1.  Task: 
o Write a query to find all trainees whose emails appear in the applicants table. 
o You must use a subquery inside a WHERE clause.
SELECT *
FROM Trainees
WHERE Email IN (SELECT Email FROM Applicants);

Extra Challenge: 
o Write a DML statement (like UPDATE or DELETE) that uses a subquery in the 
WHERE clause. 
o Example: Delete all applicants whose email matches someone in the trainees 
table.
DELETE FROM Applicants
WHERE Email IN (SELECT Email FROM Trainees);


Batch Script & Transactions
4. Research: 
o. What is a SQL transaction? 
A SQL Transaction (transaction in SQL) is a set of operations
(such as INSERT, UPDATE, DELETE)
executed as a single unit. Either all of them are executed effectively,
or all of them are issued if an error occurs.
o.How to write transaction blocks in your database tool (BEGIN TRANSACTION, 
COMMIT, ROLLBACK)?
BEGIN TRANSACTION;

-- Your DML operations here (INSERT, UPDATE, DELETE)
-- Example:
UPDATE Applicants
SET Source = 'Website'
WHERE ApplicantID = 102;

-- If all good, save the changes:
COMMIT;

-- If something goes wrong, you can cancel it:
-- ROLLBACK;


5. Task: 
o Write a script that: 
? Starts a transaction 
? Tries to insert two new applicants 
? The second insert should have a duplicate ApplicantID (to force failure) 
? Rollback the whole transaction if any error occurs
![](../image/k.PNG)

6. Add this logic: 
BEGIN TRANSACTION; 
INSERT INTO Applicants VALUES (104, 'Zahra Al Amri', 'zahra.a@example.com', 'Referral', '2025
05-10'); 
INSERT INTO Applicants VALUES (104, 'Error User', 'error@example.com', 'Website', '2025-05
11'); -- Duplicate ID 
COMMIT; -- Or use ROLLBACK if needed
![](../image/l.PNG)

 Research and summarize each of the ACID properties: 
o Atomicity 
o Consistency 
o Isolation 
o Durability

| Property            | Description                                                   | How This Script Demonstrates It                                         |
| ------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **A - Atomicity**   | All or nothing.                                               | If the second insert fails, the first insert is **also rolled back**.   |
| **C - Consistency** | Keeps DB in a valid state.                                    | Duplicate keys are not allowed, preserving **data integrity**.          |
| **I - Isolation**   | Intermediate changes are invisible to others.                 | During the transaction, no other users can see partial inserts.         |
| **D - Durability**  | Once committed, changes are saved even if the system crashes. | If both inserts had succeeded, the data would be **permanently saved**. |










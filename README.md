 # Gym Management System Using MySQL
Project Overview

Gym Management System Using MySQL is a database project designed to manage and analyze gym-related information, including members, membership plans, trainers, attendance, and payments.

The project uses a relational database structure with primary and foreign key relationships to maintain data accuracy and consistency. SQL queries are used for data retrieval, joins, filtering, aggregation, subqueries, and reporting to generate meaningful insights into gym operations.

 # Project Objectives
 Manage gym member and trainer information

Store and analyze membership plan details

Track member attendance and registrations

Analyze payment transactions and gym revenue

Understand relationships between members, trainers, memberships, and payments

Practice SQL joins, aggregate functions, and subqueries

Create SQL views for analytical reporting

 # Database Tables

The project includes the following tables, depending on the database structure:
### 1. Member

Stores gym member details, including name, gender, age, contact number, joining date, membership plan, and assigned trainer. Each member has a unique Member_ID.

### 2. Membership
Stores information about gym membership plans, including plan name, duration, and membership fees. Each membership plan has a unique Membership_ID as the primary key.

### 3.  Trainer
Stores information about gym trainers, including their names, specializations, contact details, and salaries. Each trainer has a unique Trainer_ID.

### 4.  Attendance
Records gym attendance for registered members, including attendance date, check-in time, and check-out time. Each attendance record has a unique Attendance_ID.

### 5. . Payment

Stores payment transactions made by gym members, including payment amount, date, payment mode, and payment status. Each payment has a unique Payment_ID.
## ER DIAGRAM 
## SQL joins
The project demonstrates different types of joins:
### 1. INNER JOIN – Members with Membership Plans

Displays member details along with their membership plan and fee. Only members with a matching membership record are shown.
``` SELECT
    m.Member_ID,
    m.Member_Name,
    ms.Plan_Name,
    ms.Membership_Fee
FROM Member m
INNER JOIN Membership ms
    ON m.Membership_ID = ms.Membership_ID;
 ```
### 2. LEFT JOIN – All Members and Their Payments

Displays all members, including those who have not made any payment. Members without payments will show NULL in the payment columns.
SELECT
    m.Member_ID,
    m.Member_Name,
    p.Amount,
    p.Payment_Date,
    p.Payment_Status
FROM Member m
LEFT JOIN Payment p
    ON m.Member_ID = p.Member_ID;

### 3. RIGHT JOIN – Trainers and Assigned Members

Displays all trainers, including trainers who do not currently have any assigned members.

```SELECT
    t.Trainer_ID,
    t.Trainer_Name,
    m.Member_ID,
    m.Member_Name
FROM Member m
RIGHT JOIN Trainer t
    ON m.Trainer_ID = t.Trainer_ID;
```

### 4. FULL OUTER JOIN Concept – All Members and Payments

MySQL does not directly support FULL OUTER JOIN. We can combine LEFT JOIN and RIGHT JOIN using UNION to show all members and payment records, including unmatched records.

```SELECT
    m.Member_ID,
    m.Member_Name,
    p.Payment_ID,
    p.Amount
FROM Member m
LEFT JOIN Payment p
    ON m.Member_ID = p.Member_ID

UNION

SELECT
    m.Member_ID,
    m.Member_Name,
    p.Payment_ID,
    p.Amount
FROM Member m
RIGHT JOIN Payment p
    ON m.Member_ID = p.Member_ID;
```
### 5. MULTIPLE TABLE JOIN – Complete Member Details

Combines the Member, Membership, Trainer, and Payment tables to display member information, their membership plan, assigned trainer, and payment details.

```SELECT
    m.Member_ID,
    m.Member_Name,
    ms.Plan_Name,
    t.Trainer_Name,
    p.Amount,
    p.Payment_Status
FROM Member m
INNER JOIN Membership ms
    ON m.Membership_ID = ms.Membership_ID
LEFT JOIN Trainer t
    ON m.Trainer_ID = t.Trainer_ID
LEFT JOIN Payment p
    ON m.Member_ID = p.Member_ID;
```
## SQL Subqueries Used in the Project

### 1. Members Who Made Payments Above Average

Finds members whose payment amount is greater than the average payment amount.

```sql
SELECT
    Member_ID,
    Member_Name
FROM Member
WHERE Member_ID IN (
    SELECT Member_ID
    FROM Payment
    WHERE Amount > (
        SELECT AVG(Amount)
        FROM Payment
    )
);
```

### 2. Most Expensive Membership Plan

Displays the membership plan or plans with the highest membership fee.

```sql
SELECT
    Plan_Name,
    Membership_Fee
FROM Membership
WHERE Membership_Fee = (
    SELECT MAX(Membership_Fee)
    FROM Membership
);
```

### 3. Members Who Have Completed Their Payments

Displays members who have at least one successful payment.

```sql
SELECT
    Member_ID,
    Member_Name
FROM Member
WHERE Member_ID IN (
    SELECT Member_ID
    FROM Payment
    WHERE Payment_Status = 'Successful'
);
```

### 4. Member with the Highest Attendance

Finds the member or members who have recorded the highest number of attendance entries.

```sql
SELECT
    Member_ID,
    Member_Name
FROM Member
WHERE Member_ID IN (
    SELECT Member_ID
    FROM Attendance
    GROUP BY Member_ID
    HAVING COUNT(*) = (
        SELECT MAX(Attendance_Count)
        FROM (
            SELECT COUNT(*) AS Attendance_Count
            FROM Attendance
            GROUP BY Member_ID
        ) AS Attendance_Summary
    )
);
```

### 5. Trainers with the Most Assigned Members

Identifies the trainer or trainers who have the highest number of assigned members.

```sql
SELECT
    Trainer_ID,
    Trainer_Name
FROM Trainer
WHERE Trainer_ID IN (
    SELECT Trainer_ID
    FROM Member
    WHERE Trainer_ID IS NOT NULL
    GROUP BY Trainer_ID
    HAVING COUNT(*) = (
        SELECT MAX(Member_Count)
        FROM (
            SELECT COUNT(*) AS Member_Count
            FROM Member
            WHERE Trainer_ID IS NOT NULL
            GROUP BY Trainer_ID
        ) AS Trainer_Summary
    )
);
```
## 📁 Project Files

### Gym-Management-System-MySQL

### Gym Management System.sql

Contains SQL queries for database creation, table creation, data insertion, joins, subqueries, and views used in the Gym Management System.

- [SQL File](./Gym%20Management%20System.sql)

### Gym Management System.pptx

Contains the project presentation, database structure, table descriptions, SQL queries, and outputs.

- [SQL PPT](./Gym%20Management%20System.pptx)
### Key Insights

- Identified members with above-average payment amounts.
- Found the most expensive membership plan.
- Retrieved members with successful payments.
- Identified members with the highest attendance.
- Determined which trainers have the most assigned members.

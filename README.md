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
# 1. INNER JOIN – Members with Membership Plans

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


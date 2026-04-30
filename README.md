# Student-enrolment-and-Revenue-Analysis-System-SQL-project-
sql project

Student Enrollment & Revenue Analytics System (SQL Project)

 Overview

This project is a SQL-based data analysis system designed to manage and analyze operations of a coaching institute. It integrates multiple datasets such as students, enrollments, courses, batches, payments, and attendance to generate meaningful business insights.

The goal of this project is to simulate a real-world database system and perform analytical queries using SQL.

Database Schema

The project consists of the following tables:

Students – student details (name, city, etc.)
Enrollments – student-course/batch mapping
Batches – batch information
Course – course details and pricing
Payments – transaction data
Attendance – student attendance records
Teachers – instructor details

Relationships
Students → Enrollments → Batches → Course
Enrollments → Payments
Students → Attendance
Course → Teachers

 
 Tech Stack
Database: MySQL
Language: SQL
Tools: MySQL Workbench / any SQL client
 Key Features & Analysis

1.Revenue Analysis
Total revenue generated
Course-wise revenue
Teacher-wise revenue contribution
Monthly revenue trends

2. Student Insights
City-wise student distribution
Students enrolled in multiple batches
Active students in recent periods

3.Financial Metrics
Outstanding payments per enrollment
ARPU (Average Revenue Per User)
Payment mode distribution
On-time payment rate

4. Academic Insights
Attendance rate calculation
Class size per batch
Most popular courses

 Sample Queries


Outstanding Amount per Enrollment
SELECT 
    e.enroll_id,
    c.course_name,
    c.price,
    IFNULL(SUM(p.amount), 0) AS total_paid,
    c.price - IFNULL(SUM(p.amount), 0) AS outstanding
FROM enrollments e
JOIN batches b ON e.batch_id = b.batch_id
JOIN course c ON b.course_id = c.course_id
LEFT JOIN payments p ON e.enroll_id = p.enrollment_id
GROUP BY e.enroll_id, c.course_name, c.price;

 Top 3 Courses by Revenue
SELECT 
    c.course_name,
    SUM(p.amount) AS revenue
FROM payments p
JOIN enrollments e ON p.enrollment_id = e.enroll_id
JOIN batches b ON e.batch_id = b.batch_id
JOIN course c ON b.course_id = c.course_id
GROUP BY c.course_name
ORDER BY revenue DESC
LIMIT 3;
 
 Attendance Rate
SELECT 
    SUM(CASE WHEN status = 'Present' THEN 1 ELSE 0 END) * 100.0 / COUNT(*) AS attendance_rate
FROM attendance;

Challenges Faced
Handling inconsistent column naming across tables (e.g., enroll_id vs enrollment_id)
Debugging JOIN errors and missing data
Managing data import issues from Excel to MySQL
Ensuring data consistency across relationships

Key Learnings
Strong understanding of relational database design
Mastery of JOIN operations (INNER, LEFT JOIN)
Use of aggregate functions and GROUP BY
Writing real-world business queries
Debugging SQL errors effectively

How to Run This Project
Clone the repository
Open MySQL Workbench

Create a new database:

CREATE DATABASE sql_project;
USE sql_project;
Import tables using provided SQL/CSV files
Run the queries from the project

 Future Improvements
Add dashboard visualization (Power BI / Tableau)
Normalize schema for better consistency
Add stored procedures and views
Optimize queries for performance
 Author

Nirosha Jayasundara
SQL & Data Analytics Enthusiast

 If you like this project

Give it a star  and feel free to fork or contribute!

#  Complete Database Course

> A comprehensive, beginner-to-advanced guide to learning Databases — from fundamentals to real-world applications.

---

##  Table of Contents

- [About This Course](#about-this-course)
- [Who Is This For?](#who-is-this-for)
- [Prerequisites](#prerequisites)
- [Course Roadmap](#course-roadmap)
- [Module 1 — Introduction to Databases](#module-1--introduction-to-databases)
- [Module 2 — Relational Database & SQL](#module-2--relational-database--sql)
- [Module 3 — Advanced SQL](#module-3--advanced-sql)
- [Module 4 — Database Design & Normalization](#module-4--database-design--normalization)
- [Module 5 — Transactions & Concurrency](#module-5--transactions--concurrency)
- [Module 6 — Indexing & Query Optimization](#module-6--indexing--query-optimization)
- [Module 7 — NoSQL Databases](#module-7--nosql-databases)
- [Module 8 — Database Administration (DBA)](#module-8--database-administration-dba)
- [Module 9 — Cloud Databases](#module-9--cloud-databases)
- [Module 10 — Real-World Projects](#module-10--real-world-projects)
- [Free Resources](#free-resources)
- [Recommended Books](#recommended-books)
- [YouTube Channels](#youtube-channels)
- [Practice Platforms](#practice-platforms)
- [Certifications](#certifications)
- [Contributing](#contributing)

---

##  About This Course

This is a **free, open-source, self-paced** complete database course that covers everything you need to go from a complete beginner to a confident database developer and administrator. You will learn SQL, NoSQL, database design, optimization, transactions, cloud databases, and more.

---

## 👤 Who Is This For?

| Level | Description |
|-------|-------------|
| 🟢 Beginners | No prior database knowledge required |
| 🟡 Intermediate | Developers who know some SQL but want depth |
| 🔴 Advanced | Engineers who want optimization & DBA skills |

---

## ✅ Prerequisites

- Basic understanding of computers
- Familiarity with any programming language (Python/Java/JS) is a plus
- A laptop/PC with internet connection

---

## 🗺️ Course Roadmap

```
Databases Fundamentals
        ↓
   SQL Basics
        ↓
  Advanced SQL
        ↓
Database Design & ERD
        ↓
Normalization (1NF → BCNF)
        ↓
Transactions & ACID
        ↓
Indexing & Optimization
        ↓
   NoSQL (MongoDB, Redis)
        ↓
Database Administration
        ↓
  Cloud Databases (AWS RDS, Firebase)
        ↓
  Real-World Projects 🚀
```

---

##  Module 1 — Introduction to Databases

### 🎯 Topics Covered
- What is a Database?
- Database vs File System
- Types of Databases (Relational, NoSQL, NewSQL, In-Memory)
- DBMS vs RDBMS
- Popular Databases Overview (MySQL, PostgreSQL, MongoDB, SQLite, Oracle)
- How databases are used in real-world applications

###  Key Concepts
- **DBMS** — Database Management System
- **Schema** — Blueprint/structure of a database
- **Instance** — The actual data at a point in time
- **Data Independence** — Physical vs Logical

###  Tasks
- [ ] Install MySQL / PostgreSQL on your machine
- [ ] Install DB GUI tools: DBeaver or TablePlus
- [ ] Create your first database

---

##  Module 2 — Relational Database & SQL

### 🎯 Topics Covered
- What is a Relational Database?
- Tables, Rows, Columns, Keys
- Primary Key, Foreign Key, Unique Key, Composite Key
- Basic SQL Commands

### 🔑 SQL Commands

```sql
-- Create Database
CREATE DATABASE school;

-- Create Table
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(150) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert Data
INSERT INTO students (name, age, email)
VALUES ('Ali Khan', 20, 'ali@example.com');

-- Read Data
SELECT * FROM students;
SELECT name, age FROM students WHERE age > 18;

-- Update Data
UPDATE students SET age = 21 WHERE id = 1;

-- Delete Data
DELETE FROM students WHERE id = 1;
```

### 📝 Tasks
- [ ] Create a `school` database with `students`, `teachers`, and `courses` tables
- [ ] Insert 10 rows of data into each table
- [ ] Practice SELECT, INSERT, UPDATE, DELETE

---

## 📦 Module 3 — Advanced SQL

### 🎯 Topics Covered
- **Filtering** — WHERE, AND, OR, NOT, BETWEEN, LIKE, IN
- **Sorting** — ORDER BY, ASC, DESC
- **Aggregate Functions** — COUNT, SUM, AVG, MIN, MAX
- **Grouping** — GROUP BY, HAVING
- **Joins** — INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN, SELF JOIN, CROSS JOIN
- **Subqueries** — Scalar, Correlated, Nested
- **Views** — Creating and using views
- **Stored Procedures & Functions**
- **Triggers**
- **Window Functions** — ROW_NUMBER, RANK, DENSE_RANK, PARTITION BY

### 🔑 Key Examples

```sql
-- INNER JOIN
SELECT s.name, c.course_name
FROM students s
INNER JOIN enrollments e ON s.id = e.student_id
INNER JOIN courses c ON e.course_id = c.id;

-- GROUP BY with HAVING
SELECT department, COUNT(*) AS total_students
FROM students
GROUP BY department
HAVING COUNT(*) > 5;

-- Window Function
SELECT name, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_in_dept
FROM employees;

-- Stored Procedure
DELIMITER //
CREATE PROCEDURE GetStudentsByAge(IN min_age INT)
BEGIN
    SELECT * FROM students WHERE age >= min_age;
END //
DELIMITER ;

-- Trigger
CREATE TRIGGER before_student_insert
BEFORE INSERT ON students
FOR EACH ROW
SET NEW.created_at = NOW();
```

### 📝 Tasks
- [ ] Write 5 JOIN queries on your school database
- [ ] Use GROUP BY and HAVING to find departments with most students
- [ ] Create a VIEW for active students
- [ ] Build a stored procedure to enroll a student in a course

---

## 📦 Module 4 — Database Design & Normalization

### 🎯 Topics Covered
- Entity-Relationship (ER) Diagrams
- Entities, Attributes, Relationships
- Cardinality — One-to-One, One-to-Many, Many-to-Many
- Converting ER Diagram to Tables
- Normalization
  - **1NF** — First Normal Form (Atomic Values)
  - **2NF** — Second Normal Form (Eliminate Partial Dependency)
  - **3NF** — Third Normal Form (Eliminate Transitive Dependency)
  - **BCNF** — Boyce-Codd Normal Form
- Denormalization — When and Why

### 🔑 Normalization Example

```
UNNORMALIZED TABLE:
StudentID | StudentName | Courses        | Instructor
----------|-------------|----------------|----------
1         | Ali         | Math, Physics  | Dr. Ahmed
2         | Sara        | Math           | Dr. Ahmed

AFTER 1NF:
StudentID | StudentName | Course  | Instructor
----------|-------------|---------|----------
1         | Ali         | Math    | Dr. Ahmed
1         | Ali         | Physics | Dr. Ahmed
2         | Sara        | Math    | Dr. Ahmed

AFTER 2NF & 3NF:
→ Students(StudentID, StudentName)
→ Courses(CourseID, CourseName, InstructorID)
→ Instructors(InstructorID, InstructorName)
→ Enrollments(StudentID, CourseID)
```

###  Tasks
- [ ] Draw an ER Diagram for an E-Commerce system (Users, Products, Orders, Reviews)
- [ ] Convert the ER Diagram to normalized tables up to 3NF
- [ ] Use draw.io or dbdiagram.io to design your schema

---

##  Module 5 — Transactions & Concurrency

###  Topics Covered
- What is a Transaction?
- **ACID Properties**
  - **Atomicity** — All or nothing
  - **Consistency** — Data remains valid
  - **Isolation** — Transactions don't interfere
  - **Durability** — Committed data persists
- Transaction Commands — BEGIN, COMMIT, ROLLBACK, SAVEPOINT
- Isolation Levels — READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE
- Concurrency Problems — Dirty Read, Non-Repeatable Read, Phantom Read
- Locks — Shared Lock, Exclusive Lock, Deadlocks

### 🔑 Transaction Example

```sql
START TRANSACTION;

UPDATE accounts SET balance = balance - 5000 WHERE id = 1;
UPDATE accounts SET balance = balance + 5000 WHERE id = 2;

-- If everything OK
COMMIT;

-- If something goes wrong
ROLLBACK;
```

### 📝 Tasks
- [ ] Simulate a bank transfer with transactions
- [ ] Intentionally cause a ROLLBACK on error
- [ ] Test different isolation levels

---

## 📦 Module 6 — Indexing & Query Optimization

### 🎯 Topics Covered
- What is an Index and why it matters
- Types of Indexes — B-Tree, Hash, Full-Text, Composite
- Creating and Dropping Indexes
- **EXPLAIN / EXPLAIN ANALYZE** — Reading query execution plans
- Query Optimization Tips
  - Avoid SELECT *
  - Use indexes wisely
  - Avoid functions on indexed columns
  - Use pagination (LIMIT / OFFSET)
- Partitioning — Horizontal vs Vertical

### 🔑 Index Examples

```sql
-- Create Index
CREATE INDEX idx_students_name ON students(name);

-- Composite Index
CREATE INDEX idx_name_age ON students(name, age);

-- Full Text Index
CREATE FULLTEXT INDEX idx_description ON products(description);

-- Check Query Plan
EXPLAIN SELECT * FROM students WHERE name = 'Ali';

-- Drop Index
DROP INDEX idx_students_name ON students;
```

### 📝 Tasks
- [ ] Add indexes to your school database
- [ ] Use EXPLAIN to compare query performance before and after indexing
- [ ] Optimize a slow JOIN query

---

## 📦 Module 7 — NoSQL Databases

### 🎯 Topics Covered
- What is NoSQL and when to use it
- Types of NoSQL Databases
  - **Document** — MongoDB, CouchDB
  - **Key-Value** — Redis, DynamoDB
  - **Column-Family** — Cassandra, HBase
  - **Graph** — Neo4j
- SQL vs NoSQL Comparison
- **MongoDB** — CRUD Operations, Schema Design, Aggregation Pipeline, Indexes
- **Redis** — Caching, Pub/Sub, Data Structures

### 🔑 MongoDB Examples

```javascript
// Insert
db.students.insertOne({ name: "Ali", age: 20, courses: ["Math", "Physics"] });

// Find
db.students.find({ age: { $gt: 18 } });

// Update
db.students.updateOne({ name: "Ali" }, { $set: { age: 21 } });

// Delete
db.students.deleteOne({ name: "Ali" });

// Aggregation Pipeline
db.orders.aggregate([
  { $match: { status: "completed" } },
  { $group: { _id: "$customer_id", total: { $sum: "$amount" } } },
  { $sort: { total: -1 } }
]);
```

### 📝 Tasks
- [ ] Install MongoDB locally or use MongoDB Atlas (free cloud)
- [ ] Build a blog system with MongoDB (Posts, Comments, Users)
- [ ] Set up Redis for caching frequently-accessed data

---

## 📦 Module 8 — Database Administration (DBA)

### 🎯 Topics Covered
- DBA Roles and Responsibilities
- User Management & Privileges
- Backup & Recovery — mysqldump, pg_dump
- Replication — Master-Slave, Master-Master
- High Availability & Failover
- Database Monitoring & Logging
- Performance Tuning

### 🔑 Key Commands

```sql
-- Create User
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';

-- Grant Privileges
GRANT ALL PRIVILEGES ON school.* TO 'newuser'@'localhost';

-- Revoke Privileges
REVOKE DELETE ON school.* FROM 'newuser'@'localhost';

-- Show Users
SELECT user, host FROM mysql.user;
```

```bash
# Backup Database (MySQL)
mysqldump -u root -p school > school_backup.sql

# Restore Database
mysql -u root -p school < school_backup.sql

# Backup (PostgreSQL)
pg_dump -U postgres school > school_backup.sql
```

### 📝 Tasks
- [ ] Create read-only and read-write users for your database
- [ ] Set up daily backup scripts
- [ ] Configure basic MySQL/PostgreSQL replication

---

## 📦 Module 9 — Cloud Databases

### 🎯 Topics Covered
- Cloud Database Overview
- **AWS RDS** — MySQL, PostgreSQL on AWS
- **Google Cloud SQL** — Managed relational DB
- **Firebase Firestore** — Real-time NoSQL DB
- **PlanetScale** — Serverless MySQL
- **Supabase** — Open-source Firebase alternative
- **MongoDB Atlas** — Cloud-hosted MongoDB
- Connecting Cloud DB with Applications (Node.js, Python)

### 🔑 Connecting Node.js to Cloud DB

```javascript
// MySQL (AWS RDS)
const mysql = require('mysql2');
const connection = mysql.createConnection({
  host: 'your-rds-endpoint.amazonaws.com',
  user: 'admin',
  password: 'your_password',
  database: 'school'
});

// MongoDB Atlas
const { MongoClient } = require('mongodb');
const client = new MongoClient('mongodb+srv://user:pass@cluster.mongodb.net/');
await client.connect();
```

### 📝 Tasks
- [ ] Create a free-tier AWS RDS MySQL instance
- [ ] Connect your Node.js/Python app to the cloud database
- [ ] Try Firebase Firestore with real-time listeners

---

## 📦 Module 10 — Real-World Projects

###  Project 1 — Student Management System
- Tech: MySQL + Python/Node.js
- Features: CRUD for students, courses, enrollment
- Apply: Joins, Stored Procedures, Transactions

###  Project 2 — E-Commerce Database
- Tech: PostgreSQL + any backend
- Features: Products, Orders, Inventory, Reviews
- Apply: Normalization, Indexing, Views

###  Project 3 — Social Media Backend
- Tech: MongoDB + Redis
- Features: Users, Posts, Likes, Comments, Feed
- Apply: NoSQL schema design, Caching with Redis

### 🚀 Project 4 — Banking System
- Tech: MySQL
- Features: Accounts, Transfers, Transaction History
- Apply: ACID Transactions, Triggers, Audit Logs

### 🚀 Project 5 — Analytics Dashboard
- Tech: PostgreSQL + Window Functions
- Features: Sales reports, KPIs, Aggregated stats
- Apply: Advanced SQL, Query optimization

---

## 📚 Free Resources

### 📖 Official Documentation
| Database | Documentation Link |
|----------|-------------------|
| MySQL | https://dev.mysql.com/doc/ |
| PostgreSQL | https://www.postgresql.org/docs/ |
| MongoDB | https://www.mongodb.com/docs/ |
| Redis | https://redis.io/docs/ |
| SQLite | https://www.sqlite.org/docs.html |

### 🎓 Free Online Courses
| Platform | Course | Link |
|----------|--------|------|
| freeCodeCamp | Relational Database (300hrs) | https://www.freecodecamp.org/learn/relational-database/ |
| Khan Academy | SQL Intro | https://www.khanacademy.org/computing/computer-programming/sql |
| W3Schools | SQL Tutorial | https://www.w3schools.com/sql/ |
| SQLZoo | Interactive SQL | https://sqlzoo.net/ |
| Mode Analytics | SQL Tutorial | https://mode.com/sql-tutorial/ |
| The Odin Project | Databases | https://www.theodinproject.com/ |
| CS50 (Harvard) | CS50's SQL | https://cs50.harvard.edu/sql/ |

### 🛠️ Tools & Software (Free)
| Tool | Purpose | Download |
|------|---------|---------|
| MySQL Community | RDBMS Server | https://dev.mysql.com/downloads/ |
| PostgreSQL | RDBMS Server | https://www.postgresql.org/download/ |
| MongoDB Community | NoSQL Server | https://www.mongodb.com/try/download/community |
| DBeaver | Universal DB GUI | https://dbeaver.io/download/ |
| TablePlus | DB GUI (Mac/Win) | https://tableplus.com/ |
| draw.io | ER Diagram Tool | https://app.diagrams.net/ |
| dbdiagram.io | Schema Design | https://dbdiagram.io/ |
| Redis | In-Memory DB | https://redis.io/download/ |
| Postman | API Testing | https://www.postman.com/ |
| MongoDB Compass | MongoDB GUI | https://www.mongodb.com/products/compass |

---

## 📗 Recommended Books

| Book | Author | Level |
|------|--------|-------|
| Learning SQL | Alan Beaulieu | Beginner |
| SQL Cookbook | Anthony Molinaro | Intermediate |
| Database System Concepts | Silberschatz, Korth | Academic |
| Designing Data-Intensive Applications | Martin Kleppmann | Advanced |
| High Performance MySQL | Baron Schwartz | Advanced |
| MongoDB: The Definitive Guide | Kristina Chodorow | Intermediate |
| Seven Databases in Seven Weeks | Eric Redmond | Intermediate |
| The Art of SQL | Stéphane Faroult | Advanced |

---

## 📺 YouTube Channels

| Channel | What They Cover |
|---------|----------------|
| [freeCodeCamp](https://www.youtube.com/@freecodecamp) | Full DB courses, SQL tutorials |
| [Traversy Media](https://www.youtube.com/@TraversyMedia) | MySQL, MongoDB with projects |
| [Fireship](https://www.youtube.com/@Fireship) | Quick DB concept overviews |
| [Academind](https://www.youtube.com/@academind) | SQL & NoSQL deep dives |
| [Tech With Tim](https://www.youtube.com/@TechWithTim) | Python + Databases |
| [NetworkChuck](https://www.youtube.com/@NetworkChuck) | DB admin basics |
| [Programming with Mosh](https://www.youtube.com/@programmingwithmosh) | MySQL complete course |
| [Bro Code](https://www.youtube.com/@BroCodez) | Beginner-friendly SQL |

---

## 💻 Practice Platforms

| Platform | Focus | Link |
|----------|-------|------|
| LeetCode | SQL problems (Easy→Hard) | https://leetcode.com/problemset/database/ |
| HackerRank | SQL practice challenges | https://www.hackerrank.com/domains/sql |
| SQLZoo | Interactive SQL exercises | https://sqlzoo.net/ |
| StrataScratch | Real company SQL questions | https://www.stratascratch.com/ |
| Mode SQL Tutorial | Business SQL practice | https://mode.com/sql-tutorial/ |
| DB Fiddle | Test SQL in browser | https://www.db-fiddle.com/ |
| SQLiteOnline | Run SQL in browser | https://sqliteonline.com/ |

---

## 🏆 Certifications

| Certification | Provider | Level |
|---------------|----------|-------|
| Oracle Database SQL Certified Associate | Oracle | Beginner |
| MySQL Database Administrator | Oracle | Intermediate |
| Microsoft Azure Database Administrator | Microsoft | Intermediate |
| AWS Certified Database – Specialty | Amazon | Advanced |
| MongoDB Associate Developer | MongoDB | Intermediate |
| Google Professional Data Engineer | Google | Advanced |
| PostgreSQL Professional | PostgreSQL Association | Intermediate |

---

## 🗂️ Cheat Sheets

### SQL Quick Reference

```sql
-- DDL (Data Definition Language)
CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE

-- DML (Data Manipulation Language)
SELECT, INSERT, UPDATE, DELETE

-- DCL (Data Control Language)
GRANT, REVOKE

-- TCL (Transaction Control Language)
BEGIN, COMMIT, ROLLBACK, SAVEPOINT

-- Constraints
NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, DEFAULT

-- Joins
INNER JOIN   → Only matching rows from both tables
LEFT JOIN    → All rows from left + matching from right
RIGHT JOIN   → All rows from right + matching from left
FULL JOIN    → All rows from both tables
CROSS JOIN   → Cartesian product of both tables
SELF JOIN    → Table joined with itself

-- Aggregate Functions
COUNT(), SUM(), AVG(), MIN(), MAX(), GROUP_CONCAT()

-- String Functions
CONCAT(), SUBSTRING(), LENGTH(), UPPER(), LOWER(), TRIM(), REPLACE()

-- Date Functions
NOW(), CURDATE(), DATEDIFF(), DATE_FORMAT(), YEAR(), MONTH(), DAY()
```

---

## 🤝 Contributing

Contributions are welcome! If you'd like to add more resources, fix errors, or add new modules:

1. Fork this repository
2. Create a new branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Commit: `git commit -m "Add: your description"`
5. Push: `git push origin feature/your-feature`
6. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — free to use, share, and modify.

---

## ⭐ Star This Repo

If this course helped you, please **star ⭐ this repository** and share it with others who are learning databases!

---

<div align="center">

Made with ❤️ for every developer who wants to master Databases

**Happy Learning! 🚀**

</div>

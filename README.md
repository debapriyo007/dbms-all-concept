# SQL Code Repository 📂

This repository contains a collection of SQL scripts covering various database operations, including table creation, data manipulation, joins, aggregate functions, and advanced queries. It serves as a comprehensive reference for anyone looking to revise or enhance their SQL skills.

## 📌 What's Inside?

 🔹 **Table Creation & Data Insertion** – Scripts for defining tables and inserting records.  
 🔹 **Data Retrieval** – Queries using `SELECT`, `WHERE`, `ORDER BY`, and `LIMIT`.  
 🔹 **Aggregate Functions** – Using `AVG()`, `COUNT()`, `MAX()`, `MIN()` for data analysis.  
 🔹 **Joins (INNER, LEFT, RIGHT, FULL)** – Combining multiple tables efficiently.  
 🔹 **Foreign Keys & Relationships** – Defining and managing relational data.  
 🔹 **Table Modifications** – Adding, deleting, and updating table structures.  
 🔹 **Advanced Queries** – Subqueries, self joins, and optimization techniques.  
 🔹 **Indexing & Performance Optimization** – Enhancing query efficiency.  

## 🎯 Who is this for?

 ✅ **SQL Beginners & Learners.**  
 ✅ **Interview Preparation & Competitive Programming.**  
 ✅ **Anyone looking for quick SQL reference.**  


 


## ✅ Basic Part 1
```sql
SQL

CREATE TABLE MpBatch_2019( -- U can create more col for more info.
 rollNo INT PRIMARY KEY,
    name VARCHAR(50),
    marks INT NOT NULL,
    grade VARCHAR(3),
    vill VARCHAR(50)
);



INSERT INTO MpBatch_2019
(rollNo, name, marks, grade, vill)
VALUES
(1, "Ankit", 88, "A", "Panchla"),
(2, "Meera", 65, "C", "Dharmatala"),
(3, "Rakesh", 78, "B+", "Kharagpur"),
(4, "Sneha", 82, "A", "Kolkata"),
(5, "Amit", 91, "A+", "Jamtara"),
(6, "Payal", 85, "A", "Chinsurah"),
(7, "Vikas", 92, "A+", "Bolpur"),
(8, "Neha", 74, "B", "Tarakeshwar"),
(9, "Suman", 68, "B", "Santipur"),
(10, "Kabir", 89, "A", "Garia"),
(11, "Ishita", 77, "B+", "Durgapur"),
(12, "Debu", 98, "A+", "Santipur"),
(13, "Rahim", 99, "A+", "Bolpur");


SELECT * FROM MpBatch_2019;

SELECT * FROM MpBatch_2019
-- WHERE grade = "A++"
-- LIMIT 1;

SELECT * FROM MpBatch_2019 
ORDER BY marks DESC
LIMIT 3 ;


-- i want max/min/avg marks in the table.
SELECT AVG(marks) 
FROM MpBatch_2019;

SELECT vill, name, MAX(marks) AS maxMarks
FROM MpBatch_2019
GROUP BY vill, name
ORDER BY MAX(marks) DESC;


SELECT grade,COUNT(name)
FROM MpBatch_2019
GROUP BY grade
ORDER BY grade;


CREATE TABLE payment (
   customerID INT PRIMARY KEY,
   customer VARCHAR(50),
   mode VARCHAR(50),
   city VARCHAR(50)
);

INSERT INTO payment (customerID, customer, mode, city) VALUES 
(1, 'John Doe', 'CreditCard', 'New York'),
(2, 'Jane Smith', 'DebitCard', 'Los Angeles'),
(3, 'Alice Johnson', 'NetBanking', 'Chicago'),
(4, 'Robert Brown', 'CreditCard', 'Houston'),
(5, 'Emily Davis', 'DebitCard', 'Phoenix'),
(6, 'Michael Wilson', 'NetBanking', 'Philadelphia'),
(7, 'Sophia Martinez', 'CreditCard', 'San Antonio'),
(8, 'William Taylor', 'DebitCard', 'San Diego'),
(9, 'Isabella White', 'NetBanking', 'Dallas'),
(10, 'James Harris', 'CreditCard', 'San Jose');


SELECT * FROM payment;

SELECT mode, COUNT(mode) AS NoOfPayment
FROM payment
GROUP BY mode;


-- ++++++++++++++++++ HAVING CLAUSE +++++++++++++++++++++++
-- in some case where we are not using "WHERE" clause at that time
-- we are using "HAVING" Clause.

-- * Having Clause use in "GROUP BY" clause.

SELECT vill, COUNT(name)
FROM MpBatch_2019
GROUP BY vill
HAVING MAX(marks) > 80;

-- +++++ IT'S FOLLOW A PARTICULAR ORDER TO WRITE QUARY+++++++++

SELECT vill
FROM MpBatch_2019
WHERE grade = 'A'
GROUP BY vill
HAVING MAX(marks) > 87
ORDER BY vill ASC;



-- ++++++++++++++ TABLE RELATED QUARY+++++++++++++++++++++++++++++

-- 1> Update.
UPDATE MpBatch_2019
SET grade = 'O'
WHERE grade = 'A+';

-- i want each students number increasae by 1.
UPDATE MpBatch_2019
SET marks = marks + 1;


2> Delete..
DELETE FROM MpBatch_2019
WHERE marks < 75;

SELECT * FROM MpBatch_2019;
```


## ✅ Basic Part 2

```sql
SQL

-- ++++++++++++++ FK CONECPT +++++++++++++++++++++++++++++

CREATE TABLE dept(
  id INT PRIMARY KEY,
  name VARCHAR(50)
);

CREATE TABLE teacher(
  t_Id INT PRIMARY KEY,
  name VARCHAR(50),
  dept_Id INT,
  FOREIGN KEY (dept_Id) REFERENCES dept (id)
);

-- Insert data into the dept table
INSERT INTO dept (id, name) VALUES
(1, 'Computer Science'),
(2, 'Mathematics'),
(3, 'Physics'),
(4, 'Chemistry');

-- Insert data into the teacher table
INSERT INTO teacher (t_Id, name, dept_Id) VALUES
(101, 'Alice Johnson', 1),
(102, 'Bob Smith', 2),
(103, 'Carol Davis', 1),
(104, 'David Lee', 3),
(105, 'Emma Brown', 2),
(106, 'Frank Green', 4),
(107, 'Grace Miller', 1),
(108, 'Hannah White', 3),
(109, 'Ian Black', 4),
(110, 'Julia Carter', 2);


SELECT * FROM dept;
SELECT * FROM teacher;




-- +++++++++++++++ Cascading of FK+++++++++++++++++++++++++++++++++++++++++

-- Like if i want when i some thing update on delete in , parent table 
-- that should be reflect in child table also this is called "Cascading."


CREATE TABLE teacher(
  t_Id INT PRIMARY KEY,
  name VARCHAR(50),
  dept_Id INT,
  FOREIGN KEY (dept_Id) REFERENCES dept (id)
  ON DELETE CASCADE
  ON UPDATE CASCADE
);



-- +++++++++++++++ Table Related Queary +++++++++++++++++++++++++++++++++++++++++

-- 1) ADD COLUMN


CREATE TABLE myBooks(
  book_No INT PRIMARY KEY,
  bookName VARCHAR(50),
  bookAuthor VARCHAR(50)
  
);

INSERT INTO myBooks (book_No, bookName, bookAuthor)
VALUES
(1, 'Paradise Lost', 'Milton'),
(2, 'The Waste Land', 'Eliot'),
(3, 'Songs of Innocence', 'Blake'),
(4, 'The Prelude', 'Wordsworth'),
(5, 'Ode to a Nightingale', 'John Keats'),
(6, 'The Rape of the Lock', 'Pope'),
(7, 'Sonnets from the Portuguese', 'Browning'),
(8, 'The Canterbury Tales', 'Geoffrey'),
(9, 'Don Juan', 'Lord Byron'),
(10, 'Prometheus Unbound', 'Shelley');

SELECT * FROM myBooks;

-- now add a new col name as "Published"
ALTER TABLE myBooks
ADD COLUMN myPurchaseDate DATE NOT NULL DEFAULT '2015-10-27';

SELECT * FROM myBooks;


-- 2) DROP COLUMN
-- 3) RENAME TABLE
-- 4) CHANGE COLUMN -> changing col name , col data type.
-- 5) MODIFY COLUMN -> modify data type/ constraints

TRUNCATE TABLE myBooks;

SELECT * FROM myBooks;


-- +++++++++++++++ Home WOrk +++++++++++++++++++++++++++
-- Change column name book_No to book_id

ALTER TABLE myBooks
CHANGE book_No bookId INT;

SELECT * FROM myBooks;

-- drop a col myPurchaseDate
ALTER TABLE myBooks
DROP COLUMN myPurchaseDate;

SELECT * FROM myBooks;
```

## ✅ JOIN

```sql
SQL 

-- create
CREATE TABLE Student (
  stId INT PRIMARY KEY,
  name VARCHAR(50)
);

INSERT INTO Student
(stId, name) 
VALUES 
(101, 'Alice Johnson'),
(102, 'Bob Smith'),
(103, 'Charlie Brown'),
(104, 'Diana Green'),
(105, 'Edward Davis'),
(106, 'Fiona Clarke'),
(107, 'George Harris'),
(108, 'Hannah Adams'),
(109, 'Ian Miller'),
(110, 'Julia Turner');



-- print
SELECT * FROM Student;

CREATE TABLE Course(
  courseId INT PRIMARY KEY,
  course VARCHAR(50)
);


INSERT INTO Course
(courseId, course)
VALUES
(102, 'OPPS'),
(106, 'DBMS'),
(108, 'OS'),
(111, 'Network'),
(112, 'DSA');


-- +++++++++++++++++ Inner Join +++++++++++++++++++++

SELECT * FROM Course;

SELECT * 
FROM Student
INNER JOIN Course
ON Student.stId = Course.courseId;



-- Using Aliases.

-- SELECT * 
-- FROM Student as s
-- INNER JOIN Course as c
-- ON s.stId = c.courseId;



-- +++++++++++++++++ Left Join +++++++++++++++++++++

SELECT * 
FROM Student
LEFT JOIN Course
ON Student.stId = Course.courseId;


-- +++++++++++++++++ Right Join +++++++++++++++++++++

SELECT * 
FROM Student
RIGHT JOIN Course
ON Student.stId = Course.courseId;


-- +++++++++++++++++ Full Join +++++++++++++++++++++


SELECT * 
FROM Student
LEFT JOIN Course
ON Student.stId = Course.courseId

UNION

SELECT * 
FROM Student
RIGHT JOIN Course
ON Student.stId = Course.courseId;

-- +++++++++++++++++++++++++++++++++++++++

-- Some Trick Questions.[LEFT EXCLUSIVE JOIN..]

SELECT * 
FROM Student
LEFT JOIN Course
ON Student.stId = Course.courseId
WHERE Course.courseId IS NULL;


-- Some Trick Questions.[RIGHT EXCLUSIVE JOIN..]

SELECT * 
FROM Student
RIGHT JOIN Course
ON Student.stId = Course.courseId
WHERE Student.stId IS NULL;


-- 
SELECT * 
FROM Student
LEFT JOIN Course
ON Student.stId = Course.courseId
WHERE Course.courseId IS NULL

UNION

SELECT * 
FROM Student
RIGHT JOIN Course
ON Student.stId = Course.courseId
WHERE Student.stId IS NULL;


-- +++++++++++++++++ SELF JOIN ++++++++++++++++++++++++++++++

CREATE TABLE Employee(
  empId INT PRIMARY KEY, 
  name VARCHAR(50),
  managerId INT

);

INSERT INTO Employee
(empId, name, managerId)
VALUES
(101, 'Adam', 103),
(102, 'Bob', 104),
(103, 'Casey',NULL ),
(104, 'Donal', 103);

SELECT * FROM Employee;

SELECT a.name AS ManagerName , b.name
FROM Employee AS a 
JOIN Employee AS b
ON a.empId = b.managerId;

```




<div align="center">
  <p> 💡 Keep experimenting, keep learning, and enhance your SQL expertise! 🚀   </p>
  <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/>
  <img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram"/>
  <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/>
</div>

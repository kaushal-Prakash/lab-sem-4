
# MySQL and MongoDB Database Tasks

## 1. Create Employee Table and Basic Operations (CO3)

```sql
-- Create table
CREATE TABLE Employee (
    EMPNO INT,
    ENAME VARCHAR(50),
    JOB VARCHAR(50),
    MANAGER_NO INT,
    SAL DECIMAL(10,2),
    COMMISSION DECIMAL(10,2)
);

-- Create user and grant permissions
CREATE USER 'testuser'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON *.* TO 'testuser'@'localhost';

-- Insert 3 records
START TRANSACTION;

INSERT INTO Employee (EMPNO, ENAME, JOB, MANAGER_NO, SAL, COMMISSION) VALUES 
(101, 'Alice', 'Manager', NULL, 60000, 5000),
(102, 'Bob', 'Clerk', 101, 30000, NULL),
(103, 'Charlie', 'Analyst', 101, 40000, 1000);

-- Rollback changes
ROLLBACK;

-- Add constraints
ALTER TABLE Employee 
MODIFY EMPNO INT NOT NULL,
MODIFY ENAME VARCHAR(50) NOT NULL,
ADD PRIMARY KEY (EMPNO);

-- Insert NULL test (will fail due to NOT NULL)
INSERT INTO Employee (EMPNO, ENAME, JOB, MANAGER_NO, SAL, COMMISSION) 
VALUES (104, NULL, 'Clerk', 101, 25000, NULL);
```

---

## 2. Alter Table and Data Manipulation (CO3)

```sql
-- Create table
CREATE TABLE Employ (
    EMPNO INT PRIMARY KEY,
    ENAME VARCHAR(50),
    JOB VARCHAR(50),
    MGR INT,
    SAL DECIMAL(10,2)
);

-- Add column
ALTER TABLE Employ ADD COMMISSION DECIMAL(10,2);

-- Insert records
INSERT INTO Employ VALUES
(101, 'Alice', 'Manager', NULL, 60000, 5000),
(102, 'Bob', 'Clerk', 101, 30000, NULL),
(103, 'Charlie', 'Analyst', 101, 40000, 1000),
(104, 'David', 'Clerk', 102, 28000, NULL),
(105, 'Eve', 'Sales', 101, 32000, 2000);

-- Update job titles
UPDATE Employ SET JOB = 'Senior Clerk' WHERE JOB = 'Clerk';

-- Rename column
ALTER TABLE Employ CHANGE ENAME E_NAME VARCHAR(50);

-- Delete a record
DELETE FROM Employ WHERE EMPNO = 105;
```

---

## 3. Aggregate Functions and Grouping (CO3)

```sql
-- Create table
CREATE TABLE EmployeeAgg (
    E_id INT,
    E_name VARCHAR(50),
    Age INT,
    Salary DECIMAL(10,2)
);

-- Insert records
INSERT INTO EmployeeAgg VALUES
(1, 'Alice', 30, 60000),
(2, 'Bob', 25, 30000),
(3, 'Charlie', 32, 40000),
(4, 'David', 28, 28000),
(5, 'Eve', 27, 32000);

-- Count employees
SELECT COUNT(E_name) AS total_employees FROM EmployeeAgg;

-- Max age
SELECT MAX(Age) AS max_age FROM EmployeeAgg;

-- Min age
SELECT MIN(Age) AS min_age FROM EmployeeAgg;

-- Salaries ascending
SELECT E_name, Salary FROM EmployeeAgg ORDER BY Salary ASC;

-- Grouped salaries
SELECT Salary, COUNT(*) FROM EmployeeAgg GROUP BY Salary;
```

---

## 4. Row-Level Trigger (CO4)

```sql
-- Create table
CREATE TABLE CUSTOMERS (
    ID INT,
    NAME VARCHAR(50),
    AGE INT,
    ADDRESS VARCHAR(100),
    SALARY DECIMAL(10,2)
);

-- Trigger
DELIMITER //

CREATE TRIGGER salary_diff_trigger
BEFORE UPDATE ON CUSTOMERS
FOR EACH ROW
BEGIN
    DECLARE diff DECIMAL(10,2);
    SET diff = NEW.SALARY - OLD.SALARY;
    SELECT CONCAT('Salary changed by: ', diff);
END;
//

DELIMITER ;
```

---

## 5. Cursor for Employee Table (CO4)

```sql
-- Cursor example
DELIMITER //

CREATE PROCEDURE read_employees()
BEGIN
    DECLARE done INT DEFAULT FALSE;
    DECLARE eid INT;
    DECLARE ename VARCHAR(50);
    DECLARE emp_cursor CURSOR FOR SELECT E_id, E_name FROM EmployeeAgg;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    OPEN emp_cursor;

    read_loop: LOOP
        FETCH emp_cursor INTO eid, ename;
        IF done THEN
            LEAVE read_loop;
        END IF;
        SELECT CONCAT('ID: ', eid, ' Name: ', ename);
    END LOOP;

    CLOSE emp_cursor;
END;
//

DELIMITER ;

-- Call procedure
CALL read_employees();
```

---

## 6. MongoDB CRUD Operations (CO5)

```js
// Start MongoDB shell
mongosh

// Use database
use companyDB

// Create
db.employees.insertOne({ E_id: 1, E_name: "Alice", Age: 30, Salary: 60000 })

// Read
db.employees.find()

// Update
db.employees.updateOne({ E_id: 1 }, { $set: { Salary: 65000 } })

// Delete
db.employees.deleteOne({ E_id: 1 })
```

---

## 7. Project-Based Experiment (CO1, CO2, CO3)

**Project Title**: College Management System

- Tables: Students, Courses, Faculty, Results
- Features:
  - Use MySQL for relational data
  - Use MongoDB for logging
  - Include triggers, procedures, and joins
  - Build a web frontend using PHP/Node.js
  - Add analytics using GROUP BY, JOINs, etc.

---

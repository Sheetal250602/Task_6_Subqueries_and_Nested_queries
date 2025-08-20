# Task_6_Subqueries_and_Nested_queries
# Using Database 'COMPANY' and new tables 'EMPLOYEES' and 'DEPARTMENTS' for Subqueries and Nested Queries by using MySQL Workbench.

CREATE DATABASE COMPANY;
USE COMPANY;

CREATE TABLE Employees(
employee_id INT PRIMARY KEY NOT NULL,
first_name VARCHAR(50),
last_name VARCHAR(50),
category VARCHAR(50),
department VARCHAR(50),
salary FLOAT DEFAULT 20000,
joining_date DATE
);

INSERT INTO Employees VALUES
(1, 'John', 'Smith', 'Full Time', 'Engineering', 80000, '2021-01-29'),
(2, 'Alice', 'Johnson', 'Part Time', 'HR', 30000.00, '2021-05-12'),
(3, 'Bob', 'Brown', 'Full Time', 'Finance', 90000, '2021-01-29'),
(4, 'Carol', 'White', 'Contract', 'IT', 75000, '2021-01-01'),
(5, 'David', 'Green', 'Full Time', 'Engineering', 85000, '2022-01-13'),
(6, 'Emma', 'Blue', 'Part Time', 'Finance', 32000, '2023-01-01'),
(7, 'Frank', 'Black', 'Full Time', 'HR', 60000, '2024-05-05'),
(8, 'Grace', 'Grey', 'Full Time', 'Marketing', 70000, '2021-01-22'),
(9, 'Henry', 'Red', 'Contract', 'Sales', 95000, '2021-01-08'),
(10, 'Ivy', 'Yellow', 'Full Time', 'Marketing', 28000, '2025-01-03');

SELECT * FROM Employees;

# <img width="616" height="293" alt="image" src="https://github.com/user-attachments/assets/34dad3f6-0752-4047-8d3f-31d2564d75bd" />


CREATE TABLE Departments(
    dept_id INT PRIMARY KEY NOT NULL,
    department varchar(50)
);

INSERT INTO Departments VALUES
(101, 'Engineering'),
(102, 'HR'),
(103, 'Finance'),
(104, 'Marketing'),
(105, 'Engineering'),
(106, 'Sales'),
(107, 'HR');

SELECT * FROM Departments;

# <img width="237" height="245" alt="image" src="https://github.com/user-attachments/assets/7f1bb86e-2cdd-4a76-9524-870cbee291c0" />

# NESTED QUERY:
SELECT first_name
FROM employees
WHERE department IN (SELECT department FROM Departments WHERE department = 'Engineering');

# <img width="133" height="122" alt="image" src="https://github.com/user-attachments/assets/58673605-caa2-4872-8eb0-046452214abb" />

# SCALAR SUBQUERY: 
SELECT first_name, salary FROM Employees
WHERE salary > (SELECT AVG(salary) FROM Employees);

# <img width="235" height="233" alt="image" src="https://github.com/user-attachments/assets/7b6f79a1-3e95-456b-b30b-0b97486b79ad" />

# SINGLE ROW SUBQUERY::
SELECT * FROM Employees
WHERE department = (SELECT department FROM Departments WHERE dept_id = '106');

# <img width="640" height="109" alt="image" src="https://github.com/user-attachments/assets/e19d0d96-c2ca-475b-a367-2d083f5e8f0e" />

# MULTIPLE ROW SUBQUERY:
SELECT * FROM Employees 
WHERE department IN (SELECT department FROM Departments WHERE department = 'HR');

# <img width="657" height="132" alt="image" src="https://github.com/user-attachments/assets/1a982006-502a-4feb-8158-6083774f12a2" />

# MULTIPLE COLUMN SUBQUERY:
SELECT department, salary FROM Employees
WHERE (department, salary) IN (SELECT department, salary FROM Employees
WHERE salary > 60000);

# <img width="224" height="207" alt="image" src="https://github.com/user-attachments/assets/2e8b70b4-1438-4d0b-a14b-7d3bf5a87b4b" />

# Subquery with 'IN' Operator:
SELECT * FROM Employees
WHERE department IN (SELECT department FROM Departments);

# <img width="633" height="293" alt="image" src="https://github.com/user-attachments/assets/dcded6fd-5d36-4135-887b-3d201d3792bf" />

# Subquery with 'NOT IN' Operator:
SELECT * FROM Employees
WHERE department NOT IN (SELECT department FROM Departments);

# <img width="630" height="107" alt="image" src="https://github.com/user-attachments/assets/aa564c8d-1072-4444-bc73-23d95da97061" />

# Correlated Subquery:
SELECT first_name, last_name, salary FROM Employees e1
WHERE salary > (SELECT AVG(salary) from Employees e2 WHERE e2.department = e1.department);

# <img width="283" height="164" alt="image" src="https://github.com/user-attachments/assets/f01a4963-e558-494e-9cb6-d82fd446878d" />

# Subquery with 'EXISTS':
SELECT employee_id , first_name
FROM Employees
WHERE EXISTS (SELECT 101 FROM Departments WHERE Departments.department = Employees.department);

# <img width="232" height="279" alt="image" src="https://github.com/user-attachments/assets/4483b2c7-1293-41e6-9904-d3c98ac2e9ab" />

# Subquery with 'NOT EXISTS':
SELECT employee_id , first_name
FROM Employees
WHERE NOT EXISTS (SELECT 101 FROM Departments WHERE Departments.department = Employees.department);

#<img width="235" height="109" alt="image" src="https://github.com/user-attachments/assets/5236a421-1020-4539-b275-313f97e5279a" />

# Subquery with 'FROM' clause:
SELECT department FROM
(SELECT * FROM Employees) AS A;

# <img width="156" height="278" alt="image" src="https://github.com/user-attachments/assets/7d9a2f05-2124-480a-ba2a-76f5a1f432f8" />

# Subquery with 'WHERE' and '=' :
SELECT * FROM Employees
WHERE department = (SELECT department FROM Employees WHERE department = 'Sales');

# <img width="628" height="107" alt="image" src="https://github.com/user-attachments/assets/5ebc6b8e-d491-4b79-b6e1-91fa4047485a" />





# MySQL_all_queries-

This repository contains **complete MySQL queries**, including  
concepts, tables, joins, examples, and 40+ SQL query practice problems.

---

## 1️⃣ What is MySQL and why is it popular?

MySQL is an **open-source relational database management system (RDBMS)**  
that uses SQL to store, manage, and analyze data.

### 🔹 Why MySQL is Popular
- Free & open-source  
- Widely used in web development  
- Works with large datasets  
- Integrates with Power BI, Tableau, Python  
- Easy syntax & fast performance  

---

## 2️⃣ Difference Between MySQL and Other RDBMS

| Feature | MySQL | PostgreSQL | SQL Server |
|--------|--------|------------|------------|
| Best For | Web apps | Analytics & complex queries | Enterprises |
| Performance | Fast reads | Advanced queries | Tight MS integration |
| License | Free | Free | Paid |

---

## 3️⃣ SQL vs MySQL

| SQL | MySQL |
|-----|--------|
| Query Language | Database software |
| Used to query DB | Used to store/manage DB |

> **SQL = Language | MySQL = Database using the language**

---

## 4️⃣ Primary Key vs Foreign Key

| Primary Key | Foreign Key |
|-------------|--------------|
| Unique record identifier | References PK of another table |
| Cannot be NULL | Can be NULL |
| One per table | Many allowed |

```sql
CREATE TABLE department (
  dept_id INT PRIMARY KEY,
  dept_name VARCHAR(50)
);

CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  emp_name VARCHAR(50),
  dept_id INT,
  FOREIGN KEY (dept_id) REFERENCES department(dept_id)
);

5️⃣ What Are Indexes?
CREATE INDEX idx_salary ON employees(salary);
✔ Speeds up SELECT
❌ Slows INSERT/UPDATE

6️⃣ CHAR vs VARCHAR
CHAR(10)	VARCHAR(10)
Fixed length	Variable length
Faster	Saves space
Pads spaces	Stores real characters

7️⃣ DELETE vs TRUNCATE vs DROP
DELETE FROM employees WHERE department='HR';
TRUNCATE TABLE employees;
DROP TABLE employees;

8️⃣ Common MySQL Data Types
INT, BIGINT, DECIMAL, FLOAT  
CHAR, VARCHAR, TEXT  
DATE, DATETIME, TIMESTAMP  
BOOLEAN (TINYINT(1))

9️⃣ Check MySQL Version
SELECT VERSION();

🔟 OLTP vs OLAP
OLTP	OLAP
Real-time operations	Reporting
Fast reads/writes	Aggregations
Banking apps	Power BI

1️⃣1️⃣ Get All Records
SELECT * FROM employees;

1️⃣2️⃣ DISTINCT vs GROUP BY
SELECT DISTINCT department FROM employees;
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department;

1️⃣3️⃣ WHERE Clause
SELECT * FROM employees WHERE salary > 50000;

1️⃣4️⃣ WHERE vs HAVING
SELECT department, AVG(salary)
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 50000;

1️⃣5️⃣ SQL Wildcards
SELECT * FROM employees WHERE name LIKE 'A%';
SELECT * FROM employees WHERE name LIKE '_n%';

1️⃣6️⃣ Names Starting With A
SELECT * FROM employees WHERE name LIKE 'A%';

1️⃣7️⃣ ORDER BY
SELECT * FROM employees ORDER BY salary ASC;
SELECT * FROM employees ORDER BY salary DESC;

1️⃣8️⃣ LIMIT in MySQL
SELECT * FROM employees LIMIT 5;

1️⃣9️⃣ Top 5 Highest Salaries
SELECT * FROM employees ORDER BY salary DESC LIMIT 5;

2️⃣0️⃣ Find Duplicates
SELECT name, COUNT(*)
FROM employees
GROUP BY name
HAVING COUNT(*) > 1;

2️⃣1️⃣ NULL Checks
SELECT * FROM employees WHERE manager_id IS NULL;
SELECT * FROM employees WHERE manager_id IS NOT NULL;

2️⃣2️⃣ BETWEEN
SELECT * FROM employees 
WHERE salary BETWEEN 30000 AND 60000;

2️⃣3️⃣ IN vs EXISTS
SELECT * FROM employees 
WHERE department_id IN (1,2,3);

SELECT * FROM employees e
WHERE EXISTS (
    SELECT 1 
    FROM departments d 
    WHERE e.department_id = d.id
);

2️⃣4️⃣ Aliasing
SELECT e.name AS employee_name, e.salary
FROM employees e;

2️⃣5️⃣ Employees With No Department
SELECT * FROM employees
WHERE department_id IS NULL;

🔥 JOINS
2️⃣6️⃣ Types of Joins
Join	Description
INNER	Only matching rows
LEFT	All left + matches
RIGHT	All right + matches
FULL	Not supported → use UNION
CROSS	Combines every row

2️⃣7️⃣ Inner vs Outer Join
Inner Join → Only matches

Outer Join → Includes non-matches

2️⃣8️⃣ LEFT JOIN Example
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d 
ON e.dept_id = d.dept_id;

2️⃣9️⃣ LEFT vs RIGHT JOIN
LEFT JOIN	RIGHT JOIN
Keep left	Keep right

3️⃣0️⃣ CROSS JOIN Example
SELECT product_name, store_name
FROM products
CROSS JOIN stores;

3️⃣1️⃣ Join 3 Tables
SELECT e.emp_name, d.dept_name, l.location_name
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
JOIN locations l ON d.location_id = l.location_id;

3️⃣2️⃣ Self Join Example
SELECT e.emp_name AS Employee, m.emp_name AS Manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.emp_id;

3️⃣3️⃣ JOIN vs UNION
JOIN	UNION
Combines columns	Combines rows

3️⃣4️⃣ UNION vs UNION ALL
SELECT city FROM customers
UNION
SELECT city FROM suppliers;

3️⃣5️⃣ Employees With No Manager
SELECT e.emp_name
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.emp_id
WHERE m.emp_id IS NULL;

3️⃣6️⃣ Many-to-Many Relationship
CREATE TABLE student_course (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);

3️⃣7️⃣ Referential Integrity
Maintained using FOREIGN KEY.

3️⃣8️⃣ If Join Has No Match
INNER JOIN → excluded

LEFT JOIN → included as NULL

3️⃣9️⃣ ON vs USING
-- Using ON
SELECT e.emp_id, d.dept_name
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id;

-- Using USING
SELECT e.emp_name, d.dept_name
FROM employees e
JOIN departments d USING (dept_id);

4️⃣0️⃣ Non-Equi Join
SELECT e.emp_name, s.grade
FROM employees e
JOIN salary_grades s 
ON e.salary BETWEEN s.min_salary AND s.max_salary;

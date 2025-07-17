Input: 
Employee table:
+----+-------+--------+--------------+
| id | name  | salary | departmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Jim   | 90000  | 1            |
| 3  | Henry | 80000  | 2            |
| 4  | Sam   | 60000  | 2            |
| 5  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
Department table:
+----+-------+
| id | name  |
+----+-------+
| 1  | IT    |
| 2  | Sales |
+----+-------+
Output: 
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Jim      | 90000  |
| Sales      | Henry    | 80000  |
| IT         | Max      | 90000  |
+------------+----------+--------+

%sql
CREATE TABLE Employee (
    id INT,
    name STRING,
    salary INT,
    departmentId INT
);

%sql
CREATE TABLE Department (
    id INT,
    name STRING
);

%sql
INSERT INTO Department (id, name) VALUES
(1, 'IT'),
(2, 'Sales');

INSERT INTO Employee (id, name, salary, departmentId) VALUES
(1, 'Joe', 70000, 1),
(2, 'Jim', 90000, 1),
(3, 'Henry', 80000, 2),
(4, 'Sam', 60000, 2),
(5, 'Max', 90000, 1);


#### Solution 1:
```sql
WITH CTE AS (
  SELECT 
    e.name AS employee_name,
    d.name AS department,
    e.salary AS salary
  FROM employee e
  LEFT OUTER JOIN department d
    ON e.departmentId = d.id
),
RankedCTE AS (
  SELECT 
    employee_name, 
    department, 
    salary,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS Rankk
  FROM CTE
)
SELECT employee_name, department, salary
FROM RankedCTE
WHERE Rankk = 1;
```
----------
#### Solution 2:
```sql
WITH MaxSalaries AS (
    SELECT 
        departmentId,
        MAX(salary) AS max_salary
    FROM Employee
    GROUP BY departmentId
)

SELECT 
    E.name AS empname,
    D.name AS deptname,
    E.salary
FROM Employee E
JOIN MaxSalaries M
    ON E.departmentId = M.departmentId AND E.salary = M.max_salary
JOIN Department D
    ON E.departmentId = D.id;
```

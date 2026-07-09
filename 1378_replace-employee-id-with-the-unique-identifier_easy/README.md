# Replace Employee Id With The Unique Identifier

## Problem Description
Table: Employees

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| name          | varchar |
+---------------+---------+
id is the primary key (column with unique values) for this table.
Each row of this table contains the id and the name of an employee in a company.


 

Table: EmployeeUNI

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| unique_id     | int     |
+---------------+---------+
(id, unique_id) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id and the corresponding unique id of an employee in the company.


 

Write a solution to show the unique ID of each user, If a user does not have a unique ID replace just show null.

Return the result table in any order.

The result format is in the following example.

 
Example 1:

Input: 
Employees table:
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |
+----+----------+
EmployeeUNI table:
+----+-----------+
| id | unique_id |
+----+-----------+
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |
+----+-----------+
Output: 
+-----------+----------+
| unique_id | name     |
+-----------+----------+
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |
+-----------+----------+
Explanation: 
Alice and Bob do not have a unique ID, We will show null instead.
The unique ID of Meir is 2.
The unique ID of Winston is 3.
The unique ID of Jonathan is 1.



## My Code
```mysql
# Write your MySQL query statement below
select eu.unique_id ,e.name from  Employees as e left join  EmployeeUNI as eu on  eu.id=e.id;
```

## Code Explanation
The provided MySQL query statement uses a LEFT JOIN operation to combine rows from the `Employees` table and the `EmployeeUNI` table. Here's a step-by-step breakdown of how the code works:

1. `SELECT eu.unique_id, e.name`: This line selects the `unique_id` column from the `EmployeeUNI` table (aliased as `eu`) and the `name` column from the `Employees` table (aliased as `e`).
2. `FROM Employees as e`: This line specifies the `Employees` table as the first table to join, and assigns it the alias `e`.
3. `LEFT JOIN EmployeeUNI as eu`: This line specifies the `EmployeeUNI` table as the second table to join, and assigns it the alias `eu`. The LEFT JOIN operation returns all rows from the `Employees` table and the matching rows from the `EmployeeUNI` table. If there are no matches, the result will contain NULL values for the `EmployeeUNI` table columns.
4. `ON eu.id = e.id`: This line specifies the condition for joining the two tables. The `id` column in the `EmployeeUNI` table must match the `id` column in the `Employees` table for a row to be included in the result.

The result of this query will be a table with two columns: `unique_id` and `name`. The `unique_id` column will contain the unique ID for each employee if it exists in the `EmployeeUNI` table; otherwise, it will contain NULL. The `name` column will contain the name of each employee from the `Employees` table.

## Complexity Analysis
- **Time Complexity:** The time complexity of this query is O(n), where n is the number of rows in the `Employees` table. This is because the query performs a single pass over the `Employees` table and the `EmployeeUNI` table.
- **Space Complexity:** The space complexity of this query is O(n), where n is the number of rows in the result set. This is because the query stores the result set in memory.

## Optimizations
The provided query is already optimal for this problem, as it only requires a single pass over the `Employees` and `EmployeeUNI` tables. However, there are some edge cases to consider:

* If the `id` column in either table is not indexed, the query may be slower due to the join operation. Adding an index to the `id` column in both tables can improve performance.
* If the `EmployeeUNI` table contains duplicate `id` values, the query will return duplicate rows. To avoid this, you can add a DISTINCT keyword to the SELECT statement.
* If the `Employees` table or `EmployeeUNI` table is very large, the query may use a lot of memory. In this case, you can consider using a more efficient join algorithm or partitioning the tables to reduce the amount of data being joined.

## Interview Explanation
Here's an example of how a candidate could verbally explain this solution to an interviewer:

"Okay, so the problem requires us to replace the employee ID with a unique identifier for each employee. We have two tables, `Employees` and `EmployeeUNI`, where `Employees` contains the employee ID and name, and `EmployeeUNI` contains the employee ID and unique ID.

"To solve this problem, I used a LEFT JOIN operation to combine rows from the `Employees` table and the `EmployeeUNI` table. I joined the tables on the `id` column, which is the common column between the two tables.

"The LEFT JOIN operation returns all rows from the `Employees` table and the matching rows from the `EmployeeUNI` table. If there are no matches, the result will contain NULL values for the `EmployeeUNI` table columns.

"In the SELECT statement, I selected the `unique_id` column from the `EmployeeUNI` table and the `name` column from the `Employees` table. This gives us the unique ID for each employee, if it exists, and the employee's name.

"The result of this query will be a table with two columns: `unique_id` and `name`. The `unique_id` column will contain the unique ID for each employee if it exists; otherwise, it will contain NULL.

"I chose to use a LEFT JOIN operation because we want to include all employees in the result, even if they don't have a unique ID. If we had used an INNER JOIN, we would have excluded employees without a unique ID.

"Overall, this solution is efficient because it only requires a single pass over the `Employees` and `EmployeeUNI` tables. However, if the tables are very large, we may need to consider optimizing the join operation or partitioning the tables to reduce the amount of data being joined."
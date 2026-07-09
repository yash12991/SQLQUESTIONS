# Product Sales Analysis I

## Problem Description
Table: Sales

+-------------+-------+
| Column Name | Type  |
+-------------+-------+
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |
+-------------+-------+
(sale_id, year) is the primary key (combination of columns with unique values) of this table.
product_id is a foreign key (reference column) to Product table.
Each row of this table shows a sale on the product product_id in a certain year.
Note that the price is per unit.


 

Table: Product

+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| product_id   | int     |
| product_name | varchar |
+--------------+---------+
product_id is the primary key (column with unique values) of this table.
Each row of this table indicates the product name of each product.


 

Write a solution to report the product_name, year, and price for each sale_id in the Sales table.

Return the resulting table in any order.

The result format is in the following example.

 
Example 1:

Input: 
Sales table:
+---------+------------+------+----------+-------+
| sale_id | product_id | year | quantity | price |
+---------+------------+------+----------+-------+ 
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |
+---------+------------+------+----------+-------+
Product table:
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |
+------------+--------------+
Output: 
+--------------+-------+-------+
| product_name | year  | price |
+--------------+-------+-------+
| Nokia        | 2008  | 5000  |
| Nokia        | 2009  | 5000  |
| Apple        | 2011  | 9000  |
+--------------+-------+-------+
Explanation: 
From sale_id = 1, we can conclude that Nokia was sold for 5000 in the year 2008.
From sale_id = 2, we can conclude that Nokia was sold for 5000 in the year 2009.
From sale_id = 7, we can conclude that Apple was sold for 9000 in the year 2011.



## My Code
```mysql
# Write your MySQL query statement below
select p.product_name,s.year,s.price from   Sales  as s join Product as p on s.product_id =p.product_id
```

## Code Explanation
The provided MySQL query statement is designed to solve the "Product Sales Analysis I" problem. Here's a step-by-step breakdown of how it works:
1. **Selecting Columns:** The query starts by specifying the columns that need to be selected from the database tables. In this case, it's `p.product_name`, `s.year`, and `s.price`.
2. **Table References:** The query references two tables, `Sales` and `Product`, and assigns them aliases `s` and `p` respectively. This is done to shorten the table names and make the query easier to read.
3. **Join Operation:** The query uses an `INNER JOIN` operation to combine rows from the `Sales` and `Product` tables based on a related column. In this case, the related column is `product_id`. The `ON` clause specifies the condition for the join, which is `s.product_id = p.product_id`. This means that only rows with matching `product_id` values in both tables will be included in the results.
4. **Result Set:** The final result set will contain the `product_name`, `year`, and `price` for each sale in the `Sales` table.

## Complexity Analysis
- **Time Complexity:** The time complexity of this query is O(n), where n is the number of rows in the `Sales` table. This is because the query needs to iterate over each row in the `Sales` table once to perform the join operation.
- **Space Complexity:** The space complexity of this query is O(n), where n is the number of rows in the `Sales` table. This is because the query needs to store the result set in memory, which can be as large as the number of rows in the `Sales` table.

## Optimizations
The provided query is already optimal for this problem, as it uses a simple and efficient join operation to retrieve the required data. However, there are a few edge cases to consider:
- **Indexing:** If the `product_id` column in the `Sales` table is not already indexed, adding an index can improve the performance of the join operation.
- **Data Type:** Ensuring that the data type of the `product_id` column is the same in both tables can prevent potential issues with the join operation.
- **NULL Values:** If there are NULL values in the `product_id` column in either table, the query may need to be modified to handle these cases.

## Interview Explanation
Here's how a candidate should verbally explain this solution to an interviewer:
"To solve this problem, I would use a SQL query that joins the `Sales` and `Product` tables based on the `product_id` column. The goal is to retrieve the `product_name`, `year`, and `price` for each sale in the `Sales` table.
"First, I would select the required columns from the tables. In this case, we need `product_name` from the `Product` table, and `year` and `price` from the `Sales` table.
"Next, I would use an inner join operation to combine the rows from the two tables based on the `product_id` column. This ensures that only rows with matching `product_id` values in both tables are included in the results.
"The join operation is performed using the `ON` clause, which specifies the condition for the join. In this case, the condition is `s.product_id = p.product_id`, where `s` and `p` are aliases for the `Sales` and `Product` tables respectively.
"The resulting table will contain the `product_name`, `year`, and `price` for each sale in the `Sales` table. This is achieved by combining the data from the `Sales` and `Product` tables using a simple and efficient join operation.
"In terms of performance, the time complexity of this query is O(n), where n is the number of rows in the `Sales` table. This is because the query needs to iterate over each row in the `Sales` table once to perform the join operation. The space complexity is also O(n), as the query needs to store the result set in memory.
"Overall, this solution is efficient and effective, and it meets the requirements of the problem. It's also worth noting that indexing the `product_id` column in the `Sales` table can improve the performance of the join operation, and ensuring that the data type of the `product_id` column is the same in both tables can prevent potential issues."
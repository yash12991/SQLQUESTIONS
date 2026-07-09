# Find Customer Referee

## Problem Description
Table: Customer

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
| referee_id  | int     |
+-------------+---------+
In SQL, id is the primary key column for this table.
Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.


 

Find the names of the customer that are either:


	referred by any customer with id != 2.
	not referred by any customer.


Return the result table in any order.

The result format is in the following example.

 
Example 1:

Input: 
Customer table:
+----+------+------------+
| id | name | referee_id |
+----+------+------------+
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |
+----+------+------------+
Output: 
+------+
| name |
+------+
| Will |
| Jane |
| Bill |
| Zack |
+------+



## My Code
```mysql
# Write your MySQL query statement below

select name from customer where  referee_id != 2 or referee_id is null;
```

## Code Explanation
The provided code is a MySQL query that solves the "Find Customer Referee" problem. Here's a step-by-step breakdown of how it works:
1. `select name from customer`: This line selects the `name` column from the `customer` table. It's specifying that we only want to retrieve the names of the customers that meet the conditions.
2. `where referee_id != 2 or referee_id is null`: This line filters the results to include only the customers who either have a `referee_id` that is not equal to 2 or have a `referee_id` that is null.
   - `referee_id != 2` checks if the customer was referred by someone with an id other than 2.
   - `referee_id is null` checks if the customer was not referred by anyone.
   - The `or` keyword combines these two conditions, including customers who meet either one of them.

## Complexity Analysis
- **Time Complexity:** The time complexity of this query is O(n), where n is the number of rows in the `customer` table. This is because the query scans each row in the table once to apply the filter conditions.
- **Space Complexity:** The space complexity of this query is O(n), as in the worst-case scenario, the query might return all rows from the `customer` table, requiring space to store the result set.

## Optimizations
The provided code is already quite optimal, as it directly filters the results based on the given conditions without any unnecessary steps. However, to further improve performance, especially on large tables:
- Consider adding an index on the `referee_id` column if this query is frequently executed and the table is very large. This can speed up the filtering process.
- Ensure that the MySQL server has adequate resources (CPU, memory) to handle the query efficiently.

## Interview Explanation
Here's a conversational script on how a candidate should explain this solution to an interviewer:

"Okay, so the problem asks us to find the names of customers who are either referred by any customer with an id not equal to 2 or not referred by any customer at all. To solve this, I used a simple MySQL query that selects the `name` column from the `customer` table where the `referee_id` is either not equal to 2 or is null.

"The key part of the query is the `where` clause, which uses an `or` condition to include both scenarios. The `referee_id != 2` part ensures we get customers referred by anyone except the customer with id 2, and `referee_id is null` gets us customers who weren't referred by anyone.

"In terms of complexity, this query has a time complexity of O(n), where n is the number of rows in the table, because it potentially scans every row once. The space complexity is also O(n) in the worst case, where every row matches the conditions and needs to be included in the result.

"To optimize this query for very large tables, we could consider adding an index on the `referee_id` column, which would speed up the filtering process. But overall, the query is straightforward and directly addresses the problem's requirements."
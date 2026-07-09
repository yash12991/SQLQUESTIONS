# Rising Temperature

## Problem Description
Table: Weather

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id is the column with unique values for this table.
There are no different rows with the same recordDate.
This table contains information about the temperature on a certain day.


 

Write a solution to find all dates' id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

The result format is in the following example.

 
Example 1:

Input: 
Weather table:
+----+------------+-------------+
| id | recordDate | temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
Output: 
+----+
| id |
+----+
| 2  |
| 4  |
+----+
Explanation: 
In 2015-01-02, the temperature was higher than the previous day (10 -> 25).
In 2015-01-04, the temperature was higher than the previous day (20 -> 30).



## My Code
```mysql
# Write your MySQL query statement below
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)
WHERE w1.temperature > w2.temperature;
```

## Code Explanation
The provided MySQL query statement is designed to solve the "Rising Temperature" problem by finding all dates' id with higher temperatures compared to the previous day. Here's a step-by-step breakdown of how the code works:

1. **Table Join**: The code starts by performing a self-join on the `Weather` table, aliased as `w1` and `w2`. This allows the query to compare the temperature of each day with the temperature of the previous day.
2. **Join Condition**: The join condition `w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)` ensures that the rows being compared are consecutive days. The `DATE_ADD` function adds one day to the `recordDate` in `w2`, and the result is compared with the `recordDate` in `w1`.
3. **Where Clause**: The `WHERE` clause filters the results to only include rows where the temperature in `w1` (the current day) is higher than the temperature in `w2` (the previous day).
4. **Select Statement**: Finally, the `SELECT` statement retrieves the `id` of the rows that meet the conditions, which corresponds to the dates with higher temperatures compared to the previous day.

## Complexity Analysis
- **Time Complexity:** The time complexity of this query is O(n), where n is the number of rows in the `Weather` table. This is because the query performs a self-join, which has a time complexity of O(n^2) in the worst case. However, since the join condition is based on the `recordDate` column, the query can take advantage of the index on this column (if it exists) to reduce the number of rows being joined. Additionally, the `WHERE` clause further filters the results, reducing the number of rows being returned.
- **Space Complexity:** The space complexity of this query is O(n), where n is the number of rows in the `Weather` table. This is because the query creates a temporary result set that contains the joined rows, and the maximum size of this result set is proportional to the number of rows in the input table.

## Optimizations
The provided query is already quite efficient, but there are a few potential optimizations to consider:

* **Indexing**: If the `recordDate` column is not already indexed, creating an index on this column could significantly improve the query performance.
* **Limiting the Join**: If the `Weather` table is very large, limiting the join to only include rows within a certain date range could reduce the number of rows being joined and improve performance.
* **Using a Window Function**: Instead of performing a self-join, the query could use a window function (such as `LAG`) to compare the temperature of each day with the temperature of the previous day. This could potentially be more efficient, especially for larger tables.

## Interview Explanation
Here's an example of how a candidate could verbally explain this solution to an interviewer:

"Okay, so the problem is asking us to find all the dates where the temperature is higher than the previous day. To solve this, I'm using a self-join on the `Weather` table. I'm joining the table to itself on the condition that the `recordDate` in the first instance of the table is one day after the `recordDate` in the second instance.

"This allows me to compare the temperature of each day with the temperature of the previous day. I'm using the `DATE_ADD` function to add one day to the `recordDate` in the second instance of the table, and then comparing it with the `recordDate` in the first instance.

"Once I've joined the tables, I'm filtering the results to only include rows where the temperature in the first instance is higher than the temperature in the second instance. This gives me the dates where the temperature is rising.

"Finally, I'm selecting the `id` of these rows, which corresponds to the dates with higher temperatures compared to the previous day.

"In terms of performance, this query has a time complexity of O(n) because it's performing a self-join. However, the join condition is based on the `recordDate` column, which could be indexed to improve performance. The space complexity is also O(n) because we're creating a temporary result set that contains the joined rows.

"One potential optimization could be to limit the join to only include rows within a certain date range, if the `Weather` table is very large. Alternatively, we could use a window function like `LAG` to compare the temperature of each day with the temperature of the previous day, which could potentially be more efficient."
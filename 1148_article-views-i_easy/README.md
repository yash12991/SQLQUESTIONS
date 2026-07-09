# Article Views I

## Problem Description
Table: Views

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |
+---------------+---------+
There is no primary key (column with unique values) for this table, the table may have duplicate rows.
Each row of this table indicates that some viewer viewed an article (written by some author) on some date. 
Note that equal author_id and viewer_id indicate the same person.


 

Write a solution to find all the authors that viewed at least one of their own articles.

Return the result table sorted by id in ascending order.

The result format is in the following example.

 
Example 1:

Input: 
Views table:
+------------+-----------+-----------+------------+
| article_id | author_id | viewer_id | view_date  |
+------------+-----------+-----------+------------+
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |
+------------+-----------+-----------+------------+
Output: 
+------+
| id   |
+------+
| 4    |
| 7    |
+------+



## My Code
```mysql
# Write your MySQL query statement below
select distinct author_id as id from  Views where  author_id=viewer_id  order by  author_id;
```

## Code Explanation
The given MySQL query is designed to solve the "Article Views I" problem on LeetCode. Here's a step-by-step breakdown of how it works:
1. **SELECT DISTINCT**: This statement selects only unique values from the specified column, in this case, `author_id`. The `DISTINCT` keyword ensures that each `author_id` appears only once in the output, even if there are multiple rows in the `Views` table where the same author viewed their own article.
2. **author_id as id**: This renames the `author_id` column to simply `id` in the output. This is done to match the format required by the problem statement.
3. **FROM Views**: This specifies the table from which to retrieve data, which is the `Views` table.
4. **WHERE author_id = viewer_id**: This condition filters the rows to include only those where the `author_id` is equal to the `viewer_id`. This means that only rows where the author of an article is the same person as the viewer are considered.
5. **ORDER BY author_id**: Finally, the results are sorted in ascending order by `author_id`, which is aliased as `id` in the output. This ensures that the authors are listed in order of increasing `id`.

## Complexity Analysis
- **Time Complexity:** The time complexity of this query is O(n log n) due to the sorting operation (`ORDER BY`). The query itself scans the table once, which would be O(n), but the subsequent sorting of the results (even after filtering) is what introduces the logarithmic factor. However, in practice, MySQL's query optimizer might choose an index-based sorting if an index on `author_id` exists, potentially reducing this to O(n) for the scan plus the cost of inserting into the index, but this can depend heavily on the indexing and the data distribution.
- **Space Complexity:** The space complexity is O(n) because, in the worst case, if all authors view their own articles, the result set could contain every row from the table. However, due to the `DISTINCT` keyword, this is reduced to O(k), where k is the number of unique `author_id` values that also appear as `viewer_id`.

## Optimizations
To further optimize this query, consider the following:
- **Indexing**: If this query is run frequently, creating an index on `author_id` and possibly `viewer_id` could significantly speed up the query, especially if the table is very large. This is because indexing would allow MySQL to quickly locate the rows that match the condition `author_id = viewer_id` without having to scan the entire table.
- **Data Normalization**: While not directly affecting the query's performance, ensuring data integrity through normalization (e.g., having separate tables for authors and articles) could simplify queries and reduce data redundancy in the long run.
- **Data Partitioning**: For extremely large datasets, partitioning the `Views` table based on a relevant criteria (like date ranges) could help in speeding up queries that filter by date or other criteria.

## Interview Explanation
If you were explaining this solution to an interviewer, you might start like this:

"First, let's understand what the problem is asking for. We need to find all authors who have viewed at least one of their own articles. This means we're looking for rows in the `Views` table where the `author_id` is the same as the `viewer_id`.

"To solve this, I've written a MySQL query that selects the distinct `author_id` from the `Views` table, but only where `author_id` equals `viewer_id`. This ensures we're only considering instances where the author is also the viewer.

"The query starts by selecting the distinct `author_id`, which we alias as `id` to match the required output format. We then specify the `FROM` clause to indicate we're working with the `Views` table.

"The critical part of the query is the `WHERE` clause, where we filter the rows to only include those where `author_id` equals `viewer_id`. This directly addresses the problem's requirement.

"Finally, we use the `ORDER BY` clause to sort the results by `author_id` in ascending order, ensuring the output is ordered by the author's ID.

"In terms of complexity, the time complexity of this query is O(n log n) due to the sorting, although the actual performance can depend on indexing and data distribution. The space complexity is O(k), where k is the number of unique `author_id` values that also appear as `viewer_id`, due to the `DISTINCT` keyword.

"For further optimization, considering indexing on `author_id` and possibly `viewer_id` could significantly improve performance, especially for very large tables."
# Draw The Triangle 1
## HackerRank - Alternative Queries
> P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5).
> Write a query to print the pattern P(20).

[Problem Description](https://www.hackerrank.com/challenges/draw-the-triangle-1/problem?isFullScreen=true)

## Solution
```sql
SET @number = 21;
SELECT REPEAT('* ', @number := @number - 1) 
FROM information_schema.tables
LIMIT 20;
```

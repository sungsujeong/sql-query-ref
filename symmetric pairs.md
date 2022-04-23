# Symmetric Pairs
## HackerRank - Advanced Join
> You are given a table, Functions, containing two columns: X and Y.
> Two pairs (X1, Y1) and (X2, Y2) are said to be symmetric pairs if X1 = Y2 and X2 = Y1.
> Write a query to output all such symmetric pairs in ascending order by the value of X. List the rows such that X1 ≤ Y1.

[Problem Description](https://www.hackerrank.com/challenges/symmetric-pairs/problem?isFullScreen=true)

## Solution
<details>
  <summary>Click to see the solution!</summary>
  
```sql
 SELECT t.X, t.Y
FROM (SELECT f.X, f.Y
      FROM Functions AS f 
      JOIN Functions AS f1 
      ON f.Y = f1.X  
      WHERE f.X = f1.Y) AS t
GROUP BY t.X, t.Y
HAVING COUNT(t.X) > 1 OR
       t.X < t.Y
ORDER BY t.X;
```

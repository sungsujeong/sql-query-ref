# Placement
## HackerRank - Advanced Join
> You are given three tables: Students, Friends and Packages. Students contains two columns: ID and Name. 
> Friends contains two columns: ID and Friend_ID (ID of the ONLY best friend). 
> Packages contains two columns: ID and Salary (offered salary in $ thousands per month).
> Write a query to output the names of those students whose best friends got offered a higher salary than them. 
> Names must be ordered by the salary amount offered to the best friends. 
> It is guaranteed that no two students got same salary offer.

[Problem Description](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true)

## Solution
```sql
SELECT s.Name
FROM Students AS s 
    INNER JOIN Packages AS p ON s.ID = p.ID
    INNER JOIN Friends AS f ON s.ID = f.ID
    INNER JOIN Packages AS p1 ON f.Friend_ID = p1.ID
WHERE p.Salary < p1.Salary
ORDER BY p1.Salary;
```

# SQL Project Planning
## HackerRank - Advanced Join
> You are given a table, Projects, containing three columns: Task_ID, Start_Date and End_Date. 
> It is guaranteed that the difference between the End_Date and the Start_Date is equal to 1 day for each row in the table.
> If the End_Date of the tasks are consecutive, then they are part of the same project. 
> Samantha is interested in finding the total number of different projects completed.
> Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. 
> If there is more than one project that have the same number of completion days, then order by the start date of the project.

[Problem Description](https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true)

## Solution
<details>
  <summary>Click to see the solution!</summary>
  
```sql
SELECT Start_Date, MIN(End_Date)
FROM (SELECT Start_Date
      FROM Projects
      WHERE Start_Date NOT IN (SELECT End_Date
                               FROM Projects)) p1,
      (SELECT End_Date
       FROM Projects
       WHERE End_Date NOT IN (SELECT Start_Date
                              FROM Projects)) p2
WHERE Start_Date < End_Date
GROUP BY Start_Date
ORDER BY DATEDIFF(MIN(End_Date), Start_Date), Start_Date;
```
## Note:
- p1 selects Start_Date that are not a duplicate in End_Date, picking the first Start_Date
- p2 selects End_Date that are not a duplicate  in Start_Date, picking the last End_Date
- p1 and p2 remove dupliate dates in both Start_Date and End_Date
- A table containing p1 and p2 crosses join the Start_Date and End_Date; appending each End_Date to all Start_Date
- At this point, Start_Date is an unique date that can be grouped
- WHERE clause selects Start_Date before End_Date
  ex) Choose 2015-10-01 2015-10-05, NOT 2015-11-17 2015-10-05
</details>

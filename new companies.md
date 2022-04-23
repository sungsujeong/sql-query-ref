# New Companies
## HackerRank - Basic Join
> Amber's conglomerate corporation just acquired some new companies.
> Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. 
> Order your output by ascending company_code.

[Problem Description](https://www.hackerrank.com/challenges/the-company/problem?isFullScreen=true)

## Solution
<details>
  <summary>Click to see the solution!</summary>

```sql
SELECT C.company_code, 
       C.founder, 
       COUNT(DISTINCT LM.lead_manager_code),
       COUNT(DISTINCT SM.senior_manager_code), 
       COUNT(DISTINCT M.manager_code),
       COUNT(DISTINCT E.employee_code)
FROM Company C, 
     Lead_Manager LM, 
     Senior_Manager SM,
     Manager M,
     Employee E
WHERE C.company_code = LM.company_code AND
      LM.company_code = SM.company_code AND
      SM.company_code = M.company_code AND
      M.company_code = E.company_code
GROUP BY C.company_code, C.founder
ORDER BY C.company_code;
```
</details>

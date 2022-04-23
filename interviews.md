# Interviews
## HackerRank - Advanced Join
> Samantha interviews many candidates from different colleges using coding challenges and contests. Write a query to print the contest_id, hacker_id, name, and the sums of total_submissions, total_accepted_submissions, total_views, and total_unique_views for each contest sorted by contest_id. Exclude the contest from the result if all four sums are 0.

[Problem Description](https://www.hackerrank.com/challenges/interviews/problem)

## Solution
<details>
  <summary>Click to see the solution!</summary>

```sql
SELECT ct.contest_id, 
       ct.hacker_id, 
       ct.name, 
       SUM(ss.sum_tot_sub),
       SUM(ss.sum_tot_accp_sub),
       SUM(vs.sum_tot_v),
       SUM(vs.sum_tot_uni_v)

FROM Contests AS ct
    INNER JOIN Colleges AS cl
    ON ct.contest_id = cl.contest_id
    INNER JOIN Challenges AS ch
    ON cl.college_id = ch.college_id
    LEFT JOIN 
        (SELECT challenge_id, 
                SUM(total_views) AS sum_tot_v, 
                SUM(total_unique_views) AS sum_tot_uni_v
         FROM  View_Stats
         GROUP BY challenge_id) AS vs
    ON ch.challenge_id = vs.challenge_id   
    LEFT JOIN 
        (SELECT challenge_id, 
                SUM(total_submissions) AS sum_tot_sub, 
                SUM(total_accepted_submissions) AS sum_tot_accp_sub
         FROM Submission_Stats
         GROUP BY challenge_id) AS ss
    ON ch.challenge_id = ss.challenge_id
    
GROUP BY ct.contest_id, ct.hacker_id, ct.name

HAVING (SUM(ss.sum_tot_sub) +
        SUM(ss.sum_tot_accp_sub) +
        SUM(vs.sum_tot_v) +
        SUM(vs.sum_tot_uni_v)) > 0
       
ORDER BY ct.contest_id;
```
</details>

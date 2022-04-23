# Contest Leaderboard
## HackerRank - Basic Join
> You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!
> The total score of a hacker is the sum of their maximum scores for all of the challenges. 
> Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. 
> If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. 
> Exclude all hackers with a total score of 0 from your result.

[Problem Description](https://www.hackerrank.com/challenges/contest-leaderboard/problem?isFullScreen=true&h_r=next-challenge&h_v=zen)

## Solution
<details>
  <summary>Click to see the solution!</summary>

```sql
SELECT m.hacker_id, h.name, SUM(m.score) AS tot_score
FROM (SELECT hacker_id, challenge_id, MAX(score) AS score
      FROM Submissions
      GROUP BY hacker_id, challenge_id) AS m
INNER JOIN Hackers AS h
ON m.hacker_id = h.hacker_id
GROUP BY m.hacker_id, h.name
HAVING tot_score > 0
ORDER BY tot_score DESC, m.hacker_id;
```
Note:
- Since the problem asks to select only maximum score, it is better to create a data set containing only max scores and sum them up.
</details>

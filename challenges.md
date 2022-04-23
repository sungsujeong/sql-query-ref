# Challenges
## HackerRank - Basic Join
> Julia asked her students to create some coding challenges. 
> Write a query to print the hacker_id, name, and the total number of challenges created by each student. 
> Sort your results by the total number of challenges in descending order. 
> If more than one student created the same number of challenges, then sort the result by hacker_id. 
> If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

[Problem Description](https://www.hackerrank.com/challenges/challenges/problem?isFullScreen=true)

## Solution
<details>
  <summary>Click to see the solution!</summary>

```sql
SELECT C.hacker_id, H.name, COUNT(C.challenge_id) AS totnumchal
FROM Hackers AS H
INNER JOIN Challenges AS C
ON H.hacker_id = C.hacker_id
GROUP BY C.hacker_id, H.name
HAVING totnumchal = (SELECT COUNT(C1.challenge_id)
                     FROM Challenges AS C1
                     GROUP BY C1.hacker_id
                     ORDER BY COUNT(*) DESC LIMIT 1) OR
       totnumchal NOT IN (SELECT COUNT(C2.challenge_id)
                          FROM Challenges AS C2
                          GROUP BY C2.hacker_id
                          HAVING C2.hacker_id != C.hacker_id)
ORDER BY totnumchal DESC, C.hacker_id;
```
Note:
- The chunck of code seen below selects unique hacker_id(s)
SELECT COUNT(C2.challenge_id)
FROM Challenges AS C2
GROUP BY C2.hacker_id
HAVING C2.hacker_id != C.hacker_id

- The part of code below selects unique number of challenge_id from unique hacker_id
totnumchal NOT IN (~) 
</details>

# Ollivander's Inventory
## HackerRank - Basic Join
> Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.
> Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. 
> Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. 
> If more than one wand has same power, sort the result in order of descending age.

[Problem Description](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem?isFullScreen=true)

## Solution
<details>
  <summary>Click to see the solution!</summary>

```sql
SELECT id, age, coins_needed, power
FROM Wands W
     INNER JOIN Wands_Property WP
     ON W.code = WP.code
WHERE coins_needed = (SELECT MIN(coins_needed)
                      FROM Wands W2
                      INNER JOIN Wands_Property WP2
                      ON W2.code = WP2.code
                      WHERE WP2.is_evil = 0 AND 
                            WP2.age = WP.age AND 
                            W2.power = W.power)
ORDER BY W.power DESC, WP.age DESC;
```
</details>

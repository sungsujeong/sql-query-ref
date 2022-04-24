# Print Prime Numbers
## HackerRank - Alternative Queries
> Write a query to print all prime numbers less than or equal to 1000. 
> Print your result on a single line, and use the ampersand () character as your separator (instead of a space).

[Problem Description](https://www.hackerrank.com/challenges/print-prime-numbers/problem?isFullScreen=true)

## Solution
```sql
DELIMITER $$

CREATE PROCEDURE getPrime(IN n INT, OUT result VARCHAR(1000))
BEGIN
DECLARE j, i, flag INT;   /* Declare variables */
SET j := 2;
SET result := ' ';
WHILE(j < n) DO   /* Loop from 2 to n */
    SET i := 2;
    SET flag := 0;
    
WHILE(i <= j) DO    /* Loop from 2 to j */
    IF(j%i = 0) THEN
        SET flag := flag + 1;
    END if;
    SET i := i + 1;   /* Increment i */
END WHILE;

IF(flag = 1) THEN
SET result := CONCAT(result, j, '&');   /* Concat the prime number with '&' */
END IF;

SET j := j + 1;   /* Increment j */
END WHILE;

END $$

/* Call the procedure */
CALL getPrime(1000, @result);

/* Remove last character */
SELECT SUBSTR(@result, 1, length(@result) - 1);
```

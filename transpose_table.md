# Temperature Record
## HackerRank - SQL Advanced 

## Solution
```sql
SELECT MONTH(t.record_date), MAX(t.maxr), MIN(t.minr), ROUND(AVG(t.avgr))
FROM (SELECT record_date, 
             MAX(CASE WHEN data_type = 'max' THEN data_value ELSE NULL END) AS maxr,
             MAX(CASE WHEN data_type = 'min' THEN data_value ELSE NULL END) AS minr,
             MAX(CASE WHEN data_type = 'avg' THEN data_value ELSE NULL END) AS avgr
       FROM temperature_records
       GROUP BY record_date) AS t
GROUP BY MONTH(t.record_date);
```

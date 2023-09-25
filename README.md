# 585. Investments in 2016
### Problem Link & Description : [Investments in 2016](https://leetcode.com/problems/investments-in-2016/submissions/1058219428/?envType=study-plan-v2&envId=top-sql-50)
## Solution
```sql
/* Write your T-SQL query statement below */



WITH CTE AS (
		SELECT
			*,
			COUNT(lat) OVER(PARTITION BY lat,lon) CountLatLon,
			COUNT(tiv_2015) OVER(PARTITION BY tiv_2015) CountT_2015
		FROM
			Insurance T1
)
SELECT
	ROUND(SUM(tiv_2016),2) tiv_2016 
FROM
	CTE
WHERE
	CountLatLon = 1
AND
	CountT_2015 > 1

What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

### I will check that no city has a bigger '% Revenue' than the whole country that belongs to.
### For example, I will check that no city in Israel has a bigger '% Revenue' than the country Israel.

WITH cte AS 
( 
	SELECT 	SUM(totaltransactionrevenuedivided) AS total_revenue
	FROM 	all_sessions
)

SELECT 	country,
		SUM(totaltransactionrevenuedivided)/total_revenue*100 AS "% Revenue"
FROM 	all_sessions
CROSS JOIN cte
WHERE totaltransactionrevenuedivided IS NOT NULL AND country ='Israel'
GROUP BY country, total_revenue
ORDER BY 2 DESC;

### From here I see that Israel has '% Revenue' of 4.21%
### I will check the cities in Israel now

WITH cte AS 
( 
	SELECT 	SUM(totaltransactionrevenuedivided) AS total_revenue
	FROM 	all_sessions
)

SELECT 	city, 
		SUM(totaltransactionrevenuedivided)/total_revenue*100 AS "% Revenue"
FROM 	all_sessions
CROSS JOIN cte
WHERE 	totaltransactionrevenuedivided IS NOT NULL AND country = 'Israel'
GROUP BY city, total_revenue
ORDER BY 2 DESC;

### I found only 1 city in Israel with the same amount of 4.21%, which is correct.
### I will check how many 'revenue transactions' belong to Israel:

SELECT 	country, COUNT(*)
FROM	all_sessions
WHERE 	totaltransactionrevenuedivided IS NOT NULL
GROUP BY 1;


### Israel has only 1 'Revenue Transaction'

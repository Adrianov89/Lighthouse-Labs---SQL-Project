What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

### I will check that no city has a bigger '% Revenue' than the whole country that belongs to.
### For example, I will check that no city in Israel has a bigger '% Revenue' than the country Israel.

WITH cte AS <br>
( <br>
	SELECT 	SUM(totaltransactionrevenuedivided) AS total_revenue<br>
	FROM 	all_sessions<br>
)

SELECT 	country,<br>
		SUM(totaltransactionrevenuedivided)/total_revenue*100 AS "% Revenue"<br>
FROM 	all_sessions<br>
CROSS JOIN cte<br>
WHERE totaltransactionrevenuedivided IS NOT NULL AND country ='Israel'<br>
GROUP BY country, total_revenue<br>
ORDER BY 2 DESC;<br>

### From here I see that Israel has '% Revenue' of 4.21%
### I will check the cities in Israel now

WITH cte AS <br>
( <br>
	SELECT 	SUM(totaltransactionrevenuedivided) AS total_revenue<br>
	FROM 	all_sessions<br>
)<br>

SELECT 	city,<br> 
		SUM(totaltransactionrevenuedivided)/total_revenue*100 AS "% Revenue"<br>
FROM 	all_sessions<br>
CROSS JOIN cte<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL AND country = 'Israel'<br>
GROUP BY city, total_revenue<br>
ORDER BY 2 DESC;<br>

### I found only 1 city in Israel with the same amount of 4.21%, which is correct.
### I will check how many 'revenue transactions' belong to Israel:

SELECT 	country, COUNT(*)<br>
FROM	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY 1;


### Israel has only 1 'Revenue Transaction'

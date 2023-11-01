Question 1: 

**What's the dataset date range?**

SQL Queries:

SELECT 	MIN(date), <br>
		MAX(date)<br>
FROM 	all_sessions;

Answer: 

**August 01st, 2016 - August 01st, 2017**



Question 2: 

**Assuming 'timeonsite' is in seconds, how do time on site and revenue relate to each other?**

SQL Queries:

SELECT	CASE 	WHEN timeonsite < 300 THEN 'Less than 5 Minutes'<br>
				WHEN timeonsite BETWEEN 300 AND 900 THEN 'Between 5 and 15 minutes'<br>
				WHEN timeonsite > 900 THEN 'More than 15 minutes'<br>
				END AS time_on_site, <br>
		AVG(totaltransactionrevenuedivided) AS average_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY time_on_site<br>
ORDER BY average_revenue DESC;<br>

Answer:

**The people who spend the most money are the ones who spend the least amount of time on the website**



Question 3: 

**How many pages do people visit and how does this impact the revenue?**

SQL Queries:

SELECT 	CASE 	WHEN pageviews < 6 THEN 'Less than 5 Pages'<br>
				WHEN pageviews BETWEEN 6 AND 10 THEN 'Between 5 and 10 Pages'<br>
				WHEN pageviews > 10 THEN 'More than 10 Pages'<br>
				END AS page_views, <br>
				AVG(totaltransactionrevenuedivided) AS average_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY page_views<br>
ORDER BY average_revenue DESC;<br>


Answer:

**People who spend the most money tend to visit between 5-10 pages (or listings).**



Question 4: 

**At which time of the year do people spend more?**

SQL Queries:

SELECT 	TO_CHAR(date, 'Month') As month,<br>
		AVG(totaltransactionrevenuedivided) AS average_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY month<br>
ORDER BY average_revenue DESC;<br>

Answer:

**November, July, and December are the top 3 months where people spend the most**





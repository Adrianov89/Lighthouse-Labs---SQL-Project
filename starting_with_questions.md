Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

**-- Country**

SELECT 	country, <br>
SUM(totaltransactionrevenuedivided) AS total_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY country<br>
ORDER BY total_revenue DESC;<br>

**-- City**

SELECT 	city, <br>
SUM(totaltransactionrevenuedivided) AS total_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY city<br>
ORDER BY total_revenue DESC;<br>

Answer:

**USA is the country with the highest revenue ($13,154.17), whereas San Francisco is the city with the highest revenue ($1,564.32)**



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

**-- Country:**

SELECT 	country, AVG(productquantity) <br>
FROM 	all_sessions <br>
WHERE 	productquantity IS NOT NULL AND transactions IS NOT NULL<br>
GROUP BY 1<br>
ORDER BY 2 DESC;<br><br>


**-- City:**

SELECT 	city, AVG(productquantity) <br>
FROM 	all_sessions <br>
WHERE 	productquantity IS NOT NULL AND transactions IS NOT NULL<br>
GROUP BY 1<br>
ORDER BY 2 DESC;<br>

Answer:

**Note: I used the column 'product quantity' from the 'all_sessions' table.<br><br>
Country: USA with an average product quantity of 7.44<br><br>
City: Atlanta with 4.00**





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

**-- Categories:**

SELECT 	country, v2productcategory,	SUM(totaltransactionrevenuedivided), <br>
		RANK() OVER(PARTITION BY country ORDER BY SUM(totaltransactionrevenuedivided)DESC)<br>
FROM 	all_sessions<br>
WHERE totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY 1,2<br>
ORDER BY 4, 3 DESC;


Answer:

**'Nest-USA' is the number 1 category in the top 3 countries: USA, Israel & Australia.**



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

**-- Products:**

SELECT 	country, v2productname,	SUM(totaltransactionrevenuedivided), <br>
		RANK() OVER(PARTITION BY country ORDER BY SUM(totaltransactionrevenuedivided)DESC)<br>
FROM 	all_sessions<br>
WHERE totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY 1,2<br>
ORDER BY 4,3 DESC;


Answer:

**Most popular products are thermostats, cameras, and smoke alarms.**




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

**-- Country:**

WITH cte AS <br>
( <br>
	SELECT 	SUM(totaltransactionrevenuedivided) AS total_revenue<br>
	FROM 	all_sessions<br>
)

SELECT 	country, <br>
		SUM(totaltransactionrevenuedivided)/total_revenue*100 AS "% Revenue"<br>
FROM 	all_sessions<br>
CROSS JOIN cte<br>
WHERE totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY country, total_revenue<br>
ORDER BY 2 DESC;

**-- City:**

WITH cte AS <br>
( <br>
	SELECT 	SUM(totaltransactionrevenuedivided) AS total_revenue<br>
	FROM 	all_sessions<br>
)

SELECT 	city, <br>
		SUM(totaltransactionrevenuedivided)/total_revenue*100 AS "% Revenue"<br>
FROM 	all_sessions<br>
CROSS JOIN cte<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL AND city != 'not available in demo dataset'<br>
GROUP BY city, total_revenue<br>
ORDER BY 2 DESC;

Answer:

**The United States is the country with the highest level of transaction revenues with over 92%**

**San Francisco is the city with the highest level of transaction revenues with 10.95%**






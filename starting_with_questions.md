Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

-- Country

SELECT 	country, <br>
	</p>SUM(totaltransactionrevenuedivided) AS total_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY country<br>
ORDER BY total_revenue DESC;<br>

-- City

SELECT 	city, 
	SUM(totaltransactionrevenuedivided) AS total_revenue
FROM 	all_sessions
WHERE 	totaltransactionrevenuedivided IS NOT NULL
GROUP BY city
ORDER BY total_revenue DESC;

Answer:

USA is the country with the highest revenue ($13,154.17), whereas San Francisco is the city with the highest revenue ($1,564.32)



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:








Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

-- Country<br>

SELECT 	country, <br>
SUM(totaltransactionrevenuedivided) AS total_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY country<br>
ORDER BY total_revenue DESC;<br>

-- City<br>

SELECT 	city, <br>
SUM(totaltransactionrevenuedivided) AS total_revenue<br>
FROM 	all_sessions<br>
WHERE 	totaltransactionrevenuedivided IS NOT NULL<br>
GROUP BY city<br>
ORDER BY total_revenue DESC;<br>

Answer:

USA is the country with the highest revenue ($13,154.17), whereas San Francisco is the city with the highest revenue ($1,564.32)



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

-- Country: <br>

SELECT 	country, AVG(productquantity) <br>
FROM 	all_sessions <br>
WHERE 	productquantity IS NOT NULL AND transactions IS NOT NULL<br>
GROUP BY 1<br>
ORDER BY 2 DESC;<br><br>


City: <br>
SELECT 	city, AVG(productquantity) <br>
FROM 	all_sessions <br>
WHERE 	productquantity IS NOT NULL AND transactions IS NOT NULL<br>
GROUP BY 1<br>
ORDER BY 2 DESC;<br>

Answer: <br><br>
Note: I used the column 'product quantity' from the 'all_sessions' table.<br><br>
Country: USA with an average product quantity of 7.44<br><br>
City: Atlanta with 4.00





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







